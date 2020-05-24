---
layout: post
title: "How to access nested JSON data"
categories: [Javascript]
permalink: /how-to-access-nested-json-data
---

Let's say you have following object:

```javascript
let data = {
  id: 1,
  name: "abc",
  address: {
    streetName: "cde",
    streetId: 2
  }
};
```

Now imagine if sometime, the field `address` is not available. It will throw an error in the code if you try accessing `data.address.streetName` saying `cannot read property 'streetname' of undefined.`

How to solve it?

Here is a function that you can use to get the objects property. It returns the default value if the property does not exist:

```javascript
function findProp(obj, prop, defval) {
  if (typeof defval == "undefined") defval = null;
  prop = prop.split(".");
  for (var i = 0; i < prop.length; i++) {
    if (typeof obj[prop[i]] == "undefined") return defval;
    obj = obj[prop[i]];
  }
  return obj;
}

console.log(findProp(data, "address.streetName", ""));
```

If you don't want to write this kind of function and prefer to use a library instead, well you are lucky. There is a function available in `lodash` for this. See below code on how to use it:

```javascript
const _ = require("lodash");
console.log(_.get(data, "address.streetName", ""));
```

I would recommend to use `lodash` as it also provides more error handling than writing the function yourself.
