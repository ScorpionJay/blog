---
title: es
date: 2018-09-17 10:10:29
tags:
  - js
---

[babel](http://babeljs.io/) is a JavaScript compiler.
<!--more-->
.babelrc

```
{
"presets":[],
"plugins":[]
}
```

sudo cnpm i babel-cli -g

babel test.js -o test-out.js

babel-polyfill
babel 只会转换 syntax，而新的 api 不会转换

eslint code check
parser

.eslintrc.json

```
{
  "parser": "babel-eslint",
  "plugins": ["react"],
  "rules": {
    "semi": 2
  }
}
```

use es6 in node
babel-register
require add a hook

```
// require("@babel/polyfill");

require("@babel/register")({
  presets: ["@babel/env", "@babel/flow"]
  // "plugins": ["@babel/plugin-transform-runtime"]
});

require("./demo.js");
```

(learn es6)[http://babeljs.io/docs/en/learn]
