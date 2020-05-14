# dotfiles

This repository contains dotfiles and stuff for my machine. You'll use [yadm](https://thelocehiliosan.github.io/yadm/) to install almost everything.

Before we get started, let's create SSH keys, add them to GitHub.

## Create SSH keys

First, use some command line magic to create your SSH keys. You'll need these for a few things later.

Linux
```console
$ sudo apt update
$ sudo apt install ssh
$ ssh-keygen -t rsa -b 4096 -C "david@dwilliamshome.com"
$ eval $(ssh-agent -s)
$ ssh-add ~/.ssh/id_rsa
```
Mac
```console
$ ssh-keygen -t rsa -b 4096 -C "david@dwilliamshome.com"
$ eval $(ssh-agent -s)
$ ssh-add ~/.ssh/id_rsa
```

## Add your keys to GitHub

Next, add your keys to GitHub so you can access various GitHub repositories, including the oh-my-zsh one as well as your private repos later.

First, get your public key. Copy this value to the clipboard (using `ctrl+shift+c if you're on WSL`).

```console
$ cat ~/.ssh/id_rsa.pub
```

Then, go to [github.com/settings/ssh/new](https://github.com/settings/ssh/new), name the key (for example: "My new machine!") in the Title box, and paste the public key value into the "Key" box

## Install Yadm

Now that you've got all your keys set up, let's get our `apt` package manager ready, and install [yadm](https://thelocehiliosan.github.io/yadm/):

Linux
```console
$ sudo apt install yadm
```
Mac
```console
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
$ brew install yadm
```


## Install dotfiles

Now that yadm is installed, we can go install these dotfiles. They should do everything else for us!

Linux and Mac
```console
yadm clone https://github.com/dwilliamhouston/dotfiles.git
```

>The dotfiles have a bootstrap script that switches on `uname` to execute setup for Debian/Ubuntu or OS X.
