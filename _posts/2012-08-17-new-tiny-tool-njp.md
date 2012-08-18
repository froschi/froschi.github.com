---
layout: default
title: 'New tiny tool: njp'
categories: update
tags: jekyll, automation, code
published: true
---

# New tiny tool: njp

In my little quest to be a little less annoyed every day, I automate things. Today, I discovered that whenever I wanted to create a post for a jekyll-powered site, I had to:

1. Verify the current date (I usually know, of course, but you better check)
2. Come up with a title.
3. Type out the filename, starting with the date formatted in a certain way, then the title of the post.
4. Open the file.
5. Add YAML front matter.
6. Add the title.
7. Add the default category.
8. Start editing.

Or, in most cases, I copied an old file which contains all the defaults and started editing that. That usually failed miserably, because you are bound to miss something. This kind of thing annoys me.

To be a little less annoyed, I created `njp`, or "new jekyll post". This script does the tedious bits of the process above. A session looks as follows:

	$ cd jekyll_dir/_posts
	$ date
	Fri Aug 17 20:58:09 CEST 2012
	$ njp New tiny tool: njp
	$ ls
	2012-08-17-new-tiny-tool-njp.md

There is even a bit of content in there:

	$ cat 2012-08-17-new-tiny-tool-njp.md
	---
	layout: default
	title: 'New tiny tool: njp'
	---
	
	# New tiny tool: njp

This should remind you of the page you are looking at. You can find the code [here at github](https://github.com/froschi/njp).

**Update, 2012/08/18**: I haven't been the first person doing this (no surprise there). [Here is a similar approach](http://www.layouts-the.me/rake/2011/04/23/rake_tasks_for_jekyll/), using a rake task instead of a separate script.
