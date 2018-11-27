---
title: js array method
date: 2018-09-27 10:14:48
tags:
  - js
---

js array method

<!--more-->

## filter array and return one field

```
/**
 * filter array and return one field
 */
let arr = [
  {
    name: "jay",
    age: 18
  },
  {
    name: "mike",
    age: 20
  },
  {
    name: "jack",
    age: 21
  }
];

// use filter and map
// two loop
let names1 = arr.filter(item => item.age >= 20).map(item => item.name);

// use reduce
// one loop
let names2 = arr.reduce(
  (acc, current) => (current.age >= 20 ? [...acc, current.name] : acc),
  []
);
console.log(names1);
console.log(names2);
```

## Array.from Array.of

arrayLike 对象的 key 为正整数或者０，且有 lenght 属性。函数的 arguments 和 dom 元素集。使用数组的 slice 方法也可以转成数组。

```
Array.from({length:3},(item,index)=>index);//[0,1,2]

```

```
var arr = new Array(2);
console.log(arr.length);//2
arr[0];//undefined
arr[1];//undefined

var arr = new Array(1,2);
console.log(arr.length);//2
arr[0];//undefined
arr[1];//undefined
```

Array 构造函数的传参不同，结果也不同。

```
var arr = Array.of(2);
console.log(arr.length);//1
arr[0];//2
arr[1];//undefined

var arr = Array.of(1,2);
console.log(arr.length);//2
arr[0];//1
arr[1];//2
```
