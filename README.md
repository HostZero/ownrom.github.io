# OwnROM-Website:

A website for OwnDroid and our ROM, OwnROM

http://owndroid.nl  (MAIN)

https://ownrom.github.io (BETA)

[![Issue Stats](http://issuestats.com/github/OwnROM/ownrom.github.io/badge/pr)](http://issuestats.com/github/OwnROM/ownrom.github.io)

[![Issue Stats](http://issuestats.com/github/OwnROM/ownrom.github.io/badge/issue)](http://issuestats.com/github/OwnROM/ownrom.github.io)

##Screenshot (As of April 26, 2015):

![Alt text](https://github.com/OwnROM/ownrom.github.io/blob/master/assets/images/Screenshot.png)

## Tech:

Our website uses a number of projects/software to work:

* [Bootstrap] - Bootstrap is the most popular HTML, CSS, and JS framework for developing responsive, mobile first projects on the web
* [Markdown] -Markdown is a text-to-HTML conversion tool for web writers

##Instructions:

When coping code do not copy the $ symbols or any line with # at the front

## Downloading:

```sh
#Make a directory to hold the source
$ mkdir ownrom-website
#Go to the directory
$ cd ownrom-website
#Get the source code
$ git clone https://github.com/OwnROM/ownrom.github.io
```

Or download the repo as a zip file to the right -->

Then extracting it to a new directory called ownrom-website

## Development:

Want to contribute? Great!

You may edit any file in this respitory including the readme or add files if needed if you think this will improve the site or projet

#### Needed programs:

##### Text editor:

If you need a text editor we would recommend ethier [Brackets], [Atom], [Sublime] or [Geany]

If you need a more heavyweight text editor with many features, extensions or themes use ethier [Brackets], [Atom] or [Sublime]

http://brackets.io/

http://atom.io

http://www.sublimetext.com/

If you however want a more lightweight text editor that still has a good amount of feautres try [Geany]

http://www.geany.org/

##### Framework:

Our website uses the [Bootstrap] framework. To see what you can add/edit using this see the following link

http://getbootstrap.com/

This dosent need to be installed

##### Editing multiple files:

First download the source code as explained above in the downloading section

Then initialize the local directory as a Git repository
```sh
#Go to the source directory
$ cd ownrom-website
#Initalize this as a git respitory (For pushing changes)
$ git init
```

Add the URL for the remote repository where your local repostory will be pushed.
```sh
$ git remote add origin https://github.com/OwnROM/ownrom.github.io.git
```

Then pull in any new changes
```sh
$ git pull origin master
```

You may now add/edit any files in your local respitory

After editing or adding files add the files to your local repository
```sh
#Adds all changed files to get ready for a commit
$ git add .
```

Then commit the files that you've staged in your local repository (Where commit text could be anything you want)
```sh
$ git commit -m 'commit text'
```

Finally push the changes in your local repository to GitHub
```sh
$ git push origin master
```

(If you get a error this usally means there has been changes in the respitory. Just use the ```$ git pull origin master``` command as shown above then push your changes)

##### Editing single files:

There is no need to do the steps as explained above but that would work aswell.

To edit just one file click on the file in the respitory that you want to edit, hit the edit button (the pencil), edit the file as you like and subbmit it via a commit.

##### Suggesting ideas:

To suggest ideas for this website or fixes to be made just submit a new issue and we will get right on it.

#####What gets added?

If we think your additions or changes will improve this website we will add them right away. If for some reason that we think they don't we will not add them to this project.

##Questions or need help?

Chat with The OwnDroid team and other users of this project here

[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/OwnROM/android?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)




[Bower]:http://bower.io/
[Geany]:http://www.geany.org/
[FileZilla]:https://filezilla-project.org/
[Github]:https://github.com/
[Git]:http://git-scm.com/
[Brackets]:http://brackets.io/
[Markdown]:http://daringfireball.net/projects/markdown/
[Atom]:http://atom.io
[Bootstrap]:http://getbootstrap.com/
[Sublime]:http://www.sublimetext.com/
