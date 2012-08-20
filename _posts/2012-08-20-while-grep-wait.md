---
layout: default
title: 'While grep wait'
categories: update
tags: code, shell
published: true
---

# While grep wait

If you have done any shell scripting at all, you have probably come across a situation where you wanted to wait for a period of time until a character string appeared somewhere. A case in point would be a line that you expect to appear in a log file, or a filename to appear in a directory. And I bet you have been tempted to write something beginning as such:

```bash
while ls -1 | grep foo; do
```
