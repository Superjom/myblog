---
title: "Prefessional Cuda C Reading Note"
date: 2018-12-15T12:54:07+08:00
draft: true
---

# CUDA Programming model

CUDA special features to harness the GPU architectures:

- A way to organize threads on the GPU through a hierarchy
- A way to organize memory on the GPU through a hierarchy 

![](/Users/yanchunwei/project/myblog/static/images/professional-cuda-c/1.png)

## Organizing threads

- All threads spawned by a single kernel launch are collectively called a grid (网格)
  - all threads in the same grid share the same global memory space
- A grid is made up of many thread blocks
  - a thread block is a group of threads that can cooperate with each other using
    - block-local synchronization
    - block-local shared memory
    - threads from different block can not cooperate.
- To distinguish the threads
  - `blockIdx ` (block index within a grid)
  - `threadIdx` (thread index within a block)

```c++
dim3 block(3); // 3, 1, 1
dim3 grid((numElem+block.x-1)/block.x); // x, 1, 1
someKernel<<< grid, block >>>();
```



Changing execution configurations affects performance.
A naive kernel implementation does not generally yield the best performance.
For a given kernel, trying different grid and block dimensions may yield better performance.



## Managing Devices

Some APIs:

- `cudaGetDeviceCount`
- `cudaGetDeviceProperties`
- environment variable `CUDA_VISIBLE_DEVICES` to change the GPU to use in the runtime.

# CUDA Executation Model

CUDA employs a Single Instruction Multiple Thread (SIMT) architecture to manage and execute
threads in groups of 32 called warps.

All the threads in a same warp executes the same instruction at the same time.

- A thread block is scheduled on only one SM.
- once a block is on a SM, it will remain there until end of execution
- One SM can holds more than one block in the same time.

Shared memory and register are precious resource in an SM

- shared memory are partitioned among blocks
- registers are partitoned among threads
- the number of active warps on a SM is limitted for the limitted resource
  - Once a running warp is idle, the SM is free to schedule another avaiable warp from the other block that is resident(without overhead)

## Profing driven development

Developing an HPC application usually involves two major steps:

1. Developing the code for correctness 
2. Improving the code for performance 

Profiling tools provide deep insight into kernel performance and help you identify bottlenecks in
kernels.

## Warp Divergence(32)

GPUs are comparatively simple devices without complex branch prediction mechanisms(unlike CPU).

Make the threads in the same warp execute the same instruction will make higher performance.

e.g. A program with simple assignment operation

- with large amount of blocks, the warp divergent version takes 0.12ms, while the optimized one takes only 0.05ms.
- with small number of blocks, the optimized one is slower(the extra estimitation also result in new overhead).

All in all:

- Warp divergence occurs when threads within a warp take different code paths. 

- Different if-then-else branches are executed serially. 

  The 

  ```c++
  if (...) {} else {}
  ```

  will be optimized and generate codes like

  ```c++
  if (cond) {...}
  if (!cond) {...}
  ```

  so the `else` block will wait for the `if` block, that's why considering the "Warp Divergence" that important.

- Try to adjust branch granularity to be a multiple of warp size to avoid warp divergence. 

- Different warps can execute different code with no penalty on performance. 

## Resource Partitioning

