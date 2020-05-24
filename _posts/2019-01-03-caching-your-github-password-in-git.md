---
layout: post
title: "Caching your GitHub password in Git"
categories: [Git]
permalink: /caching-your-github-password-in-git
---

Tired of typing username and password every time you issue a git command in command line? Here is a small command that will save you a lot time:

```bash
$ git config --global credential.helper cache

$ git config --global credential.helper 'cache --timeout=600'
```

I have tried using this on bash in Windows (WSL) and it works fine for me.
