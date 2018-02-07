---
title: Mac Setup List
date: 2018-01-25 21:51:25
tags: [Mac]
---
The following list is hint for setup Mac. Continuing adding.

<!-- more -->
## iTerm2
We are going to be spending a lot of time on command-line. So it is a good idea to use a better tool. iTerm2 is the choice.

Download : [iTerm2](http://www.iterm2.com)
Install  : Drag and drop iTerm app into Appllactions folder

We like to use colorful command-line. Download from [iTerm2 Color Schemes](https://github.com/mbadolato/iTerm2-Color-Schemes/tree/master/schemes).I'd like to clone all the schemes, and choice one the like best.

To enable color in iTerm2, add the following lines in `.bash_profile` under `~`.
```
# Set CLICOLOR if you want Ansi Colors in iTerm2
export CLICOLOR=1

# Set colors to match iTerm2 Terminal Colors
export TERM=xterm-256color
```

## Homebrew
```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

## Git
I tred a lot of time to download Git from [Git-SCM](https://git-scm.com/downloads), but never successed. So I changed to use `homebrew` to install git instead.
```bash
brew install git
```

## NPM (Nodejs)
NPM cannot install itself, it can be installed by [Nodejs](https://nodejs.org/en/).

## Hexo
I use [Hexo](https://hexo.io/) to setup my [Blog](http://gu-yuan.top), and using GitHub to store my blog.
```bash
npm install hexo -g
```
For I am using Git for this blog, so need to use hexo git deploy toolkit.
```bash
npm install hexo-deployer-git --save
```
and then setup `_config.yml` in *deploy* block
```
deploy:
  type: git
  repo: https://github.com/guyuanershi/guyuanershi.github.io.git
  branch: master
```

## Fira Code
I'd like to use `Fira Code`, it gives some nice symbol, such as >=,
Download from [here](https://github.com/tonsky/FiraCode)

* Mac:  
Open `Font Book` and select the download `Fira Code` (.otf, .ttf)
* Win:  
Double click font file to install

## VSCode
There are a lot editor, but for me `Vim` and `VScode` is enough.
Download from here: [VSCode](https://code.visualstudio.com/)

>Set Fira Code in VSCode ([link](https://github.com/tonsky/FiraCode/wiki/VS-Code-Instructions))
```
    "editor.fontFamily": "Fira Code",
    "editor.fontLigatures": true
```