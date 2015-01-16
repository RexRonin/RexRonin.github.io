---
layout: post
title: Droid Rage v1
tags: rage android google fragment lifecycle
---

I'm sitting in the courtyard at the back of my house listening to Interpol's "Everything is Wrong" because it suits my mood. I'm taking a little break from working on the Android app for my startup because I nearly flipped my keyboard in anger at discovering yet another little landmine the Android Dev Team decided to lay for unwary users of their framework. So I have decided instead to spend my time seeing if I can get a new entry added to the rotation of programmer slang:

>'droid Rage
>The anger an Android developer feels on a weekly basis at discovering yet another landmine in the Android Framework; Pun on "'roid Rage";

So what caused me to nearly flip my keyboard? [This](http://stackoverflow.com/questions/11353075/how-can-i-maintain-fragment-state-when-added-to-the-back-stack). So why is the fragment transaction pop from backstack behaviour so fury inducing? Where do I start? The thing that made me so angry is that this behaviour means that I need *yet another* nested if statement in the code that initialises my fragments. It is also *yet another* wildly inconsistent behaviour pattern in this framework. So any fragment you write really has to handle the following in their onCreateView function:

1. Created for the first time(_rootView == null && savedInstanceState == null)
2. Loaded from being inactive(_rootView == null && savedInstanceState != null)(I hope this is the case, afaik there is no case that they the could both be non-null)
3. Popped from the back stack(_rootView != null && savedInstanceState == null)

To me the last one is just another blinding case of inconsistency in the framework. Why not when the Fragment gets pushed onto the backstack just call onSaveInstanceState, have it serialise the data it needs and then when it is popped again, have it call onCreateView like it just got restored from the background???

If you sit down and think about it, I'm guessing that this isn't done because of some performance/overhead concern with inflating the Fragment layout again or some other cost invovled in rebuilding it all again when the user hits back(btw, this is all just me guessing about the motivation, it could just have easily been "I hate Simon and hope he gets really mad when he has to implement all his Fragments like this"). IMO this was a mistake. If it is that expensive to create fragments(ie. you are happy for the user to wait around while the Fragment is created the first time) I think the solution would be to make this process quicker, not make yet another place where developers have to make their code significantly more complex and know the inner workings of the framework in order to have an app that functions correctly without bugs and crashes. It also makes it easier for developers to build bad applications. There is a false sense of performance in that after a user pays the cost for a possibly expensive Fragment to be created, as long as they navigate along the back stack the developer can get away with more crappy code.

This highlights my major gripe with the Android framework: It is wildly inconsistent in behaviour and I assume underlying implementation. I'm not sure whether this was caused by the speed with which the initial version was written or that there are just a bunch of people in different parts of the google offices all working on different parts of it with no communication and no oversight so they just implement different bits in the way that suits them best at the time and the people who use the framework can just deal with it. Or that the team is just pretty mediocre and can't actually build a simple or easy to use framework :(


Excellent Android Lifecycle diagram: [Steve Pomeroy](https://plus.google.com/wm/1/+StevePomeroy/posts/HsthxN21Yp1?pid=5914215085941005954&oid=101826485820997153590)
