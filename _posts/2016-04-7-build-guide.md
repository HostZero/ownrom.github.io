---
layout: post
title: Build Guide 
---

**"Warning this build guide is in the works, if something dosent work or needs to be updated please contact [Victor Linfield](https://plus.google.com/+VictorLinfield) via hangouts."**

### Introduction

So you want to build OwnROM? Well then, here is how.

### What you’ll need

* An Android device supported by Cyanogenmod

* A relatively recent Linux computer with a reasonable amount of RAM (aim for 8 GB+) and about 50 GB of free storage (100 GB or more if you enable ccache) 

Note: This guide assumes you have Ubuntu installed on your computer. If you don't have it installed check out our Ubuntu installation guide (link coming soon) - Other Linux distributions will also work, however certain packages and scripts will have to be changed to work on these systems. 

Note: using SSDs results in considerably faster build times than traditional hard drives

* A USB cable compatible with the your device (typically micro USB, but older devices may use mini USB or have a proprietary cable)

* A decent Internet connection & reliable electricity 

* Some familiarity with basic Android operation and terminology. It would help if you've installed custom ROMs on other devices and are familiar with recovery. It may also be useful to know some basic command line concepts such as cd for “change directory”, the concept of directory hierarchies, that in Linux they are separated by /, etc.

Note: You want to use a 64-bit version of Linux. A 32-bit Linux environment will only work if you are building CyanogenMod 6 and older. 

So lets begin!

### Automatically

