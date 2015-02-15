---
layout: post
title: Android Material UI Switch
tags: android material widget switch
is_archive: true
---

I just recently completed upgrading the styling of an android app to conform to google's new [material ui](http://www.google.com/design/spec/material-design/introduction.html). In particular I had to build a few components from scratch as they aren't available to us lowly developers that have to be backwards compatible and support devices that run on things like Android v3.0.

So I have decided to open source the components I wrote. There are a few of these floating around the web already but none of the ones I found really worked the way I would think they would and no offence(well some offence) to their creators but alot of them were insanely messing and overly complicated. This may of course just be someone in a glass house throwing stones though so I'll let you be the judge of the code. Also of course just feel free to grab the bits you need if it's useful to someone else I am happy.

Also before anyone points out the obvious, yes this switch doesn't look exactly like the material one. Google changed it after I built this one and I haven't bothered to update it yet. In theory it shouldn't be super hard to make the line segments render really thickly and with a curved end to make it look exaclty like the google ones. This code should at least get you most of the way.

There is a surprising amount of code in this widget, so be warned.





####Example Usage

{% gist RexRonin/695873bf318baaa0b09a example_usage.xml %}

<br/> 

Now on to the most important parts (IMO at least):




####Reading in the properties from the xml

This is pretty standard, but I think its worth going through the rigmarole so that you can just configure your widgets via xml without having to go through the horror story of half-xml half-java definitions.

{% gist RexRonin/695873bf318baaa0b09a reading_attributes.java %}

 
<br/>



####Animating the values that describe the switch

This is hopefully again pretty straightforward. The switch uses 1 `ValueAnimator` that animates from 0->1 or 1->0 and each tick it modifies the switch paramenters to move from right to left and change colour and fill. It uses an `ArgbEvaluator` to handle the colours changing during the animation.

{% gist RexRonin/695873bf318baaa0b09a animate_values.java %}


<br/>



####Drawing

Again pretty straightforward this just draws out the control using the canvas. 

Just a little note about performance here. You should never be allocating objects in a draw call. You should also try and keep any logic to a minimum(ie. no calculating fibonacci sequences) as it is the easiest way to cause a bunch of preventable performance problems. This might even be able to be made more efficient, I haven't had any issues so far so I have just left it as-is(leave a comment in the [gist](https://gist.github.com/RexRonin/695873bf318baaa0b09a) if you see something any feedback is appreciated).

{% gist RexRonin/695873bf318baaa0b09a drawing.java %}

<br/>



There is also a bunch of really tedious code that I'm not going to cover involved in laying out the control when it gets measured and when the size of the control is changed.

Also please forgive my use of `x * 0.5f` instead of `x / 2`. Its a hangover from game development in c++. I also do the completely unneccessary `++i` instead of `i++` at the end of a for loop as well out of habit.

The complete gist source can be found [here](https://gist.github.com/RexRonin/695873bf318baaa0b09a)

This widget makes use of some of my general utility functions [here](https://gist.github.com/RexRonin/12fa0ba593832c8ed7e2)