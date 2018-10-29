---
title: js array method
date: 2018-09-27 10:14:48
tags:
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
