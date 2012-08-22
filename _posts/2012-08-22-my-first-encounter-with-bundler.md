---
layout: default
title: 'My first encounter with bundler'
categories: update
tags: ruby, bundler, code, jekyll
published: true
---

# My first encounter with bundler

When pushing my pages to froschi.github.com, they would sometime not update. Github is processing uploaded pages with jekyll, and I am using jekyll locally to look at my changes before I push them. So, when my pushes did not update the live site, I fired up jekyll on my own computer to find if anything was wrong.

Things looked ok, so I started poking around on the interwebs. It turned out that Github is using two specifc versions of software to process pages: jekyll 0.11.0 (to generate static pages) and liquid 2.2.2, the latter being a template engine. So I figure that the problem might be in a version mismatch; my local install was more up to date:

    $ jekyll -v
    0.11.2

Installing the two packages at the older versions would be easy to do, but how to I get them to be used for testing in this project, and in this project only? Luckily, bundler is here to help.

Bundler is a Ruby gem which can mainly do two things for you. First, it can manage the dependencies of your project, in the sense that it makes sure that all the gems required are actually installed. You can do this by creating a file named `Gemfile` in your project's root directory. In my case, it would contain something like this:

    source :rubygems
    gem "jekyll"
    gem "liquid"
    gem "rdiscount"

I added the `rdiscount` gem, too, because that's what the github pages are using for processing markdown, which is the markup language that I use in my pages. If I want to install all the gems from this `Gemfile`, I run `bundle` as follows:

    $ bundle install

And that's it.

While this is great for making sure that particular software exists on a host which is to run your software, it does not lock the project into a particular version of the software. However, you can just add version numbers to your `Gemfile`:

    source :rubygems
    gem "jekyll", "0.11.0"
    gem "liquid", "2.2.2"
    gem "rdiscount"

These are exact version; you could specify "greater than version X" or "lower than or equal to version Y", if you wanted to. Again, run `bundle install` and `bundler` will install the versions specified, plus dependencies.

Speaking of dependencies. `bundler` will keep version numbers of the gems you specified and those that are depended on in an additional file, called `Gemfile.lock`. Include that file in your repository, its presence prevents `bundle` from walking through the dependency evaluation chain all the time.

But how do we now actually _use_ the dependencies? After all, by default we will get the latest version which is installed. The solution is to run your executable through `bundler`. In my case, I run jekyll as follows:

    $ bundle exec jekyll -v
    0.10.0

Tadaa! This works for the following, longer call, too:

    $ bundle exec jekyll --safe --pygments --server --auto

Neat. The next thing to do is to stick this into a `rake` task, but I am pretty sure you can do that yourself.

**Update**: There was nothing wrong with the pages I uploaded. It's just that sometimes, Github pages need a lot of time to update.