We now have a setup/build script located on [Github](https://github.com/OwnROM/Setup.sh) 

All you have to do is run the script from your home directory and follow the onscreen instructions.

Includes the following:

Running the script initially will ask you for settings to run the other sripts included

Any other time running the script will give you a menu with the following options:

* Setup - Setup script to install needed software to build for OwnROM, only needed to run once 

* Build - Build for OwnROM and options to sync before building

* Sync - Sync OwnROM sources

* Settings - Rerun the setup script to change settings

### Manualy

### Prepare the Build Environment

Note: You only need to do these steps the first time you build. If you previously prepared your build environment and have downloaded the OwnROM source code for another device, skip to Prepare the device-specific code.

### Install the SDK

If you have not previously installed adb and fastboot, install the Android SDK. "SDK" stands for Software Developer Kit, and it includes useful tools that you can use to flash software, look at the system logs in real time, grab screen shots, and more-- all from your computer.

* Go [Here](http://developer.android.com/sdk/index.html) and scroll down to "SDK Tools Only" and download the Linux Version.

* Accept the Terms and Conditions and download the package.

* Extract the SDK package you just downloaded and rename it to: "android-sdk"

* Remove the extracted and renamed folder to your "Home" directory.

* Stay in your home folder and pres "Ctrl + H" and find your ".bashrc" file.

* Open this file with the editor of your choose and scroll all the way down and add this lines at the bottom of the file:

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

* If the SDK pops up then you have successfully installed the "Android-SDK"

* In the SDK check every box from the latest android versions and all the build tools and select install

* Accept every license and let them install....

### Configure your USB Ports:

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

### Install the Build Packages 

Several "build packages" are needed to build OwnROM. You can install these using the package manager of your choice.

You'll need:

{% highlight bash %}
$ sudo apt-get install bison build-essential curl flex git gnupg gperf libesd0-dev liblz4-tool libncurses5-dev libsdl1.2-dev libwxgtk2.8-dev libxml2 libxml2-utils lzop maven openjdk-7-jdk openjdk-7-jre pngcrush schedtool squashfs-tools xsltproc zip zlib1g-dev g++-multilib gcc-multilib lib32ncurses5-dev lib32readline-gplv2-dev lib32z1-dev maven
{% endhighlight %}

Also see [http://source.android.com/source/initializing.html](http://source.android.com/source/initializing.html) which lists needed packages.

### Create the directories

To create them:

{% highlight bash %}
$ mkdir -p ~/bin
$ mkdir -p ~/android/system
{% endhighlight %}

### Install the repo command

Enter the following to download the "repo" binary and make it executable (runnable):

{% highlight bash %}
$ curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
$ chmod a+x ~/bin/repo
{% endhighlight %}

Put the ~/bin directory in your path of execution

In recent versions of Ubuntu, ~/bin should already be in your PATH. You can check this by opening ~/.profile with a text editor and verifying the following code exists (add it if it is missing):

{% highlight bash %}
# set PATH so it includes user's private bin if it exists
if [ -d "$HOME/bin" ] ; then
    PATH="$HOME/bin:$PATH"
fi
{% endhighlight %}

### Initialize the OwnROM source repository

Enter the following to initialize the repository:

{% highlight bash %}
$ cd ~/android/system/
$ repo init -u git://github.com/OwnROM/android -b own-mm
{% endhighlight %}

### Download the source code

To start the download of all the source code to your computer:

{% highlight bash %}
$ repo sync
{% endhighlight %}

The OwnROM manifests include a sensible default configuration for repo, which we strongly suggest you use (i.e. don't add any options to sync). For reference, our default values are -j 4 and -c. The -j 4 part means that there will be four simultaneous threads/connections. If you experience problems syncing, you can lower this to -j 3 or -j 2. -c will ask repo to pull in only the current branch, instead of the entire CM history.

Prepare to wait a long time while the source code downloads.

### Prepare the device-specific code

After the source downloads, ensure you are in the root of the source code (cd ~/android/system), then type:

{% highlight bash %}
$ source build/envsetup.sh
$ breakfast DEVICECODENAME
{% endhighlight %}

This will download the device specific configuration and kernel source for your device. An alternative to using the breakfast command is to build your own local manifest. To do this, you will need to locate your device on CyanogenMod's GitHub and list all of the repositories defined in cm.dependencies in your local manifest.

### Extract proprietary blobs

Now ensure that your Android Device is connected to your computer via the USB cable and that you are in the ~/android/system/device/MANUFACTUER/CODENAME directory. Then run the extract-files.sh script:

{% highlight bash %}
$ ./extract-files.sh
{% endhighlight %}

You should see the proprietary files (aka “blobs”) get pulled from the device and moved to the ~/android/system/vendor/MANUFACTUER directory. If you see errors about adb being unable to pull the files, adb may not be in the path of execution. If this is the case, see the adb page for suggestions for dealing with "command not found" errors.

Note: Your device should already be running a build of CyanogenMod for the branch you wish to build for the extract-files.sh script to function properly.

Note: It’s important that these proprietary files are extracted to the ~/android/system/vendor/MANUFACTUER directory by using the extract-files.sh script. Makefiles are generated at the same time to make sure the blobs are eventually copied to the device. Without these blobs, OwnROM may build without error, but you’ll be missing important functionality, such as graphics libraries that enable you to see anything!

### Turn on caching to speed up build

You can speed up subsequent builds by adding

{% highlight bash %}
export USE_CCACHE=1
{% endhighlight %}

to your ~/.bashrc file (what's a .bashrc file?). Then, specify the amount of disk space to dedicate to ccache by typing this from the top of your Android tree:

{% highlight bash %}
prebuilts/misc/linux-x86/ccache/ccache -M 50G
{% endhighlight %}

where 50G corresponds to 50GB of cache. This only needs to be run once and the setting will be remembered. Anywhere in the range of 25GB to 100GB will result in very noticeably increased build speeds (for instance, a typical 1hr build time can be reduced to 20min). If you're only building for one device, 25GB-50GB is fine. If you plan to build for several devices that do not share the same kernel source, aim for 75GB-100GB. This space will be permanently occupied on your drive, so take this into consideration. See more information about ccache on Google's android build environment initialization page.

### Start the build

Time to start building! So now type:

{% highlight bash %}
$ croot
$ brunch DEVICENAME
{% endhighlight %}

The build should begin.

### If the build breaks...

If you experience this not-enough-memory-related error...

{% highlight bash %}
ERROR: signapk.jar failed: return code 1make: *** [out/target/product/DEVICENAME/ownrom_DEVICENAME-ota-eng.root.zip] Error 1
{% endhighlight %}

...you may want to make the following change to ~/android/system/build/tools/releasetools/common.py:

Search for instances of -Xmx2048m (it should appear either under OPTIONS.java_args or near usage of signapk.jar), and replace it with -Xmx1024m or -Xmx512m.

Then start the build again (with brunch).

If you see a message about things suddenly being “killed” for no reason, your (virtual) machine may have run out of memory or storage space. Assign it more resources and try again.

### Install the build

Assuming the build completed without error (it will be obvious when it finishes), type:

{% highlight bash %}
$ cd $OUT
{% endhighlight %}

in the same terminal window that you did the build. Here you will find all the files that were created. The stuff that will go in /system is in a folder called system. The stuff that will become your ramdisk is in a folder called root. And your kernel is called... kernel.

But that is all just background info. The file we are interested in is ownrom-12.1-20160417-UNOFFICIAL-DEVICENAME.zip, which is the OwnROM installation package.

### Install OwnROM

Back to the $OUT directory on your computer-- you should see a file that looks something like:

{% highlight bash %}
"ownrom-12.1-20160417-UNOFFICIAL-DEVICENAME.zip"
{% endhighlight %}

Note: The above file name may vary depending on the version of OwnROM you are building. Your build may not include a version number or may identify itself as a "KANG" rather than UNOFFICIAL version. Regardless, the file name will end in .zip and should be titled similarly to official builds.

Now you can flash the ownrom...zip file above as usual via recovery mode. Before doing so, now is a good time to make a backup of whatever installation is currently running on the device in case something goes wrong with the flash attempt. 

### To get assistance

If you have any problems:

Head over to our [G+ community](http://bit.ly/1Fye9Gd) or [contact us](/contribute.html).
