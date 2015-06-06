---
layout: post
title: ArchLinux 3rd Party App Install Guide for Noobs
tags: productivity linux development noob
---

If you are a Linux noob with a Windows background like me you will probably find yourself looking up all kinds of random stuff that should be easy(and actually really is) but you just don't know how. Since I keep looking these things up I've decided I'm going to document them all on my blog for future reference. So without further ado:

####How to Install a 3rd Party App on ArchLinux(Manjaro)

Notes:
- whenever I say {my-application-xxxx} I obviously mean the application specific file/folder you just downloaded

#####Download the package
Download the tar/zip package of the app you want to install(as an example I'm going to use [Android Studio](https://developer.android.com/sdk/installing/index.html?pkg=studio))
- Extract the tar/zip to a folder:
	- Tar file:
		- `tar -zxvf {my-application-tar-file}.tar.gz`
			- eg. `tar -zxvf ~/Downloads/android-studio.tar.gz`
	- Zip file:
		- be embarressed you don't know how to do this with bash yet :(
		- open thunar
		- double-click the file
		- extract the file		
- Take ownership of the folder/file you just extracted
	- `sudo chown -R root:root {my-application-folder}`
		eg. `sudo chown -R root:root ~/Downloads/android-studio /opt`
- Move the application to the `/opt` directory
	- `sudo mv {my-application-folder}
		eg. `sudo mv ~/Downloads/android-studio /opt`
- Create symlink so you don't have to nav around in bash
	- `sudo ln -s /opt/{my-application-start-file} /usr/local/bin/{my-application-shortcut-name}`
		eg. `sudo ln -s /opt/android-studio/bin/studio.sh /usr/local/bin/android-studio`

Done! Grats, you can now use your new application. 
