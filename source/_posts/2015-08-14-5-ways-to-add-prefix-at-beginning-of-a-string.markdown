---
layout: post
title: "5 ways to add prefix at beginning of a string"
date: 2015-08-14 15:00:30 +0300
comments: true
categories: ruby 
---

Mostly all of us like their our names. That's why effective email often starts from username.
I had a task where I need to fetch any information about receiver and add it to very beginning of email.

So, challenge accepted and I writing fetch method, then refactor it to class and ta-da: 
we have a chance to guess username. Our emails'll become much pretty. But wait! 
Need to add it name to email at first. And I started think about: which way most common for it case,
how great rubist can implement that? Below I present five variants which I found.

<!--more-->

## 1. Array#join

[Array#join](http://ruby-doc.org/core-2.2.2/Array.html#method-i-join)

What? Array? Did you joke? Sure, not) Lets see:

```ruby
str = "world"
prefix = "Hello, "
result = [prefix, str].join # => "Hello, world"
```

But what about GC in this case? Here we use 3 strings and 1 array. 
Not really careful about a RAM. Lets see another variants.

## 2. Insert

[String#insert](http://ruby-doc.org/core-2.2.2/String.html#method-i-insert)

```ruby
str = "world"
str.insert(0, "Hello, ") # => Hello, world
```

It created only 2 strings, cool! How you can see it also return changed line immediately.
Why I mention that? Please, see #3 and #4

## 3. [with Regexp]

[String#:[]](http://ruby-doc.org/core-2.2.2/String.html#method-i-5B-5D-3D)

```ruby
str = "world"
str[/\A/] = "Hello, " # => "Hello, "
str                   # => "Hello, world"
```

Isn't that awesome? Ruby `String#:[]` method can get `Regexp` like an argument! 
Did you know about it before? I nope) So I glad to gain new experience. 

## 4. [with funny smile]

```ruby
str = "world"
str[0,0] = "Hello, " # => "Hello, "
str                  # => "Hello, world"
```

As you can see from documentation, the squarebrackets method can get a second argument.
And when it is, first arg become an index, which you can specify for replacing
next `%second_arg%` values.

## 5. Prepend

[String#prepend](http://ruby-doc.org/core-2.2.2/String.html#method-i-prepend)

And the last one, but not in relevance.

```ruby
str = "world"
str.prepend("Hello, ") # => "Hello, world"
```

# Conclusion

So, which one you'll use? It's completely your choice. I think that most ruby way to use `prepend`.
But lets see benchmarks at first.

[Benchmark Gist](https://gist.github.com/goodniceweb/85665d4fcfc3f1c0a423)

```bash
Comparison:
       String#insert:  2557799.1 i/s
      String#prepend:  2521598.6 i/s - 1.01x slower
        String#[0,0]:  2422770.0 i/s - 1.06x slower
          Array#join:  1650504.4 i/s - 1.55x slower
       String#[/\A/]:  1065932.3 i/s - 2.40x slower
```

Wow, looks great! Ruby way not only good for eyes but faster as well for it case. Glad to know it.
Are you not?



