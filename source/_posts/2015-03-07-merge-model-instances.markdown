---
layout: post
title: "Merge model instances"
date: 2015-03-07 22:18:42 +0200
comments: true
categories: ruby gems
---

Sometimes we can understand that our model field required validation too late. Better late than nerer: you add validation to model and get better new records. But what we can do with old invalid data? 

Just merge it!

Yes, I know: sometimes it can be impossible. For sensitive, personal data maybe. But sometimes it can give very good results.

In one of my projects was need to merge customers records. There some tools for ActiveRecord:

<!--more-->

1. https://github.com/collectiveidea/merger
2. https://github.com/grosser/ar_merge

First - older solution, add `merge!` method to your model instance. Unmaintainable anymore.
Second - newer solution(looks like it work with rails 4).
All above gems provide nice features:
- different built-in protections
- removes merged records
- merge associations as well

Sounds great, but not for MongoId. For MongoId I found only `merge-mongoid`:
https://github.com/fallanic/merge-mongoid

It contains almost all required things, only associations was not merged.

For me it was important so I forked this gem and add missing feature. I also rewrite all tests, because looks like previous maintainer is not Ruby developer =)
So, for now you will find new versions here: https://github.com/goodniceweb/merge-mongoid

Lot of things in TODO:
- merge more association and embedded types correct
- rewrite hard to read code
- tests with differents environments and mongoid versions

Therefore, pull requests are welcome!

Have a nice web!
