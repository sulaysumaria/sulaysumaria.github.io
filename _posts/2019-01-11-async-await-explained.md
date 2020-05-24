---
layout: post
title: "async/await explained"
categories: [Javascript]
permalink: /async-await-explained
---

async/await are great things to use. It makes the code more readable and cleaner. It will be good if understood by an example.

Consider following code to create a file on file system and write data to it:

```javascript
// Write data to a file
function createData(dir, file, data, callback) {
  // Open the file for writing
  fs.open(lib.baseDir + dir + "/" + file, "wx", (err, fileDescriptor) => {
    if (!err && fileDescriptor) {
      // Convert data to string
      let stringData = JSON.stringify(data);

      // Write to file and close it
      fs.writeFile(fileDescriptor, stringData, err => {
        if (!err) {
          fs.close(fileDescriptor, err => {
            if (!err) {
              callback(false); // 7 tabs here
            } else {
              callback("Error closing new file");
            }
          });
        } else {
          callback("Error writing to new file");
        }
      });
    } else {
      callback("Could not create new file, it may already exist");
    }
  });
}
```

If you see on line 14, there is a total of 7 tabs. So maximum indentetaion needed is upto 7 tabs. Though it is a white space, it still occupies space on filesystem. The above snippet contains `799` characters in all!

Now lets see how this can be written using async/await

```javascript
// Write data to a file
function createData(dir, file, data) {
  try {
    // Open the file for writing
    let fileDescriptor = fs.openSync(lib.baseDir + dir + "/" + file, "wx");

    // Convert data to string
    let stringData = JSON.stringify(data);

    // Write to file and close it
    fs.writeFileSync(fileDescriptor, stringData);

    fs.closeSync(fileDescriptor);

    // return
    return Promise.resolve();
  } catch (e) {
    console.log(e);
    return Promise.reject(e);
  }
}
```

For this particular case, we are using the sync versions of functions from `fs`. Here the maximum indentation required is only upto 2. And the number of lines are also less. The above snippet contains `490` characters (which is much lesser than `799` characters in original code).

This can be explained with more examples also, will add more examples soon.
