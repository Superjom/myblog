---
title: "Javascript 笔记"
date: 2018-10-27T15:07:59+08:00
draft: true
---

# 基本信息

## 输出信息
### Using innerHTML

```js
document.getElementById("demo").innerHTML = "1+1";
```

### document.write()
```js
document.write("appended to the tail");
```

### window.alert()
```
window.alert("this is an alert");
```

### console.log()
For debugging purposes.

```js
console.log("debugging"');
```

## Comment

有两种方式：

```js
// xxx
```

或者

```js
/*
 x
 b
 */
```

## Data types

```js
typeof 1 // get number
typeof "a" // get string
typeof null // get object
var a;  // variable without value
typeof a // get undefined
typeof null // get object
```

## 函数

```js
function xx(args...) {
    // statements
}

// 例如
function factorial(n) {
    var res = 1;
    while (n > 1) {
        res *= (n--);
    }
    return res;
}
```

## object

```js
var person = {
    firstName: "First",
    secondName: "Second",
    fullName: function (name) {
        return this.firstName + " " + this.secondName;
    }
};

console.log("FullName: " + person.fullName())
```

## string methods

```js
var ss = "hello world";
ss.indexOf("world");  // get 6
```

其他相似的方法包括：

- lastIndexOf
- slice
- substr
- replace
- toUpperCase
- toLowerCase
- charAt
- split
- 