---
layout: post
title: How to Install some stuff on Xubuntu 16.04 (Xenial Xerus)
description: I just recently upgraded (which I was holding off for a long time) my OS to Xubuntu 16.04 from 14.04. This is a post detailing how I install/reinstall most of the common stuff I use so that I won't forget them in the future.
tags:
  - Xubuntu
  - '16.04'
comments: true
pinned: false
---

I recently upgraded my machine to Xubuntu 16.04 after almost 3 years of using Xubuntu 14.04. This is always an exciting (or frustrating) time for me as it allows me to reinstall most of my stuff and keep my machine updated.

This post will just detail how I install/reinstall on Xubuntu 16.04 the common software and tools I use everyday as well as the not-so-common ones that I keep for special ocassions so that I don't forget them in the future.


### Set Proxy for the Shell (bash)
I usually set my proxy in the bash config file (```.bashrc```) if I need to access the web through the shell.
```shell
cd ~
nano .bashrc
```

Add this line to ```.bashrc``` file.
```shell
#PROXY SETTINGS
export {http,https,ftp}_proxy=<proxy-username>:<proxy-password>@<proxy-host>:<proxy-port>
```

Restart the shell.

Another method is to create a ```95proxies``` file inside ```/etc/apt/apt.conf.d/```.
```shell
sudo nano /etc/apt/apt.conf.d/95proxies
```

Then add the following lines:
```shell
Acquire::http::proxy "<proxy-username>:<proxy-password>@<proxy-host>:<proxy-port>";
Acquire::https::proxy "<proxy-username>:<proxy-password>@<proxy-host>:<proxy-port>";
Acquire::ftp::proxy "<proxy-username>:<proxy-password>@<proxy-host>:<proxy-port>";
```

### Atom
The first thing I reinstalled was [Atom](https://atom.io) because every developer/programmer needs a good text-editor. A few years ago, this spot was reserved for Sublime Text (still one of the best text editors EVER) but recently I've found myself liking and using Atom more. Atom gets plus points for being open-source -- something that Sublime is not (probably one of the few bad points with Sublime for me).

If you're using 'buntu, installing Atom is easy. Just download the [.deb](https://atom.io/download/deb) then install it using:
```shell
sudo dpkg --install atom-amd64.deb
```

### LibreOffice
LibreOffice is my go-to Office Suite. Xubuntu comes packaged with LibreOffice Writer, Calc, and Math but not the entire Suite. What I usually do is remove the built-in LibreOffice package and replace it with one from the [LibreOffice Fresh PPA](https://launchpad.net/~libreoffice/+archive/ubuntu/ppa).

First, you remove all the built-in LibreOffice packages.
```shell
sudo apt remove libreoffice-*
```

Then add the PPA to your software sources.
```shell
sudo add-apt-repository ppa:libreoffice/ppa
sudo apt update
```

Then install LibreOffice.
```shell
sudo apt install libreoffice
```

If the above method doesn't work, we can try using snaps.
```shell
sudo apt install snapd
```

```shell
sudo snap install libreoffice
```

### PDF Chain
PDF Chain is a GUI for the PDF Toolkit (PDFtk). For those times I need to combine or split pdf files.
```shell
sudo add-apt-repository ppa:pdfchain-team/ppa
sudo apt update
sudo apt install pdfchain
```

### pip
Because Python devs still need pip.
```shell
sudo apt install python-pip python3-pip
```

### virtualenvwrapper
Same as above. virtualenvwrapper makes Python development easier.
```shell
sudo pip install virtualenvwrapper
```

Edit ```.bashrc``` by adding
```shell
export WORKON_HOME=$HOME/.virtualenvs
export PROJECT_HOME=$HOME/Projects
source /usr/local/bin/virtualenvwrapper.sh
```

### GRASS GIS
Add the UbuntuGIS Unstable PPA to your software sources
```shell
sudo add-apt-repository ppa:ubuntugis/ubuntugis-unstable
```

or you can add the following lines to your ```/etc/apt/sources.list```
```shell
deb http://ppa.launchpad.net/ubuntugis/ubuntugis-unstable/ubuntu xenial main
deb-src http://ppa.launchpad.net/ubuntugis/ubuntugis-unstable/ubuntu xenial main
```

Update your software sources and install GRASS.
```shell
sudo apt update
sudo apt install grass
```

### rvm (Ruby Version Manager)
```shell
curl -sSL https://get.rvm.io | bash -s stable --ruby
```

Add the following lines to ```.bashrc``` if you encounter the 'rvm is not a function' message
```shell
source $HOME/.rvm/scripts/rvm
```
*A Note with RVM: The PATH export lines of RVM should be the last line in your .profile or .bashrc files*

### Steam
Download the [Steam installer (.deb)](http://store.steampowered.com/about/) and run it.

When you first run Steam, it will ask you to download certain packages. Install these packages.

Update Steam and start playing.

*If you're behind a firewall, you won't be able to play but you'll be able to update steam through the command line.*
```shell
steam update
```