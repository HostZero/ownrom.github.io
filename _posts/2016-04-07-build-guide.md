---
layout: post
title: Build Guide
---

# Build Guide

### April 11, 2016

<br>

{% highlight bash %}
"WARNING NOT TESTED FOR MARSHMALLOW"
{% endhighlight %}

<br>

So you want to build OwnROM? Well then, here is how:

First you have to make sure you have a pc that meets the following requirements:

* A Linux or Mac OS system.

It is also possible to build Android in a virtual machine on unsupported systems such as Windows.
If you are running Linux in a virtual machine, you need at least 16GB of RAM/swap and 100GB or more of disk space in order to build the Android tree.

* A 64-bit environment is required for Gingerbread (2.3.x) and newer versions, including the master branch. You can compile older versions on 32-bit systems.

* At least 100GB of free disk space for a checkout, 150GB for a single build, and 200GB or more for multiple builds. If you employ ccache, you will need even more space.

If your pc meets this requirements then your ready to download and get building...

This whole tutorial is made assuming you have the latest Ubuntu version running on your pc, if not click HERE (link will follow)
for our "how to install Ubuntu on my pc" guide...


Now lets get your machine ready to build OwnROM:

Downloadin and installing the Android SDK:

* Go [Here](http://developer.android.com/sdk/index.html) and scroll down to "SDK Tools Only" and download the Linux Version.

* Accept the Terms and Conditions and download the package.

* Extract the SDK package you just downloaded and rename it to: "android-sdk"

* Remove the extracted and renamed folder to your "Home" directory.

* Stay in your home folder and pres "Ctrl + H" and find your ".bashrc" file.

* Open this file with the editor of your choise and scrool all the way down and add this lines at the bottom of the file:

{% highlight bash %}
# Android tools
export PATH=${PATH}:~/android-sdk/tools
export PATH=${PATH}:~/android-sdk/platform-tools
export PATH=${PATH}:~/bin 
{% endhighlight %}
                   
* Safe and close the file.

* Now search for your ".profile" file in your "Home" folder.

* Open it and add this lines at the bottom of the file:

{% highlight bash %}
PATH="$HOME/android-sdk/tools:$HOME/android-sdk/platform-tools:$PATH
{% endhighlight %}

* Save and close.

* Now open a terminal end make this command:

{% highlight bash %}
$ android
{% endhighlight %}

* If the SDK pops up then you have succesfully installed the "Android-SDK"

* In the SDK check every box from the latest android versions and all the build tools and select install

* Accept every license and let them install....

Configure your USB Ports:

* Open a new terminal and type:

{% highlight bash %}
$ sudo apt-get install gksu
{% endhighlight %}

* If the installation is complete type:

{% highlight bash %}
$ gksudo gedit /etc/udev/rules.d/51-android.rules
{% endhighlight %}

* Inside of this blank text file insert:

{% highlight bash %}
#Acer
SUBSYSTEM=="usb", ATTR{idVendor}=="0502", MODE="0666"

#ASUS
SUBSYSTEM=="usb", ATTR{idVendor}=="0b05", MODE="0666"

#Dell
SUBSYSTEM=="usb", ATTR{idVendor}=="413c", MODE="0666"

#Foxconn
SUBSYSTEM=="usb", ATTR{idVendor}=="0489", MODE="0666"

#Garmin-Asus
SUBSYSTEM=="usb", ATTR{idVendor}=="091E", MODE="0666"

#Google
SUBSYSTEM=="usb", ATTR{idVendor}=="18d1", MODE="0666"

#HTC
SUBSYSTEM=="usb", ATTR{idVendor}=="0bb4", MODE="0666"

#Huawei
SUBSYSTEM=="usb", ATTR{idVendor}=="12d1", MODE="0666"

#K-Touch
SUBSYSTEM=="usb", ATTR{idVendor}=="24e3", MODE="0666"

#KT Tech
SUBSYSTEM=="usb", ATTR{idVendor}=="2116", MODE="0666"

#Kyocera
SUBSYSTEM=="usb", ATTR{idVendor}=="0482", MODE="0666"

#Lenevo
SUBSYSTEM=="usb", ATTR{idVendor}=="17EF", MODE="0666"

#LG
SUBSYSTEM=="usb", ATTR{idVendor}=="1004", MODE="0666"

#Motorola
SUBSYSTEM=="usb", ATTR{idVendor}=="22b8", MODE="0666"

#NEC
SUBSYSTEM=="usb", ATTR{idVendor}=="0409", MODE="0666"

#Nook
SUBSYSTEM=="usb", ATTR{idVendor}=="2080", MODE="0666"

#Nvidia
SUBSYSTEM=="usb", ATTR{idVendor}=="0955", MODE="0666"

#OTGV
SUBSYSTEM=="usb", ATTR{idVendor}=="2257", MODE="0666"

#Pantech
SUBSYSTEM=="usb", ATTR{idVendor}=="10A9", MODE="0666"

#Philips
SUBSYSTEM=="usb", ATTR{idVendor}=="0471", MODE="0666"

#PMC-Sierra
SUBSYSTEM=="usb", ATTR{idVendor}=="04da", MODE="0666"

#Qualcomm
SUBSYSTEM=="usb", ATTR{idVendor}=="05c6", MODE="0666"

#SK Telesys
SUBSYSTEM=="usb", ATTR{idVendor}=="1f53", MODE="0666"

#Samsung
SUBSYSTEM=="usb", ATTR{idVendor}=="04e8", MODE="0666"

#Sharp
SUBSYSTEM=="usb", ATTR{idVendor}=="04dd", MODE="0666"

#Sony Ericsson
SUBSYSTEM=="usb", ATTR{idVendor}=="0fce", MODE="0666"

#Toshiba
SUBSYSTEM=="usb", ATTR{idVendor}=="0930", MODE="0666"

#ZTE
SUBSYSTEM=="usb", ATTR{idVendor}=="19D2", MODE="0666"
{% endhighlight %}

* Save and close the file.

* In your terminal you make the following command:

{% highlight bash %}
$ sudo chmod a+r /etc/udev/rules.d/51-android.rules
{% endhighlight %}

Installing Dependencies and Download the OwnROM Source:

we have an automated script ready for you to download the things you need...

Open a new terminal and make the following Commands:

{% highlight bash %}
$ git clone https://github.com/OwnROM/Setup.sh
$ . Setup.sh/setup.sh
{% endhighlight %}

(watch the space between the "." and "Setup.sh/setup.sh")

Follow the instructions and wait for it to finish, this is going to take long time...

Lets start building:

* Make the following commands:

{% highlight bash %}
$ cd path/to/your/ownrom/root/directory
$ . ownrom.sh
{% endhighlight %}

(again the space between "." and ownrom.sh)

* And follow the instructions
 
* When your build is finished whithout any problems you'll see something like this:

{% highlight bash %}
"Package Complete: /home/user/Desktop/OwnROM/out/target/product/<device codename>/OwnROM-ALPHA-0.1-UNOFFICAL-2015.06.02.zip"
{% endhighlight %}

* Head over to this directory and copy the .zip package to your phone and flash it in a custom recovery.

This was it...

Trouble Shooting:

If you have any problems:

Head over to our [G+ community](http://bit.ly/1Fye9Gd) or [contact us](/contribute.html).
