---
layout: post
title: Icon Fonts in Android
tags: android iconfont widget
is_archive: true
---

Are your images bloating the size of your APK files? Do you want a way to make your images scale perfectly without having to splat them out like 4 times for different res devices? Look no further! IconFonts are your friend!

Also I assume alot of people are already using this in android, this is just my version of it.

####What the hell is an IconFont?

This is basically a trick in use most commonly[1] on the web. Its basically using a custom font like a sprite map. Only its better because a font can be made different sizes(due to being vector based?) without loss in quality. It won't work for detailed images, but is absolutely perfect for icons or any image that is basically 2 tone(ie. 1 foreground colour and a background colour). You can even change the colour at runtime. 

####So how much will my APK really shrink if I use this witchcraft?

As an anecdotal example I took our apk from just over 8mb to around the 4.5mb mark. So alot. 

####This is going to be a pain in the arse to implement isn't it?

Not really. Well maybe, depending on your photoshop/image editor of your choice/ability to get someone else to do this for you(in my case someone else did it for me :)). Basically, you need to get all your icon images into svg format and then use something like photoshop or [fontastic](http://fontastic.me/) to create a font from them. Once you have that, the rest is super easy. Just add the resulting `.ttf` file to your android project under `src/main/assets` then use the code in my [gist](https://gist.github.com/RexRonin/263d17c141dd1d7595ad) to render it in your ui. 

####Example usage

{% gist RexRonin/263d17c141dd1d7595ad ExampleUsage.xml %}

<br/>

I'm not going to run through the code 'cos there really isn't much to run through. It just does the standard load strongly typed attributes, then has a simple function to ask the singleton `IconFontManager` to load the Typeface. It then just sets the typeface on itself using the built in function. The `IconFontView` extends `TextView` to make this whole process simpler. 

The complete gist source can be found [here](https://gist.github.com/RexRonin/263d17c141dd1d7595ad)

By the way, this code isn't original obviously. I cobbled it together from a bunch of sources that have been lost in the mists of time, this is just the code that I ended up using that I thought was ok. Also I don't *think* the `IconFontManager.getTypeface` function is threadsafe, meaning that if you did multiple concurrent calls to load fonts you may hit issues. This hasn't impacted my app yet(or at least that I have ever seen or heard reports of) so I'm assuming its safe for now. Just be warned.

[1]: according to me who has done 0 research about this statement