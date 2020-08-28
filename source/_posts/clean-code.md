---
title: clean-code
date: 2020-04-03 23:54:45
tags:
  - JS
  - 开发规范
---

如何写出整洁的代码

<!--more-->

**If life is a joke, let us play it.**
**假如生活是一则玩笑，不妨游乐其中**

# Clean Code

一个项目免不了多人合作，每个人用的开发工具，代码风格也各异，自己负责自己的模块还好，但是免不了多人写同一个模块，写的好的代码可以欣赏，写的差异太大，难免会骂街。那么有办法做到大家写的代码尽量统一呢，答案是肯定的，通过一系列工具，让一个项目看起来像是一个人写的。

## editorconfig

解决开发工具的不同

### 常用开发工具

- [sublimetext](http://www.sublimetext.com)
- [vs code](https://code.visualstudio.com)
- [webstorm](https://www.jetbrains.com/webstorm)
- [idea](https://www.jetbrains.com/idea)

### 什么是 EditorConfig？

EditorConfig 有助于维护跨多个编辑器和 IDE 从事同一项目的多个开发人员的一致编码风格。EditorConfig 项目包括一个用于定义编码样式的文件格式和一个文本编辑器插件集合，这些文本编辑器插件使编辑器可以读取文件格式并遵循定义的样式。EditorConfig 文件易于阅读，并且可以与版本控制系统很好地协同工作。

### 如何使用

创建.editorconfig 文件

我使用的是 vs code 需安装插件 EditorConfig for VS Code

> 属性配置

| 属性                       | 作用                         | 值                                                                                                                                                                                                              |
| -------------------------- | ---------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `indent_style`             | 缩进方式                     | 设置为`tab`或`space`分别使用硬标签或软标签。该值不区分大小写。                                                                                                                                                  |
| `indent_size`              | 缩进大小                     | 设置为整数，该整数定义用于每个缩进级别的列数和软标签的宽度（如果支持）。如果等于`tab`，`indent_size`则应将其设置为制表符大小，该大小应为`tab_width`（如果指定）；否则，标签大小由编辑器设置。该值不区分大小写。 |
| `tab_width`                | tab 宽度                     | 设置为整数，定义用于表示制表符的列数。该默认值为，`indent_size`通常不需要指定。                                                                                                                                 |
| `end_of_line`              | 换行方式                     | 设置为`lf`，`cr`或`crlf`控制表示换行的方式。该值不区分大小写。                                                                                                                                                  |
| `charset`                  | 编码                         | 设置为`latin1`，`utf-8`，`utf-8-bom`，`utf-16be`或`utf-16le`控制字符集。`utf-8-bom`不鼓励使用。                                                                                                                 |
| `trim_trailing_whitespace` | 是否删除每行最后多的空白符号 | 设置为`true`删除文件中所有在换行符之前的空白字符，并`false`确保没有。                                                                                                                                           |
| `insert_final_newline`     | 是否以换行为结束             | 设置以`true`确保文件在保存时以换行符结尾，并`false` 确保没有。                                                                                                                                                  |
| `root`                     |                              | 必须在序言中指定。设置为`true`停止`.editorconfig`对当前文件的 文件搜索。该值不区分大小写。                                                                                                                      |

### Demo

```
# http://editorconfig.org
root = true

[*]
charset = utf-8
end_of_line = lf
indent_size = 2
indent_style = space
insert_final_newline = true
max_line_length = 100
trim_trailing_whitespace = true

[*.md]
max_line_length = 0
trim_trailing_whitespace = false

[COMMIT_EDITMSG]
max_line_length = 0
```

## Prettier

代码要漂亮

### 什么是 [Prettier](https://prettier.io)

写的代码不仅要功能强大，也必须漂亮，只要你保存，无论你的代码格式有多散乱，立马整整齐齐，赏心悦目。

vscode 的插件是 prettier-vscode

### 如何使用

创建.editorconfig 文件

我使用的是 vs code 需安装插件 EditorConfig for VS Code

[属性配置](https://prettier.io/docs/en/options.html)

| 属性          | 作用                 | 值                   |
| ------------- | -------------------- | -------------------- |
| `printWidth`  | 每行长度             | string 一般为 80 100 |
| `tabWidth`    | tab 宽度             | string               |
| `singleQuote` | 单引号还是双引号     | boolean              |
| `arrowParens` | 箭头函数是否需要括号 | always avoid         |

### Demo

.prettierrc

```
{
  "printWidth": 100,
  "tabWidth": 2,
  "singleQuote": false,
  "arrowParens": "always"
}
```

## Eslint

### 什么是 eslint

[eslint](https://eslint.org/) 是帮助你找到 javascript 代码中的错误并修复。

### 如何使用

```
npm i eslint -D
```

配置 eslintrc,有不想校验的可在.eslintignore 中配置

### Demo

.eslintrc

```
{
  "parser": "babel-eslint",
  "plugins": ["eslint-plugin-react", "react-hooks"],
  "extends": ["eslint:recommended", "plugin:react/recommended"],
  "settings": {
    "react": {
      "version": "detect"
    }
  },
  "rules": {
    "semi": 2,
    "react/prop-types": 0,
    "no-console": "off",
    "no-undef": "off",
    "react-hooks/rules-of-hooks": "error",
    "react-hooks/exhaustive-deps": "error",
    "react/jsx-handler-names": [
      1,
      {
        "eventHandlerPrefix": "fn",
        "eventHandlerPropPrefix": "on"
      }
    ],
    "react/jsx-no-bind": [
      1,
      {
        "ignoreDOMComponents": false,
        "ignoreRefs": true,
        "allowArrowFunctions": true,
        "allowFunctions": false,
        "allowBind": false
      }
    ],
    "react/sort-comp": [
      "error",
      {
        "order": ["static-methods", "lifecycle", "/^on.+$/", "everything-else", "render"],
        "groups": {
          "lifecycle": [
            "displayName",
            "propTypes",
            "contextTypes",
            "childContextTypes",
            "mixins",
            "statics",
            "defaultProps",
            "constructor",
            "getDefaultProps",
            "state",
            "getInitialState",
            "getChildContext",
            "getDerivedStateFromProps",
            "componentWillMount",
            "UNSAFE_componentWillMount",
            "componentDidMount",
            "componentWillReceiveProps",
            "UNSAFE_componentWillReceiveProps",
            "shouldComponentUpdate",
            "componentWillUpdate",
            "UNSAFE_componentWillUpdate",
            "getSnapshotBeforeUpdate",
            "componentDidUpdate",
            "componentDidCatch",
            "componentWillUnmount"
          ]
        }
      }
    ]
  }
}

```

.eslintignore

```
# Third party
**/node_modules
```

## Stylelint

### 什么是 stylelint

[stylelint](https://stylelint.io) 是强大的 css 代码审查工具，可帮助避免错误并在样式中强制执行约定。

### 如何使用

项目中可使用 stylelint stylelint-config-standard 这两个插件

```
npm i stylelint stylelint-config-standard -D
```

创建.styleintrc.json 文件

```
{
  "extends": "stylelint-config-standard"
}

```

## git hooks

### 什么是 git hooks

[hooks](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks)是一些在`.git/hooks`目录的脚本,安装一些插件可在 git 的特定事件触发调用

```
npm i husky lint-stage -D
```

### Demo

```
 "lint-staged": "lint-staged",
    "lint:css": "stylelint --fix 'src/**/*.scss'",
    "lint:js": "eslint --fix src",
    "prettier": "prettier --write  \"./**/*.{js,jsx,css,scss,md,json}\"",
    "test": "npm run lint"
  },
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged",
      "commit-msg": "commitlint -e $HUSKY_GIT_PARAMS"
    }
  },
  "lint-staged": {
    "src/**/*{js,jsx}": [
      "prettier --write  \"./**/*.{js,jsx,css,scss,md,json}\"",
      "eslint --fix",
      "git add"
    ]
  },
```

## commitlint

### 什么是 commitlint

git 提交信息校验，校验避免无意义的提交信息。

### 如何使用

```
npm install --save-dev @commitlint/config-conventional @commitlint/cli

echo "module.exports = {extends: ['@commitlint/config-conventional']};" > commitlint.config.js
"husky": {
    "hooks": {
      "pre-commit": "npm run test",
      "commit-msg": "commitlint -e $HUSKY_GIT_PARAMS"
    }
  }
```

```
  "precommit": "lint-staged"
  },
  "lint-staged": {
    "src/**/*": [
      "prettier --write  \"./**/*.{js,jsx,css,less,md,json}\"",
      "eslint --fix",
      "git add"
    ]
  },
```

- [commitlint](https://github.com/conventional-changelog/commitlint)
- [@commitlint/config-conventional](https://github.com/conventional-changelog/commitlint/tree/master/@commitlint/config-conventional)

```
[
  'build',
  'ci',
  'chore',
  'docs',
  'feat',
  'fix',
  'perf',
  'refactor',
  'revert',
  'style',
  'test'
]
```

```
echo "foo: some message" # 失败
echo "fix: some message" # 通过
```

## 最后

说了一堆废话，直接看项目吧[react-mobile-kit](https://github.com/FFET/react-mobile-kit)
