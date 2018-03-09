---
layout: post
comments: true
title:  "Rebuilding My Development Environment - Part 2"
date:   2018-03-09 14:00:00 -0400
categories: git github bash terminal osx
---

# Rebuilding my development environment - Part 2
### Let's Continue and Credit
So, In [Part 1](https://jonbarcus.github.io/git/github/bash/terminal/ruby/gem/homebrew/osx/2018/02/27/rebuilding-my-dev-envr-part1.html) we got back up-and-running.  That's pretty nice.  Now we're going to tackle my Bash profile.  I'm thinking we'll break it down in to sections.

To give credit where credit is due, most of this Bash profile was written by Philip Lamplugh and updated by PJ Hughes in their capacity as Instructors with [General Assembly](https://generalassemb.ly/) (of which I'm a 2014 Alum).  I didn't know PJ, but Phil was my lead instructor and he was awesome.  Their resources are located at the bottom of this post.

### Bash Housekeeping
Let's take a look at my Bash profile:  `open -e ~/.bash_profile`
Right now, my bash profile consists of:
```bash
eval "$(rbenv init -)"
eval "$(ssh-agent -s)"
```

Before I got started here, I added this to my bash profile, saved it, closed and relaunched terminal:
```bash
alias subl='open -a "Sublime Text"'
export EDITOR="subl -w"
```
This just makes working with the bash profile a little easier.

There are some useful aliases that we were provided with and I like to make use of these:

```bash
# Lists folders and files like normal, but adds a slash for directories
alias ls="ls -F"
# Long list will include hidden files too
alias ll="ls -la"
# rm will now prompt before removing
alias rm="rm -i"
# we can get some color in terminal
export CLICOLOR=1
# This is where they're coming from:  http://geoff.greer.fm/lscolors/
# Here you can play around with what color is used for folders and files
export LSCOLORS=chexcxdxbxegedabagacad # PJ: turned off
# If you change your bash profile you can reload without leaving terminal
alias reload=clear; source ~/.bash_profile
# Here are some things to make TAB a friend in Terminal
# Not sure if all are necessary, but it works as of OSX 10.13.3
bind 'set completion-ignore-case on'
bind 'set show-all-if-ambiguous on'
bind 'TAB: menu-complete'
```

Basically, all I can think of that's left is getting PostgreSQL working.  Will tackle that another time!

=====================
Resources
=====================
http://cli.learncodethehardway.org/bash_cheat_sheet.pdf
http://ss64.com/bash/syntax-prompt.html
https://dougbarton.us/Bash/Bash-prompts.html
http://sage.ucsc.edu/xtal/iterm_tab_customization.html