---
title: 老项目改造
date: 2023-01-01 15:55:04
tags:
  - react 工具
---

老项目改造，删除无效变量

<!--more-->

## 背景

接手一个项目，历史原因，技术都落后几年了，不想去动，但这几年一直围着这个项目在弄，实在是烦了，不说全翻，对于有点洁癖的还是把实在受不了、碍事的改掉。
没有规矩就没有方圆，eslint，prettier，commitlint 这几个早早就加上，痛苦的就是 lint 虽然加上了，但是要关闭一堆 lint，这加个了寂寞，尤其这玩意 no-unused-vars，
vscode 一看，好多灰色的变量，干了干了。

## 写一个 vscode 插件

可以写一个 vscode 插件，如何写，可参照[官方指导](https://code.visualstudio.com/api/get-started/your-first-extension)

> 安装脚手架

```
npm install -g yo generator-code
```

> 运行脚手架

```
yo code
```

按照选项选择

## 使用 babel

- @babel/parser 生成 AST 语法树
- @babel/traverse 遍历 AST 语法树
- @babel/generator 根据 AST 语法树生成代码
- @babel/types 工具库

### 文件遍历

```
/**
 * list dir files
 */

const fs = require("fs");
const path = require("path");

function dir(basePath) {
  const list = [];

  function _dir(basePath, filePath) {
    filePath = filePath || basePath;

    const files = fs.readdirSync(filePath);
    files.forEach((filename) => {
      const filedir = path.join(filePath, filename);
      const stats = fs.statSync(filedir, function(err, stats) {
        if (err) {
          console.warn("fail");
          return;
        }
      });

      var isFile = stats.isFile();
      var isDir = stats.isDirectory();
      if (isFile) {
        list.push(filedir);
        // console.log(filedir);
      }
      if (isDir) {
        _dir(basePath, filedir);
      }
    });
  }

  _dir(basePath);

  return list;
}

module.exports = dir;
```

### 操作 AST 代码

```
/**
 * @author Jay
 * @since 2022-12-28
 * @description 删除没有使用的代码
 */

const types = require("@babel/types");
const parser = require("@babel/parser");
const traverse = require("@babel/traverse").default;
const generate = require("@babel/generator").default;

function removeUnusedCode(code) {
  // 解析
  const ast = parser.parse(code, {
    sourceType: "module", // module
    plugins: ["jsx"], // jsx
  });

  // 生成ast
  traverse(ast, {
    // 处理 const var let
    VariableDeclaration(path) {
      const { node } = path;
      const { declarations } = node;

      try {
        node.declarations = declarations.filter((declaration) => {
          const { id } = declaration;
          if (types.isObjectPattern(id)) {
            // path.scope.getBinding(name).referenced 判断变量是否被引用
            // 通过filter移除掉没有使用的变量
            id.properties = id.properties.filter((property) => {
              const binding = path.scope.getBinding(property.key.name);
              // referenced 变量是否被引用
              // constantViolations 变量被重新定义的地方
              const { referenced, constantViolations } = binding;
              if (!referenced && constantViolations.length > 0) {
                constantViolations.map((violationPath) => {
                  // 如果变量未使用过，被修改的语句也需要一起移除
                  violationPath.remove();
                });
              }
              return referenced;
            });
            // 如果对象中所有变量都没有被应用，则该对象整个移除
            return id.properties.length > 0;
          } else {
            // const a = 1;
            // @ts-ignore
            const binding = path.scope.getBinding(id.name);
            const { referenced, constantViolations } = binding;
            if (!referenced && constantViolations.length > 0) {
              constantViolations.map((violationPath) => {
                violationPath.remove();
              });
            }
            return referenced;
          }
        });

        if (node.declarations.length === 0) {
          path.remove();
        }
      } catch (error) {}
    },
    // 处理 import
    ImportDeclaration(path) {
      const { node } = path;
      const { specifiers } = node;
      if (!specifiers.length) {
        return;
      }
      node.specifiers = specifiers.filter((specifier) => {
        const { local } = specifier;

        // React 不删除
        if (local.name === "React") return true;

        const binding = path.scope.getBinding(local.name);
        return !!binding.referenced;
      });
      if (node.specifiers.length === 0) {
        path.remove();
      }
    },
    // 处理 function
    FunctionDeclaration(path) {
      const { node } = path;
      const { id } = node;
      const binding = path.scope.getBinding(id.name);
      if (!binding?.referenced) {
        path.remove();
      }
    },

    // 函数调用表达式
    // CallExpression(path) {
    //   // 删除console
    //   if (path.node.callee && t.isIdentifier(path.node.callee.property, { name: "console" })) {
    //     path.remove();
    //   }

    //   // if (path.node.callee && t.isIdentifier(path.node.callee.property, { name: "log" })) {
    //   //   // path.remove();
    //   //   // console.log(path.node.callee.property);
    //   //   path.node.callee.property.name = "info";
    //   // }
    // },
  });

  // 生成code 字符串
  return generate(ast, {
    retainLines: true,
    compact: false,
    auxiliaryCommentAfter: undefined,
    jsescOption: {
      es6: false,
      concise: false,
    },
  }).code;
}

module.exports = removeUnusedCode;

const s = `
const a = 1;
const b = 1;

console.log(a);

const aa = () => {};

import React,     { Component, PureComponent } from "react";

export class Hello extends Component {
  constructor(props) {
    super(props);
    this.state = {
      list: [], //列表
    };
  }

  render() {
    return          <div>test123</div>;
  }
}

export default Hello;

`;

const ss = `
import React from "react";
import { hot } from "react-hot-loader/root";
import { Provider } from "react-redux";
import createStore from "@/redux/store/configureStore";
import Routes from "@/routes";
import "./themes";

class App extends React.Component {
  render() {
    return (
      <Provider store={createStore()}>
        <Routes />
      </Provider>
    );
  }
}

export default hot(App);
`;

const result = removeUnusedCode(ss);
console.log(result);
```

### 测试

```
// 遍历文件
// const files = dir("file path");

files.forEach((item) => {
  if (!item.includes(".js")) return;
  fs.readFile(item, "utf-8", function(err, data) {
    if (err) throw err;
    data = removeUnusedCode(data);
    fs.writeFile(item, data, { flag: "w" }, function(err) {
      if (err) {
        throw err;
      }
    });
  });
  //
});
```
