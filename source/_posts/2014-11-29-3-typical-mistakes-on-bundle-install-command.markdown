---
layout: post
title: "3 typical mistakes on bundle install command"
date: 2014-11-29 19:51:13 +0200
comments: true
categories: ruby rails
---

## 1. Old rubygem

One day I tried to `bundle install` like always, but… I had it error

```bash
ERROR:  While executing gem ... (Gem::RemoteFetcher::UnknownHostError)
    no such name (https://api.rubygems.org/gems/%any_gem_as_you_want-version%)
```

…instead new gems. Of course, I had not problem with `gem '%any_gem_as_you_want-version%'`. It was smth. else.

Fast googling show me that can catch it error for many reasons. In a my case to resolve a problem I need only update rubygem in single command:

<!--more-->

```bash
gem update --system
```

Also I find that some of gems can be too old for new rubygem. You can check it by `gem outdated` command. If it retrieve you smth., maybe you find useful to update it gems by `gem update %gem_name%`

## 2. Nokogiri error

When I installed nokorigi gem I had an error with big backtrace:

```bash
Building nokogiri using packaged libraries.
Building libxml2-2.8.0 for nokogiri with the following patches applied:
        - 0001-Fix-parser-local-buffers-size-problems.patch
        - 0002-Fix-entities-local-buffers-size-problems.patch
        - 0003-Fix-an-error-in-previous-commit.patch
        - 0004-Fix-potential-out-of-bound-access.patch
        - 0005-Detect-excessive-entities-expansion-upon-replacement.patch
        - 0006-Do-not-fetch-external-parsed-entities.patch
        - 0007-Enforce-XML_PARSER_EOF-state-handling-through-the-pa.patch
        - 0008-Improve-handling-of-xmlStopParser.patch
        - 0009-Fix-a-couple-of-return-without-value.patch
        - 0010-Keep-non-significant-blanks-node-in-HTML-parser.patch
        - 0011-Do-not-fetch-external-parameter-entities.patch
************************************************************************
IMPORTANT!  Nokogiri builds and uses a packaged version of libxml2.

If this is a concern for you and you want to use the system library
instead, abort this installation process and reinstall nokogiri as
follows:

    gem install nokogiri -- --use-system-libraries

If you are using Bundler, tell it to use the option:

    bundle config build.nokogiri --use-system-libraries
    bundle install

However, note that nokogiri does not necessarily support all versions
of libxml2.

For example, libxml2-2.9.0 and higher are currently known to be broken
and thus unsupported by nokogiri, due to compatibility problems and
XPath optimization bugs.
************************************************************************
```

**This is solution:**

```bash
sudo apt-get install libxslt1-dev
```

## 3. Rmagick

With rmagick I retrieve similar problem:

```bash
I have trouble with it:
Gem::Ext::BuildError: ERROR: Failed to build gem native extension.

    /home/adminuser/.rvm/rubies/ruby-2.1.1/bin/ruby extconf.rb                                    
checking for Ruby version >= 1.8.5... yes                                                         
checking for gcc... yes                                                                           
checking for Magick-config... no                                                                  
Can't install RMagick 2.13.2. Can't find Magick-config in /home/adminuser/.rvm/gems/ruby-2.1.1/bin:/home/adminuser/.rvm/gems/ruby-2.1.1@global/bin:/home/adminuser/.rvm/rubies/ruby-2.1.1/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/home/adminuser/.rvm/bin:/home/adminuser/.rvm/bin                                                                                 

*** extconf.rb failed ***                                                                         
Could not create Makefile due to some reason, probably lack of necessary                          
libraries and/or headers.  Check the mkmf.log file for more details.  You may                     
need configuration options.                                                                       

Provided configuration options:                                                                   

extconf failed, exit code 1                                                                       

Gem files will remain installed in /home/adminuser/.rvm/gems/ruby-2.1.1/gems/rmagick-2.13.2 for inspection.                                                                                         
Results logged to /home/adminuser/.rvm/gems/ruby-2.1.1/extensions/x86-linux/2.1.0/rmagick-2.13.2/gem_make.out                                                                                       
An error occurred while installing rmagick (2.13.2), and Bundler cannot continue.
Make sure that `gem install rmagick -v '2.13.2'` succeeds before bundling.
```

Here is solution (be dangerous, it need over 180MB free space):

```bash
sudo apt-get install imagemagick libmagickwand-dev
```

Have a nice web!


