---
layout: post
title: "Last modified date for a file"
categories: [Node]
permalink: /nodejs-last-modified-date
---

Here is the code to find the last modified date of a file using node's `fs`:

Note: The date returned is in UTC, so make sure to add your timezone's offset to it.

```javascript
const fs = require("fs");
const util = require("util");

let stats = fs.statSync("./README.md");

let mtime = new Date(util.inspect(stats.mtime));

console.log(mtime); // 2019-02-18T17:44:56.798Z
```
