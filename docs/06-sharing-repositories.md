# Sharing Your Repository

Git is a distributed VCS, which means all project collaborators have a copy of the repository on their machine!

Centralizing a repository on a server that will be authoritative is not mandatory. It all depends on your work organization.

Note that as a consequence, the central repository is not a critical point of the system. In particular, a backup is not essential (but remains good practice!) since each collaborator has a copy.

**Warning!** You must not modify the history of modifications that have been shared. For example, don't do git reset. Your collaborators may have started making modifications from a commit you deleted. If you want to undo a commit, prefer git revert.

## Sharing by Simple Copy

A simple way to share your repository is to copy it to a medium (USB key, for example) and transmit it.

By placing yourself in the root directory of your working directory, copy your repository:
```bash
$ cd ..
$ cp -Rf git-tuto git-tuto-cp
$ cd git-tuto-cp
```

Notice with git log that you've just created a clone, which you can now compress as tar.gz and send by email, for example!

You can also do the same thing with the git clone command:
```bash
$ cd ..
$ git clone git-tuto git-tuto-clone
```

Enter the git-tuto-clone directory to see that you get the same result.

## Creating a Bare Repository

When you want to share your repository on a server, it's recommended to create a "bare" repository. A bare repository doesn't contain a working directory, only the Git history.

To create a bare repository:
```bash
$ cd ..
$ git clone --bare git-tuto git-tuto.git
```

By convention, bare repositories have the .git extension.

## Sharing via SSH

git clone can be used with various network protocols (ftp, http, ssh...).

To test 'ssh', let's start with a local test (replace '<uid>' with your login name):
```bash
$ git clone ssh://<uid>@localhost/full/path/to/git-tuto git-tuto-ssh
```

Check the git-tuto-ssh directory.

**Note**: you could have done a simple scp but we'll see later that it's not completely equivalent...

## Remote Repositories

When you clone a repository, Git automatically creates a reference to the original repository called "origin".

You can see the list of remote repositories with:
```bash
$ git remote -v
origin  /full/path/to/git-tuto (fetch)
origin  /full/path/to/git-tuto (push)
```

You can add other remote repositories:
```bash
$ git remote add <name> <url>
```

And remove them:
```bash
$ git remote remove <name>
```

## Fetching and Pulling Changes

When working with remote repositories, you need to synchronize your local repository with the remote one.

**git fetch** downloads changes from the remote repository but doesn't merge them:
```bash
$ git fetch origin
```

**git pull** downloads changes and merges them into your current branch:
```bash
$ git pull origin master
```

git pull is equivalent to:
```bash
$ git fetch origin
$ git merge origin/master
```

## Pushing Changes

To send your commits to a remote repository:
```bash
$ git push origin master
```

This command sends the commits from your local master branch to the master branch of the origin remote.

If the remote branch has been modified since your last pull, Git will refuse the push. You'll need to pull the changes first, resolve any conflicts, then push again.

---

**Previous:** [← Going Back: Reset and Revert](05-reset-and-revert.md) | **Next:** [Rebase: An Alternative to Merge →](07-rebase.md)

