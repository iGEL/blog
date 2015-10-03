---
layout: post
title: "Baruco Talks You Should Watch"
date: 2015-10-14T22:58:10+02:00
---

I've been watching all Baruco 2015 talks. First kudos to the organizers. The selection of talks was really great! Here are the talks I liked the best:

## Matz: Ruby 3.0 (or SSS)

<iframe width="710" height="399" src="https://www.youtube-nocookie.com/embed/48iKjUcENRE?rel=0" frameborder="0" allowfullscreen></iframe>
Of course you gotta watch it, or aren't you interested where Ruby is going? Matz explains his ideas for Ruby 3.0 and how he wants to make it easy to upgrade. However, Ruby 3.0 is still far away & they're still experimenting. He announced that we'll see Ruby 2.3 this Xmas and I'm sure we'll also see 2.4 next Xmas before Ruby 3.0 will arrive.

## Sandi Metz: Nothing is Something

<iframe width="710" height="399" src="https://www.youtube-nocookie.com/embed/9mLK_8hKii8?rel=0" frameborder="0" allowfullscreen></iframe>
I'm kinda a fanboy of Sandi, I think she explains important ideas of object oriented programming in a very comprehensible way.
She gave the talk at least twice before at [BathRuby](https://youtu.be/9lv2lBq6x4A) & [RailsConf](https://youtu.be/OMPfEXIlTVE), but even if you watched there, it's still good to get a refresh.
She talks about how to do conditions by just sending messages (so, how to do Ruby without `if`), the Null Object Pattern and why you should avoid inheritance in many cases and should compose your objects instead.
Again, really well explained, definitely recommended!

## Aaron Pattersson: Request & Response

<iframe width="710" height="399" src="https://www.youtube-nocookie.com/embed/1EeWXojdqvU?rel=0" frameborder="0" allowfullscreen></iframe>
Again, I'm biased: I like Aaron's weird humor and trolling the audience.
I also think that his work in Rails (& Ruby) is really valuable, especially since he's cleaning things up and speed them up instead of throwing weird, immature features like ActionCable on the dung hill.
He talks about how to improve Rack and make it take advantage of HTTP/2.
If you don't like his humor, skip the first 5 minutes, but don't skip the talk!

## Yahuda Katz: Rewriting a Ruby C Extension in Rust

<iframe width="710" height="399" src="https://www.youtube-nocookie.com/embed/2BdJeSC4FFI?rel=0" frameborder="0" allowfullscreen></iframe>
Yahuda is not really active in Ruby lands any more <abbr title="As far as I can see">afaics</abbr>, but spends lots of time with Ember.js and Rust.
I like the ideas I hear about Rust, so it's no surprise to me that I also liked his talk.
Yahuda talked about his experiences of reimplementing [fast_blank](https://github.com/SamSaffron/fast_blank) in Rust for fun.
fast_blank is a C implementation of ActiveSupport's `blank?` method, because a typical Rails app spends about 4% of it's CPU time there.
But just by translating nice Ruby code into Rust, they came up with something faster and much more readable than C.
He then takes this example and explains, why it's faster.

## Corey Haines: Fun with Lambdas!

<iframe width="710" height="399" src="https://www.youtube-nocookie.com/embed/gULkBpl3e7c?rel=0" frameborder="0" allowfullscreen></iframe>
Not much practical value for your daily work, but lots of fun with Lambda Calculus in Ruby. Have you implemented lists with just lambdas? Watch it!

## John Cinnamond: Extreme Object-Oriented Ruby.

<iframe width="710" height="399" src="https://www.youtube-nocookie.com/embed/FDs-sSxo2iY?rel=0" frameborder="0" allowfullscreen></iframe>
John takes Sandi's obsession with Object Orientation to the next level.
The result is again not really relevant to real work, but fun.
John defines allows four concepts in his pure OO Ruby: Defining classes, instantiate them, store references to them and send messages to them, but nothing else.
Built in classes like `Fixnum`, `String`, `Array`, `TrueClass` & `FalseClass` violate that and are forbidden.
But can he create a pure OO version of them without breaking the rules? Let's watch!

## Bryan Liles: After you commit that code.

<iframe width="710" height="399" src="https://www.youtube-nocookie.com/embed/xytTA4dKaP0?rel=0" frameborder="0" allowfullscreen></iframe>
A more devops oriented talk, but the average company has to fix things in this area.
The style of presentation is a bit confusing, but I actually liked it because made the talk more interesting.
And the ideas presented where right down my alley, so go watch it.

## The Rest

There were more talks even for the Baruco part that I haven't mentioned here. Most of them are still worth watching. The only talks that I didn't like were from Rin Raeuber and Ernie Miller. You can find all talks in [this playlist](https://youtu.be/CLPgyri3fEY?list=PLe9psSNJBf77PgzYZ2yId2RfUkd9_lMMr).

Let's end with the highlighs video:
<iframe width="710" height="399" src="https://www.youtube-nocookie.com/embed/UUKh1cEfJ0w?rel=0" frameborder="0" allowfullscreen></iframe>
