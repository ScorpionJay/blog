---
title: front-end-knowledge
date: 2023-04-24 17:07:37
tags:
---

前端知识体系

<!--more-->

# 前端知识体系

## JavaScript

### 简短的历史

1995 年出来, 网景公司 LiveScript，JScript；EcmaScript 262 TC39

EcamScript Dom Bom

### 数据类型

var、const、let

const 变量指向的内存地址不能变

数据类型分为基本数据类型和引用数据类型。基本数据类型存储在栈里，引用数据类型存储在堆里。
基本数据类型有：null、undefine、string、number、boolean、symbol、bigint
引用数据类型有：Object、Function、Array、RegExp、Date

typeof 操作符判断基本数据类型

```
typeof null === 'object' // 历史原因
typeof undefined === 'undefined'
typeof '' === 'string'
typeof 1 === 'number'
typeof true === 'boolean'
typeof Symbol() === 'symbol'
typeof 1n === 'bigint'
typeof (()=>{}) === 'function'
typeof {} === 'object'
typeof [] === 'object'
```

判断引用数据类型

[instanceof](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/instanceof) 运算符用于检测构造函数的 prototype 属性是否出现在某个实例对象的原型链上

```
function Car(){

}

const autoCar = new Car()

autoCar instanceof Car
autoCar instanceof Object
```

使用 Object 原型对象的 toString 方法

```
Object.prototype.toString.call({}) === '[object Object]'

Object.prototype.toString.call([]) === '[object Array]'

Object.prototype.toString.call('') === '[object String]'

Object.prototype.toString.call(1) === '[object Number]'

Object.prototype.toString.call(true) === '[object Boolean]'

Object.prototype.toString.call(1n) === '[object BigInt]'
```

自定义 Symbol.toStringTag

```
const  arr = [];
arr[Symbol.toStringTag] = 'hack';
Object.prototype.toString.call(arr)  // '[object hack]'
```

objectName 该方法可以放到公共 utils 里

```
function objectName(object) {
  const name = Object.prototype.toString.call(object);
  return name.replace(/^\[object (.*)\]$/, function (m, p0) {
    return p0;
  });
}
```

#### 数据类型介绍

#### String

#### Number

#### Object

> getPrototypeOf

Object.getPrototypeOf() 方法返回指定对象的原型（内部[[Prototype]]属性的值）。

#### Array

#### Date 时间

构造函数有 new 和 无 new 的区别，有 new 返回的是 date 对象，无 new 返回的是字符串 等同于 new Date().toString()

静态方法 now、parse、UTC

为了兼容 ios 不兼容-
可以重写 Date，构造函数、原型链、静态方法

```
const oldDate = Date;

Date = function(){
   arguments[0] = arguments[0].replace(/-/g,'/')
   return new oldDate(...arguments)
}

const a = Date('2022/01/23 11:22:33')
```

### 操作符

```
+ - * /
```

> new 操作符

(1) 在内存中创建一个新对象。
(2) 这个新对象内部的[[Prototype]]特性被赋值为构造函数的 prototype 属性。
(3) 构造函数内部的 this 被赋值为这个新对象（即 this 指向新对象）。
(4) 执行构造函数内部的代码（给新对象添加属性）。
(5) 如果构造函数返回非空对象，则返回该对象；否则，返回刚创建的新对象。

```
function myNew(){
  const obj = {};
  const fn = [].shift.call(arguments);
  obj.__proto__ = (fn.prototype);
  const result = fn.apply(obj,...arguments);
  return result instanceof Object ? result : obj;
}


function myNew(){
  const fn = [].shift.call(arguments);
  const obj = Object.create(fn.prototype);
  const result = fn.apply(obj,...arguments);
  return result instanceof Object ? result : obj;
}
```

### 语句

条件

```
if else

switch()
case a:

    break;
case b:

    break;
default:
```

三元

循环

```
for(let i=1;i<10;i++){

}
```

#### for in

用来遍历对象或者数组

```
for in

for of
```

### 原型链

对象、原型对象、构造函数

```
function Dog(){

}

const dog1 = new Dog()

Dog.prototype.__proto__.constructor // Object
```

### 闭包 clouser

```
function add(){
    let value = 1;

    return function(number){
        value +=number
        return value
    }
}

const foo = add()
foo()
```

### this 指向

### 垃圾回收机制 GC

- 标记法
- 计数法

# 应用

## 防抖截流

### 防抖

事件被触发 n 秒后再执行回调，如果在这 n 内事件又触发，则重新计算时间

```
function debounce(fn,wait){
  let timer = null;

  return function(){
    let context = this;
    const args = arguments;

    if(timer){
      clearTimeout(timer);
      timer = null;
    }

    timer = setTimeout(()=>{
      fn.apply(context,args)
    },wait)
  }
}
```

### 截流

规定的时间内，只有一次触发事件执行

```
function throttle(fn,delay){
  let curTime = Date.now();

  return function(){
    let context = this,
        args = arguments;
        nowTime = Date.now()

    if(nowTime - curTime >= delay){
      curTime = Date.now();
      return fn.apply(context,args)
    }
  }
}
```

## 移动端适配

```
function setRem() {
  // browser width
  const w = document.documentElement.clientWidth;
  // calculate rate
  const fs = (w / 750) * 100;
  // set root html font size
  document.querySelector("html").style.fontSize = fs + "px";
}

setRem();
window.addEventListener("resize",setRem);
```
