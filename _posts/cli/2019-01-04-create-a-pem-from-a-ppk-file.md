---
layout: post
title: "Create a PEM from a PPK file"
categories: [CLI]
permalink: /create-a-pem-from-a-ppk-file
---

I have been working with aws EC2 instances for a while now. When generating a new key file for ssh login, aws provides a ppk file. I use Bitvise for ssh access and it accepts pem files. So I google every time how to convert ppk file to pem file. Here is the solution:

First and install the putty on linux

```bash
apt-get install putty-tools
```

and then use below command to generate the pem file.

```bash
puttygen server.ppk -O private-openssh -o server.pem
```
