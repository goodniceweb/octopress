---
layout: post
title: "Brug meetup overview"
date: 2015-11-14 21:40:01 +0300
comments: true
---

Today I've visited BRUG meetup and want to share my experience from it.

First of all I want to thank the organizers. You've done a great job guys!
Secondly, the speakers. I didn't feel bored at anytime. Furthermore, lot of tricky parts
were discussed there. [@leopard_me](https://twitter.com/leopard_me) (Alexey Vasiliev)
came to us from Kyiv and [@akirill0v](https://twitter.com/akirill0v) (Alexandr Kirillov) - from Moskov.
It almost 500 miles for both! Guys, your talks were awesome.

I want to leave here some lines about each talk just for myself. So, here we go.

<!-- more -->

### Juriy Koleda - Ruby and Friends

The talk about Apache Thrift. "Hello World" and things like "Guys, don't be scared of it! It's amaizing!"
Speaker's cheerfulness encoraged listeners to keep attention during whole day.

Mostly enough for beginning but right now I haven't got any task which requires another PL. Anyway, thanks [FUT](http://github.com/FUT)

### Julia Oleckaya & Konstantin Reido - Web Push Notifications

They started from history and ended with service for reducing of web push notifications usage.
Girls happen infrequently on Ruby events for us, so we're very glad to hear their talks.

I haven't worked with Web Push Notifications yet but looks like it's really hard to customize it.
I hope, service, which they descibed, will not be off soon. Save it in bookmarks: https://github.com/rpush/rpush

### Alexandr Kirillov - Ruby Object Mapper: Revolution

First pure Ruby talk. The author told about [ROM](https://github.com/rom-rb/rom).
He started from good and bad parts of ActiveRecord and then 
described the basic of how to understand and use ROM.

Mainlines:

- ROM has five main components: Adapters, Relations, Mappers, Commands and Repositories
- don't rewrite whole project from ActiveRecord to ROM just because you heard smth. about it
- if you need smth. customizable: different storages, super custom select and insert data, etc. etc - use ROM;
  for prototyping still use ActiveRecord - don't increase complexity until it will be necessary
- ROM has a lot of storages: if you need save your data in different ways - ROM is for you

### Alexey Vasiliev - Crystal: Ruby syntax and C performance

[@leopard_me](https://twitter.com/leopard_me) introduced Crystal for us. Basics,
similarities and differencies with Ruby, good and bad parts. Full coverage from the speaker - nothing to be added.

Summary:

- compiled language - comparing performance with Ruby do not relevant
- NOT PRODUCTION READY YET
- almost like GoLang on performance
- pretty Ruby syntax
- under ACTIVE development
- has not many tools and utils, here some of them:
  [kemal](https://github.com/kemalcr/kemal) - sinatra inspired web framework
  [amethyst](https://github.com/Codcore/amethyst) - more abstract web framework but not rails :)
  [shards](https://github.com/ysbaddaden/shards) - their bundler (dependency resolver)
  [awesome-list](https://github.com/veelenga/awesome-crystal) - other tools in pretty awesome github style ;)

### Andrew Kumanyaev - As we fled from PostgreSQL or when relational databases can not handle

Have not idea what it was about. I was off during this talk :(

### Sergey Alexeev - Hunting down memory leaks

Lot of fun on latest talk. Thanks [@AlexeevS](https://twitter.com/AlexeevS). On the other hand - he described really
tricky things deeply and gripping. To be honest - memory leaks do happen not so frequently, but when they do,
I want to understand what I need to do to resolve the issue. And the author explained the steps:

- Find the memory leak
- Destroy it

To make the first step you can use a few helpers: [leaky gems list](https://github.com/ASoftCo/leaky-gems),
[New Relic](http://newrelic.com/), and smth. else which I'll describe as soon as presentations will shared.

## Conclusion

I feel not enough Ruby for me - only one pure Ruby talk. But, how Alexey said behind a scenes,
"we know a lot of Ruby things and to have success in such meetup speaker needs to talk about the
things, which stay away from Ruby Community". I think he is mostly right. But when I'm back to my project
I feel maybe we're missing smth. important about Ruby? Maybe we can't cook good OOP?
I still remember [Nothing is Something](https://www.youtube.com/watch?v=OMPfEXIlTVE)
by [@sandimetz](https://twitter.com/sandimetz) from RubyConf2015 and I think
lot of things can be  better implemented than now

Anyway, I was really glad to have such a good weekend like this. Hope you feel the same if you visited this event.
