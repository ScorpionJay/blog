title: js special
date: 2015-11-06 10:34:45
tags:

- js

---

js 的神奇

<!--more-->

## escape unescape

## understanding-primitive-and-getter-setters

```
console.log(a==1&&a==2&a==3);//true
console.log(a===1&&a===2&a===3);//true
```

```
const a = { value : 0 };
a.valueOf = function() {
    return this.value += 1;
};

console.log(a==1 && a==2 && a==3); //true
```

```
var value = 0; //window.value
Object.defineProperty(window, 'a', {
    get: function() {
        return this.value += 1;
    }
});

console.log(a===1 && a===2 && a===3) /true
```

http://theanubhav.com/2018/11/07/understanding-primitive-and-getter-setters/

https://ivweb.io/article.html?_id=100337
