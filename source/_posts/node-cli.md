---
title: node cli
date: 2019-04-05 22:50:49
tags:
---

写一个自己的 CLI

<!--more-->

```
mkdir jinit

头部写
#!/usr/bin/env node

npm i -g

```

```

#!/usr/bin/env node
const path = require("path");
const fs = require("fs");

const currentBaseName = path.basename(process.cwd());

console.log("当前文件名", currentBaseName);

fs.writeFile("README.md", `# ${currentBaseName}`, "utf8", function(error) {
  if (error) {
    console.log(error);
    return false;
  }
  console.log("写入成功");
});

fs.writeFile("index.js", `# import react from "react"`, "utf8", function(
  error
) {
  if (error) {
    console.log(error);
    return false;
  }
  console.log("写入成功");
});

```

## ref

https://www.jianshu.com/p/1c5d086c68fa
