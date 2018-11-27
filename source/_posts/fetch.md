---
title: fetch
date: 2018-11-07 14:11:10
tags:
  - js
---

fetch
<!--more-->

```
var p1 = fetch("https://m.shanghaim.net/api/banner/get1")
  .then(response => {
    if (response.status === 200) {
      return response.json();
    } else {
      throw new Error("Something went wrong on api server!");
    }
  })
  .then(e => e)
  .catch(error => {
    throw error;
  });
var p2 = fetch("https://m.shanghaim.net/api/music/top212")
  .then(response => {
    if (response.status === 200) {
      return response.json();
    } else {
      throw new Error("Something went wrong on api server!");
    }
  })
  .then(e => e)
  .catch(error => {
    throw error;
  });

Promise.all([p1, p2])
  .then(result => {
    console.log(result);
  })
  .catch(error => {
    console.log("ERROR " + error);
  });
```
