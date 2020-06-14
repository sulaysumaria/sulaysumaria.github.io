---
layout: post
title: "Clone a specific branch from git"
categories: [Git]
permalink: /clone-a-specific-branch-from-git
---

Here is the command if you want to clone a specific branch. One use case can be you want to clone just `staging` branch on staging server without cloning `master` branch and then switching to `staging` branch.

```bash
git clone --single-branch --branch <branchname> <remote-repo>
```
