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

If you have Two-Factor Authentication enbled on Github do the following:

You'll need to store your personal access token in your netrc as two factor authentication prevents your username/password from being used on the command line. To fix this follow these steps:

Mac or Linux
1. Go to https://github.com/settings/tokens/new
2. Put in the name "Command Line" for the Token Description
3. For the scopes, enable all the top scopes (e.g., click the checkboxes: repo, admin:org, etc, etc...), then click Generate Token.  You'll need to copy the token it generates, it's in a green window with a clipboard icon next to it.
4. Open a terminal window (Go to the Applications folder, Utilities folder, run Terminal application)
5. touch ~/.netrc; open -a "TextEdit" ~/.netrc (or the CLI editor of your choice)

Enter:
  machine github.com
  login [your_github_login_name]
  password [the_token_copied_from_above]
  machine api.github.com
  login [your_github_login_name]
  password [the_token_copied_from_above]
  Make sure to replace [your_github_login_name] with your github login, NOT your email address. Make sure to replace [the_token_copied_from_above] with the token.

6. Save these changes, and close the editor.
7. Run chmod 600 ~/.netrc in the terminal

To test this run curl -n https://api.github.com/user, you should see your user information in a JSON response. You can also test this by trying to clone out a private https repo, it should no longer ask for your password.

## Install Yadm

Now that you've got all your keys set up, let's get 'yadm' setup.

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
$ yadm clone https://github.com/dwilliamhouston/dotfiles.git
```

The dotfiles have a bootstrap script that switches on `uname` to execute setup for Debian/Ubuntu or OS X.
