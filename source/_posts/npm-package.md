---
title: npm package
date: 2019-04-06 22:09:01
tags:
  - npm
---

自己写一个 npm 包

<!--more-->

> 注册

先到https://registry.npmjs.org/ 上注册一个账号

> npm adduser

```
jay:jinit jaywang$ npm adduser
Username: scorpionjay
Password:
Email: (this IS public) jay.wang.scorpion@gmail.com
Logged in as scorpionjay on https://registry.npmjs.org/.
```

> npm publish

```
jay:jinit jaywang$ npm publish
npm notice
npm notice 📦  jinit@0.0.1
npm notice === Tarball Contents ===
npm notice 346B package.json
npm notice 402B index.js
npm notice 23B  README.md
npm notice === Tarball Details ===
npm notice name:          jinit
npm notice version:       0.0.1
npm notice package size:  584 B
npm notice unpacked size: 771 B
npm notice shasum:        beb675a0887770284bcdead95d234c387e04797d
npm notice integrity:     sha512-9syIV2wbITn/v[...]8skdo/uvKN6eQ==
npm notice total files:   3
npm notice
+ jinit@0.0.1
```

> update

后面更新版本需要提高下 version

> unpublish

```
jay:jinit jaywang$ npm unpublish jinit --force
npm WARN using --force I sure hope you know what you are doing.
⸨░░░░░░░░░░░░░░░░░░⸩ ⠇ : WARN using --force I sure hope you know what you are doing.
```

24 小时只能发一次
403 Forbidden - PUT https://registry.npmjs.org/jinit - jinit cannot be republished until 24 hours have passed.
