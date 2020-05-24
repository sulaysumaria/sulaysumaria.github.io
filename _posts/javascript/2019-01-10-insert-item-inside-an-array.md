---
layout: post
title: "Insert item inside an Array"
categories: [Javascript]
permalink: /insert-item-inside-an-array
---

Inserting an item into an existing array is a daily common task. You can add elements to the end of an array using push, to the beginning using unshift, or to the middle using splice.

Those are known methods, but it doesn’t mean there isn’t a more performant way. Here we go:

### Adding an element at the end

Adding an element at the end of the array is easy with push(), but it can be done in different ways.

```javascript
var arr = [1, 2, 3, 4, 5];
var arr2 = [];

arr.push(6);
arr[arr.length] = 6;
arr2 = arr.concat([6]);
```

Both first methods modify the original array. Don’t believe me? Check the <a href="http://jsperf.com/push-item-inside-an-array" target="_blank" >jsperf</a>

### Add an element at the beginning

Now if we are trying to add an item to the beginning of the array:

```javascript
var arr = [1, 2, 3, 4, 5];

arr.unshift(0);
[0].concat(arr);
```

Here is a little more detail: unshift edits the original array; concat returns a new array. <a href="http://jsperf.com/unshift-item-inside-an-array" target="_blank" >jsperf</a>

### Add an element in the middle

Adding items in the middle of an array is easy with splice, and it’s the most performant way to do it.

```javascript
var items = ["one", "two", "three", "four"];
items.splice(items.length / 2, 0, "hello");
```

I hope these tips will be useful for you.
