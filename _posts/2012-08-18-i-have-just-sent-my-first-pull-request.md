---
layout: default
title: 'I have just sent my first pull request'
categories: ['update']
published: true
---

# I have just sent my first pull request

For most people this won't be a big thing, but I have just sent [my first pull request on github](https://github.com/jedi4ever/veewee/pull/365). For the uninitiated amongst you: it means that I have asked someone else to review and incorporate a change to their code that I have made.

I have been working with Vagrant a lot recently; it's a tool that allows you to quickly create (and throw away) virtual machines, based on pre-defined "base boxes". There is another tool, called veewee, which can be used to create such base boxes.

By default, the boxes which are created by veewee are configured to use dynamically allocated storage: it grows as it's being used by the VM, up to a pre-defined limit. This is great if you don't have a huge amount of space on your local disk to reserve for this purpose. However, this advantage comes at the cost of increased I/O latency, because most of the metadata in the filesystem (and similar shenanigans) is also not allocated at creation time.

VirtualBox, which is what I am using with Vagrant, supports fixed size disks which are wholly allocated at creation time. This option costs more space and takes more time at creation time, but increases the speed at which the VM can access its storage. The command line tool option is `VBoxManage createhd --variant Fixed`.

I have added the `:disk_variant` flag to be an optional argument in a VM configuration template; it's also included as an option to the call to VBoxManage in the background. Dynamic allocation is still the default behaviour.

Let's see what the response to my first pull request looks like.
