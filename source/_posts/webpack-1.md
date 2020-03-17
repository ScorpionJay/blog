---
title: webpack
date: 2019-12-03 21:24:33
tags:
  - webpack
---

学习 webpack 打包

<!--more-->

```
yarn init

yarn add webpack webpack-cli

mkdir src

touch index.js

```

```
 npx webpack --mode=development  src/index.js
```

```
(function (modules) { // webpackBootstrap

  // The module cache
  var installedModules = {};

  // The require function
  function __webpack_require__(moduleId) {

    // Check if module is in cache
    if (installedModules[moduleId]) {
      return installedModules[moduleId].exports;
    }
    // Create a new module (and put it into the cache)
    var module = installedModules[moduleId] = {
      i: moduleId,
      l: false,
      exports: {}
    };

    // Execute the module function
    modules[moduleId].call(module.exports, module, module.exports, __webpack_require__);

    // Flag the module as loaded
    module.l = true;

    // Return the exports of the module
    return module.exports;
  }


  // Load entry module and return exports
  return __webpack_require__(__webpack_require__.s = "./src/index.js");
})
  ({

    "./src/index.js":
      (function (module, exports) {

        eval("const a = \"hello world\";\nconsole.log(a);\n\n\n//# sourceURL=webpack:///./src/index.js?");

      })

  });
```

> 回顾

- 立即执行函数
- call
- 模块
