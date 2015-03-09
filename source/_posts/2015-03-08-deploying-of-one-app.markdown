---
layout: post
title: "deploying of one app"
date: 2015-03-08 00:57:32 +0200
comments: true
categories: ruby rails
---

I have Rails 4.1.8 app. One day I want to deploy it in production. Used `capistrano (3.3.5)` for it.

On server I used Apache2 + Passenger (4.0.59). Install of apache module was fine as usual. But on visit web it raise `stdin is not a tty` passenger error. I looked into [few](https://code.google.com/p/phusion-passenger/issues/detail?id=891) [places](https://code.google.com/p/phusion-passenger/issues/detail?id=891) [for](https://code.google.com/p/phusion-passenger/issues/detail?id=914) [figure out](https://github.com/phusion/passenger/issues/1129) problem but have not success.

Then I removed `apache + passenger` and installed `nginx + unicorn`. It also not worked for me. Any useful info in logs - only "500 error", "smth. went wrong". I felt that something magical going on and disable capistrano recipies. I run it by hand like a daemon. In retrospect I see its mistake.

<!--more-->

Next time I tried to use `thin` instead of `unicorn` but it not worked too. With `puma` also have not results.

Then I tried to run server manually from console and gotcha: puma was blocked by webrick with some custom settings. Here is output:

```bash
$ RAILS_ENV=production bundle exec rails s      
=> Booting Puma
=> Rails 4.1.8 application starting in production on http://0.0.0.0:3000
=> Run `rails server -h` for more startup options
=> Notice: server is listening on all interfaces (0.0.0.0). Consider using 127.0.0.1 (--binding option)
=> Ctrl-C to shutdown server
[2015-02-28 06:32:46] INFO  WEBrick 1.3.1
[2015-02-28 06:32:46] INFO  ruby 2.1.5 (2014-11-13) [i686-linux]
[2015-02-28 06:32:46] INFO  WEBrick::HTTPServer#start: pid=19659 port=2010
^C[2015-02-28 06:32:54] INFO  going to shutdown ...
[2015-02-28 06:32:54] INFO  WEBrick::HTTPServer#start done.
Puma 2.11.1 starting...
* Min threads: 0, max threads: 16
* Environment: production
* Listening on tcp://0.0.0.0:3000
```

Above you can see: puma tried to initialize, reach line `=> Ctrl-C to shutdown server`, than webrick interrupt her flow, initialize and block it.
When I shut down webrick by `^C`. puma continue to initialize and everything work fine.

I tried to search in whole rails repo, in whole source of my app and no found smth. for initialize webrick in production with such strange custom behaviour: always `pid=19659 port=2010`, always block any server you use: passenger, unicorn, thin, puma, and... webrick o_0. Here is output:

```bash
$ RAILS_ENV=production bundle exec rails s webrick
=> Booting WEBrick
=> Rails 4.1.8 application starting in production on http://0.0.0.0:3000
=> Run `rails server -h` for more startup options
=> Notice: server is listening on all interfaces (0.0.0.0). Consider using 127.0.0.1 (--binding option)
=> Ctrl-C to shutdown server
[2015-02-28 06:35:31] INFO  WEBrick 1.3.1
[2015-02-28 06:35:31] INFO  ruby 2.1.5 (2014-11-13) [i686-linux]
[2015-02-28 06:35:31] INFO  WEBrick::HTTPServer#start: pid=19698 port=2010
^C[2015-02-28 06:35:43] INFO  going to shutdown ...
[2015-02-28 06:35:43] INFO  WEBrick::HTTPServer#start done.
[2015-02-28 06:35:43] INFO  WEBrick 1.3.1
[2015-02-28 06:35:43] INFO  ruby 2.1.5 (2014-11-13) [i686-linux]
[2015-02-28 06:35:43] INFO  WEBrick::HTTPServer#start: pid=19698 port=3000
```

I tried to upgrade my rails app to 4.1.9 - same result. Then - to 4.2.0 and it also not work. 

Btw, in development mode everything was fine.

Guys from my team suggested to track every called line of code. I found [Kernel#set_trace_func](http://ruby-doc.org//core-2.2.0/Kernel.html#method-i-set_trace_func) very useful for it, injected it to `bin/rails` script and thats it! Enemy was detected. Thats was `syntaxhighlighter` test from tinymce extensions.
