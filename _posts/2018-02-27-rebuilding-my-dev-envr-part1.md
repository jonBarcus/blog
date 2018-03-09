---
layout: post
comments: true
title:  "Rebuilding My Development Environment - Part 1"
date:   2018-02-27 14:00:00 -0400
categories: git github bash terminal ruby gem homebrew osx
---

# Rebuilding my development environment - Part 1
### Again? Seriosuly?
So, apparently my old SSD decided to go kaput.  Fortunately, I had the foresight to e-mail this to me _just in case_ it did.  Phew.  Hold on to your butts.  One thing that I've been weighing while my computer has been out of comission, is whether or not I should start with the Bash profile.  I don't think I will and we'll just go with the generic stuff that everyone can make use of.  I'll share some of my Bash profile settings in another part.

### Original Start
As fate would have it, my partition got messed up and I had to reformat my disk and reinstall the OS about two months after it wiped my SSD, re-installed the OS, and set up my dev environment.

I had lamented my not writing about the process a couple months ago, so, now I get a second chance!  Though I had a pretty cool "How to get Disqus working with your GitHub-hosted Jekyll blog" post in the works that's lost to eternity.  C'est dommage.

Part 1 is going to cover up to the point where I can push this up to my blog.

### Optional Section - Applications I love and always install

- [Spectacle](https://www.spectacleapp.com/) - a wonderful application that allows you to quickly reposition windows around your display(s).  I can't live without this
- [Dash](https://kapeli.com/dash) - a great application that will store documentation offline for you (handy when your internet connection is crappy or non-existent)
- [Alfred](https://www.alfredapp.com/) - as-is, this app is only useful if you make it useful.  It can become quite the powerful tool if you get the Powerpack and set up some Workflows
- [Sublime Text](https://www.sublimetext.com/3) - this is my preferred text editor.  I just like it.  Everyone has their preferences and I'm not dogmatic about this.  Use what works best for you!

### The Fun Stuff Begins - Homebrew

Alright.  I love [Homebrew](https://brew.sh/).  This is a wonderful package manager and it's how I manage my installs in Terminal.  It's also the first thing I install.

So, heading to Terminal, I run:
```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
This will run normal stuff but, if you don't have it installed already, is going to prompt you for your password to install **The Xcode Command Line Tools**.  Go for it.

### The Fun Stuff Continues - Git

What's next?  Why don't we install Git?

Now that we have Homebrew installed, installing Git is as easy as:  `brew install git`

Once that's installed, if you run `git --version` in Terminal, you'll likely see that you're still running Apple's Git.

Run `hash -r` in Terminal and that will clear some cached executable paths and when you run `git --version` again you should see the version of git that you installed!

### What's Next? Ruby!

Ruby is what I know right now, so that's my focus here.  Again, not being dogmatic here, but I prefer [**rbenv**](https://github.com/rbenv/rbenv) instead of **RVM** .  There's a nice and simple comparision [here](https://github.com/rbenv/rbenv/wiki/Why-rbenv%3F) if you want to take a look.  If not, we'll get to installing rbenv and Ruby.

Inside Terminal, let's run `brew install rbenv`

So now that we've got rbenv installed, let's install the latest Ruby.

We can see all the available versions by running `rbenv install -l` (that's a little L).  As of this post, the latest is 2.5.0.

I'll run rbenv install 2.5.0 by running `rbenv install 2.5.0` .

After that's done, we'll run `ruby -v` and find that we're still running the Ruby version that comes with OS X.

The way I resolved this was to add `eval "$(rbenv init -)"` to the my `.bash_profile` and then restart terminal.

Now, if you run `rbenv global 2.5.0` and check `ruby -v` you should see that the Ruby version it returns is correct.

### GitHub

Alright.  We're closer to getting this post up on my blog.

Let's make sure our computer can play nice with GitHub.  We'll need an SSH key first.  GitHub has some great instructions on setting this up [here](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).

If you don't want to go there, here's the gist (no GitHub-pun intended):

1. In Terminal, run this: 
```bash
ssh-keygen -t rsa -b 4096 -C "your_github_email@emaildomain.com"
```
1. It'll then do some stuff, and you can hit _enter_ when prompted for a location if the default location is fine
1. Then you'll be prompted for a passcode and to confirm it, go for it
So now you've got an SSH key, awesome.  So we need to add the key to ssh-agent
1. Start the agent by running `eval "$(ssh-agent -s)"`
1. Then take look at [Step 2 in Adding your SSH key to the ssh-agent section](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/) and see if that's something that applies to you
1. Then, you'll add the key the agent:  `ssh-add -K ~/.ssh/id_rsa`
Now, you can [add the key to your Github account](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/) and you should be good to go!

You might want to [test your SSH connection to GitHub](https://help.github.com/articles/testing-your-ssh-connection/).

### Cloning Your Repo (if you're here because you were in the same situation or similar situation)

Okay, so now it's time to get that repo back on the local machine.  If you've got Git working and everything is all set from the GitHub section, this should be pretty easy.
1. In Terminal, go to the folder where you'd like the GitHub repo cloned to (it'll create a new folder with the repo in it)
1. On GitHub, open the repo and click on the *Clone or download* button and if you see the _Clone with SSH_ title, copy that script section
1. In Terminal, enter `git clone` and paste what you copied from the GitHub repo and run it
You should be all set!  Make sure things copied correctly.

You'll want to check the remotes `git remote -v` and make sure it's got the correct *fetch* and *push* options.
If it does you're all set!

In Part 2 I'll start on my Bash profile.  Hope this was helpful!