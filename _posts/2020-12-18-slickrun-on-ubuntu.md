---
layout: post
title: SlickRun on Ubuntu
date: 2020-12-18 12:33
author: ayvazyan
comments: true
categories: [Productivity, Ubuntu, Tools]
---


*\* I'm using Ubuntu 20.04 as my main operating system for some time now. 
So I'd like to document some tips in my blog.*


I've been using [SlickRun](https://bayden.com/slickrun/) on Windows for years. It's just great. I can launch any program or website. For example to open work item #123, I just type `wi 123` and it will create a correct URL for me and open that work item in my browser.

The more generic example might be `google abc` command to search `abc` on the eb. It does so by adding `abc` to the url, so it's something like `https://www.google.com/search?q=abc`.

I needed a similar workflow for Ubuntu and here's my solution.
<!--more-->
## Configure gRun as SlickRun

1. I installed [**gRun**](https://launchpad.net/ubuntu/+source/grun/0.9.3-2) the program that allows to launch programs and scripts using the `apt install grun` command.
2. I configured the `Alt+Q` hotkey for **gRun** under **Settings -> Keyboard Shortcuts**. (by default **SlickRun** is using that one)
3. Then I created `.grun` folder in my home directory using the `mkdir ~/.grun` command.
4. In that folder I created the `~/.gurn/grun-enable` script that will allow to configure new URLs:
```
echo "xdg-open $1" > ~/.grun/$2
chmod +x ~/.grun/$2
```
5. Now we need to add `.grun` folder into the **PATH**, so that we can launch commands without specifying **/.grun** prefix. To do so add the text below to the very end of `~/.profile` and re-login.
```
if [ -d "$HOME/.grun/" ] ; then
    PATH="$HOME/.grun/:$PATH"
fi
```
6. That's it!

Now we can configure google search using the following command:
`grun-enable https://www.google.com/search?q=\$1 google`.

And use it by typing `google abc` in **gRun** or in terminal.

## VPN
Would like to connect to VPN via **gRun** or terminal? We've got you covered. Just put `nmcli con up id CONNECTION_NAME_HERE` into `~/.grun/vpn` and then mark it as executable via `chmod +x ~/.grun/vpn`. 
Or you can do that with one liner:

`echo "nmcli con up id CONNECTION_NAME_HERE" > ~/.grun/vpn && chmod +x ~/.grun/vpn`

## What's next?
So we've got an easy way to run virtually anything with `Alt+Q` (or any other you used to). 
For me that makes a real difference, now I feel at home :)

Hope you will like it to you, Dear Reader.