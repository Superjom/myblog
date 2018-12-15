---
bltitle: "Cuda Init"
date: 2018-10-31T21:57:57+08:00
draft: true
---

作为一个GPU新手，一直没有系统学习和使用过CUDA，下面这一系列博客里，我将记录相关的学习过程。



# 基本模型





# 一个简单的例子

## GPU上的向量加

```c++
__global__
void add(int n, float *x, float *y)
{
  for (int i = 0; i < n; i++)
      y[i] = x[i] + y[i];
}
```

其中，`__global__` 表示，在GPU device上执行，但可以被 host 调用。



`cudaMallocManaged` 和 `cudaMalloc` 不同，前者可以分配CPU和GPU均可以访问的memory，后者只能分配GPU的memory。

GPU 高性能的方式是，利用超级多的core并行加速，下面是一个并行的版本

```c++
__global__
void kernel(float *x, float *y, int n) {
	int idx = threadIdx.x;
	int stride = blockDim.x;
    for (int i = idx; i < n; i += stride) {
    	x[i] += y[i];
    }
}
```



# Stream

相关接口

```c++
cudaStream_t stream;
cudaStreamCreate(&stream);
cudaStreamDestroy(stream); // Sync host until all the tasks in the stream are finished.
```





# Memory

## Device Memory

## Pageable host memory

## Pined(Page-locked) host memory

https://www.cs.virginia.edu/~mwb7w/cuda_support/pinned_tradeoff.html



# Profiler



