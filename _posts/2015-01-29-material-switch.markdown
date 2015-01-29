---
layout: post
title: Android Material UI Switch
tags: android material switch
---

I just recently completed upgrading the styling of an android app to conform to google's new [material ui](http://www.google.com/design/spec/material-design/introduction.html). In particular I had to build a few components from scratch as they aren't available to us lowly developers that have to be backwards compatible and support devices that run on things like Android v3.0.

So I have decided to open source the components I wrote. There are a few of these floating around the web already but none of the ones I found really worked the way I would think they would and no offence(well some offence) to their creators but alot of them were insanely messing and overly complicated. This may of course just be someone in a glass house throwing stones though so I'll let you be the judge of the code. Also of course just feel free to grab the bits you need if it's useful to someone else I am happy.

There is a surprising amount of code in this widget, so be warned.

###Example Usage

{% gist RexRonin/695873bf318baaa0b09a example_usage.xml %}

The most important parts (IMO at least):

###Reading in the properties from the xml


###Hooking up the tap input


###Animating the values that describe the switch


###Drawing


There is also a bunch of really tedious code that I'm not going to cover involved in laying out the control when it gets measured and when the size of the control is changed.

Also please forgive my use of `x * 0.5f` instead of `x / 2` its a hangover from game development in c++. I also do the completely unneccessary now ++i instead of i++ at the end of a for loop as well out of habit.

[The complete Gist](https://gist.github.com/RexRonin/b854949aec862f66b75b)

This widget makes use of some of my general utility functions [here](https://gist.github.com/RexRonin/12fa0ba593832c8ed7e2)