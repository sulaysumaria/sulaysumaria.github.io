---
layout: post
title: "Add a new property to Mongoose Document after fetch"
categories: [MongoDB]
permalink: /add-a-new-property-to-mongoose-document-after-fetch
---

Consider following code:

```javascript
try {
  let user = await User.findOne().exec();
  user.email = "johndoe@hacked.com";
  user.save();
} catch (e) {
  console.log(e);
}
```

The above code will not update the user's email. Why? Because the `user` is an immutable mongoose model instance, not a JSON object. So you cannot change property of that object.

Then, how to do so? Well, there are a few ways to do so.

- lean()

```javascript
try {
  let user = await User.findOne()
    .lean() // here
    .exec();
  user.email = "johndoe@hacked.com";
  user.save();
} catch (e) {
  console.log(e);
}
```

- toObject()

```javascript
try {
  let user = await User.findOne().exec();
  user.toObject(); // here
  user.email = "johndoe@hacked.com";
  user.save();
} catch (e) {
  console.log(e);
}
```

If you got any other way to do so, do contact me and I will add your solution here too.
