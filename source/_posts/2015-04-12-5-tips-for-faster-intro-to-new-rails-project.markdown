---
layout: post
title: "5 Tips for Faster Intro to New Rails Project"
date: 2015-04-12 15:15:36 +0300
comments: true
categories: tips
---
What most common problems when you receive new project? No right answer here.
Some people find not so easy to figure out models relationships, some have troubles 
with estimates at beginning.

Here I'll describe what help me to dive intro new project faster. Btw, 
[here](https://bitly.com/a/bitlinks/1aaBwNi) my presentation which I made in five minutes 
before free talk section on [RubyMeetup #12](http://www.meetup.com/kharkov-rb/events/221648244)

<!-- more -->

1. Static Analysis Tools
-----------------------

Ruby have a lot of static analysis tools, ex. [reek](https://github.com/troessner/reek), 
[flay](https://github.com/seattlerb/flay), [ruby-lint](https://github.com/yorickpeterse/ruby-lint), 
etc. etc. But I found most helpful for me the [flog](https://github.com/seattlerb/flog). 
It counts [cyclomatic complexity](http://en.wikipedia.org/wiki/Cyclomatic_complexity) of method. 
So if you may to estimate task, which assumes working with existing code, 
you just see it's value of `flog` output. After that you will have one part of puzzle.

From the other hand, flogging whole project can take much time. Here is tip for make 
static analysis easier:

```bash
flog -gm . > project_name.flog
```

Than, if you need to see flog results, you just execute smth. like this:

```bash
grep ‘method_name’ *.flog
```

2. Project History
------------------

Don't forget that `git log` have a lot of cool options. Here few of them:

* -p
* -L
* --author
* --since
* --until

Also I highly recommend to use `git blame` I your favorite editor/IDE. 
I use vim. If you too, maybe you find useful [git fugitive](https://github.com/tpope/vim-fugitive)
plugin. 

{% img https://blog.xargs.io/presentations/surviving_large_unfamiliar_codebases/images/fugitive-git-blame.png %}

Most frequently I used `blame` with `flog` for build leaderboard of previous developers
in my mind.

Know project history will help you to estimate more precisely.

3. Routes
---------

Where I can find code, which executed on this route? - one of my most common questions in new project.

On big projects routes is permanent as usual. Everybody knows that `rake` command preload whole Rails 
environment. So I propose to execute `rake routes` once.

```bash
rake routes > project_name.routes
```

After above command you can easily find project route by single line command:

```bash
grep “where_is_stupid_route” *.routes
```

4. Graphical Representation of Schema
-------------------------------------

Did you whenever want to see whole bunch of models, attributes and relationships in pretty
graphic? There is nothing easier. Few gems for this already exist.

* https://github.com/voormedia/rails-erd
* https://github.com/preston/railroady

### Rails-erd

{% img http://rails-erd.rubyforge.org/examples/event-forms.png %}

### Railroady

{% img https://camo.githubusercontent.com/c369587851d104f137a32a288f0dd3aa3614c320/68747470733a2f2f7261772e6769746875622e636f6d2f6d70656c7a736865726d616e2f63636d74762f6d61737465722f646f63732f6d6f64656c732e706e67 %}

5. Take a task!
---------------

Only during work you will get real experience. No another way to feel yourself comfortable in new project.


