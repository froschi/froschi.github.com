---
layout: default
title: 'While grep wait'
categories: update
tags: code, shell
published: true
---

# While grep wait

If you have done any shell scripting at all, you have probably come across a situation where you wanted to wait for a period of time until a character string appeared somewhere. A case in point would be a line that you expect to appear in a log file, or a filename to appear in a directory. And I bet you have been tempted to write something beginning like this:

```
while ls -1 | grep foo; do
```

Which is the source of all kinds of troubles, most of which is that it doesn't work, because of the pipe. Then you might have started putting that expression in backticks, which then begs the question what is going to happen to the return value of the command, which is essentially what you are looking for.

Instead of fighting with this (and the subsequent problems that will ensue) you should do something like this:

```
while true; do
  ls -1 | grep foo
  if [ "$?" -eq "0" ]; then
    # do whatever you want to happen when the condition has finally come to pass
    break
  else
    sleep 5
  fi
done
```

What is essentially happening here is that you create a (potentially eternal) loop, in which you run your command over and over, check its return value, sleep if the output didn't satisfy you, and eventually quit as soon as you are happy.

I am using that approach in a script which waits until the resync of a RAID array has completed. During the process, the string `resync` appears in the output of `cat /proc/mdstat`, and it's gone as soon as the process has completed. It has fewer side effects than the first approach, and is a lot easier to read, too.
