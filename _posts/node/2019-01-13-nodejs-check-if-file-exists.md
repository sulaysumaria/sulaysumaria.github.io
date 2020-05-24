---
layout: post
title: "Check if File Exists"
categories: [Node]
permalink: /nodejs-check-if-file-exists
---

Here is the code to check whether file exists or not using node's `fs`:

```javascript
const fs = require("fs");

try {
  let stats = fs.statSync("./README.md");
} catch (e) {
  if (e.code === "ENOENT") {
    // file does not exist.
  }
}
```

There were methods like `fs.exists` and `path.exists` (with their sync versions), but are now deprecated.

From Node js documentation, seems like the best way to go if you plan on opening the file after checking its existence, is to actually open it and handle the errors if it doesn't exists. Because your file could be removed between your exists check and the open function
