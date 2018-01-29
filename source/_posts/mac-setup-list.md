---
title: Mac Setup List
date: 2018-01-25 21:51:25
tags:
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
```bash
brew install git
```

## NPM (Nodejs)
Install NPM just install [Nodejs](https://nodejs.org/en/).

## Hexo
```bash
npm install hexo -g
```

## VSCode
[VSCode](https://code.visualstudio.com/)