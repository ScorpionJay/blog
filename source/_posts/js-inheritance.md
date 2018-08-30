---
title: js inheritance
date: 2018-08-30 23:34:13
tags: js
---

理解JavaScript中如何现实继承
<!--more-->

## 知识点
- 什么是prototype、\_\_proto__
- 构造函数、原型对象、实例的关系
- 原型链
- 操作符new
- 继承

## 什么是prototype、\_\_proto__
Object.prototype可以访问原型对象
Object.prototype的\_\_proto__属性暴露了通过它访问的对象内部[[Prototype]]（一个对象或null）

## 构造函数、原型对象、实例的关系
	
构造函数Object、Array、String、RegExp这些js内置对象、自定对象就是通过function来定义。我们可以通过new操作符来创建实例。构造函数有一个prototype属性可以访问该构造函数的原型对象，而该原型对象有一个constructor属性，指向构造函数，这里形成一个小闭环。通过实例的__proto__属性我们可以访问到该实例对象构造函数的原型对象

~~~
var arr = new Array();
console.log(Array.prototype.constructor === Array);//true
console.log(arr.__proto__ === Array.prototype);//true
~~~

## 原型链
我们访问一个对象的属性，会访问该对象，找不到就在该对象的原型对象上找，找不到就在该原型对象的原型对象上找，直到找到，最顶端是null
~~~
// 下面的代码演示了js引擎如何访问属性
function getProperty(obj,prop){
	if(obj.hasOwnProperty(prop)){
		return obj[prop]
	}else if(obj.__proto__ !== null){
		return getProperty(obj.__proto__,prop)
	}else{
		return undefined
	}
}
var obj = {name:'jay'}
obj.name // jay
getProperty(obj,'name')// jay
~~~

## new
像其他面向对象语言一样，使用new来实例化一个列，那么js里操作符new做了什么
- 1.创建了一个实例，该对象的__proto__指向构造函数的原型对象
- 2.初始化该实例，this指向创建的实例
- 3.返回该实例

~~~
function New(f){
	var obj = {__proto__:f.prototype}; // step 1
	return function(){
		f.apply(obj,arguments); // step 2
		return obj;	// step 3
	}
}

function Dog(name,age){
	this.name = name;
	this.age = age;
}
Dog.prototype.say = function(){
	console.log(this.name,this.age)
}
var dog1 = new Dog('xiaohei',1);
dog1.say();//xiaohei 1
console.log(dog1 instanceof Dog);//true

var dog2 = New(Dog)('xiaobai',2);
dog2.say();//xiaobai 2
console.log(dog2 instanceof Dog);//true
~~~

## 继承
### 原型链继承
~~~
function Animal(name){
	this.name = name;
	this.say = function(){
		console.log(this.name,this.age);
	}
}

function Dog(name,age){
	this.name = name;
	this.age = age;
}
Dog.prototype = new Animal('animal');

var dog = new Dog('xiaohei',1);
dog.say();//xiaohei 1
console.log(dog instanceof Animal); // false
console.log(dog instanceof Dog); // true
~~~
dog的构造函数没有say这个方法，但是Dog的原型对象指向了Animal，所以就有say方法了。其实我们自定义的对象都默认继承了Object，也就是prototype指向Object的实例,所以我们可以使用Object的toString方法。
~~~
function Dog(){}
Dog.prototype = new Object();
~~~
缺点父类的属性被覆盖

### 构造函数继承
~~~
function Animal(name,age){
	this.name = name;
	this.age = age;
	this.say = function(){
		console.log(this.name,this.age);
	}
}

function Dog(){
	Animal.apply(this,arguments);
}

var dog = new Dog('xiaohei',1);
dog.say();//xiaohei 1
console.log(dog instanceof Animal); // false
console.log(dog instanceof Dog); // true
~~~

### 组合继承
~~~
function Animal(name,age){
	this.name = name;
	this.age = age;
	this.say = function(){
		console.log(this.name,this.age);
	}
}

function Dog(){
	Animal.apply(this,arguments);
}

Dog.prototype = new Animal();
Dog.prototype.constructor = Dog;

var dog = new Dog('xiaohei',1);
dog.say();//xiaohei 1
console.log(dog instanceof Animal); // true
console.log(dog instanceof Dog); // true
~~~

### 寄生组合继承
~~~
function Animal(name,age){
	this.name = name;
	this.age = age;
	this.say = function(){
		console.log(this.name,this.age);
	}
}

function Dog(){
	Animal.apply(this,arguments);
}

(function(){
  var Super = function(){};
  Super.prototype = Animal.prototype;
  Dog.prototype = new Super();
})();

Dog.prototype.constructor = Dog; 

var dog = new Dog('xiaohei',1);
dog.say();//xiaohei 1
console.log(dog instanceof Animal); // true
console.log(dog instanceof Dog); // true
~~~

## REF
- [Javascript – How Prototypal Inheritance really works](http://blog.vjeux.com/2011/javascript/how-prototypal-inheritance-really-works.html)
- [js高级程序设计]()
- [Inheritance](https://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)