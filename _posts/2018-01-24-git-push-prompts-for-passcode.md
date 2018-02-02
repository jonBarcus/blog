---
layout: post
comments: true
title:  "Dealing with a password prompt when executing 'git push' in Terminal"
date:   2018-01-24 14:00:00 -0400
categories: git github bash terminal passcode
---

# Dealing with a password prompt when executing 'git push' in Terminal
So, a few weeks ago I completely blew away my hard drive (and my development environment along with it) and installed a fresh OSX.

I should have documented the whole process, I definitely had a bunch of issues getting my .bash_profile set and everything in my development environment back up-and-running.

Anyway, decided to tackle this!

I had thought I set everything up correctly.  Generated the SSH key, uploaded it to Github, etc.

I cloned the repo with SSH, but found that I kept getting prompted for my password every time I ran :
```bash
git push origin master
```

When I googled what was happening, the general consensus was that I had cloned my github repo with *https* instead of *SSH* and the recommendation was to store a password in the OS X Keychain.  I was loathe to do so, so I didn't.

After another week of it I decided to look in to it again.  I decided to double-check how the heck I cloned the repo:
```bash
git remote -v
```

I wasn't crazy!  It returned the
```bash
git@github.com:USERNAME/REPOSITORY.git
```
that it was supposed to and _not_ the 
```bash
https://github.com/USERNAME/REPOSITORY.git
```
that I was worried about.

With this in mind, I looked again about storing a password.  What I found/was reminded about, is that SSH shouldn't be using a password, it uses a key!  Duh.

So, I started to look in to how I could check and make sure that I had set up my SSH correctly in bash.

So, I found what appears to be a test to make sure you're authenticating correctly with github:
```bash
ssh -T git@github.com
```
It prompted me for my passphrase for my key at its local location:
```bash
'/users/username/.ssh/id_rsa'
```
I entered the passphrase and it confirmed I was successfully authenticated!

Next, I decided to add/re-add my SSH private key to the ssh-agent:
```bash
ssh-add -K ~/.ssh/id_rsa
```

The *-K* is important because it's storing the passcode in OSX's Keychain.  I didn't realize I had to do this at first, and I wanted to avoid it but relented.

When I next ran
```bash
git push origin master
```
it worked!

There ya go!

I hope this is helpful to you, should you come across this!