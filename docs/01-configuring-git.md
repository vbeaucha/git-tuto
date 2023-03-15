# Configuring Git

## Initialize a Git Repository

To initialize a local git repository, nothing could be simpler:
```bash
$ git init gitrepo
$ cd gitrepo
```

## Identify Your Commits

When you make a commit on git, we need to know who you are!
You can identify yourself like this:
```bash
$ git config --global user.name "your name"
$ git config --global user.email email@email.com
```

## Customize Your Git

Git allows a wide range of customization. To start, I invite you to modify your editor and define a push strategy that will be useful to avoid certain warnings later:
```bash
$ git config --global core.editor vim
$ git config --global push.default simple
```

## Add a Prompt for Your Git Repos

Download this [script](https://raw.githubusercontent.com/git/git/master/contrib/completion/git-prompt.sh) and install it in your local directory, then add these lines to your *~/.bashrc* file:

```sh
. ~/.git-prompt.sh
export GIT_PS1_SHOWDIRTYSTATE=1
export PS1='\[\e[1;32m\u@\h\]\e[m:\]\e[1;34m\w$(__git_ps1 " (%s)")\]\e[m\$\] \]'
```

Reload your bashrc:
```bash
source ~/.bashrc
```

---

**Next:** [My Very First Commit →](02-first-commit.md)

