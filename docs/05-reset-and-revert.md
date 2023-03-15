# Going Back and Maintaining a Linear History

## Deleting a Commit

There's a command that allows you to go back and delete a commit:

```bash
$ git reset HEAD^
```

There are 3 reset options in git:
1. --soft: The commit is deleted but the modifications are stored in the index awaiting validation
2. --mixed: default mode, modifications are stored in the working directory
3. --hard: Modifications are deleted (use with caution)

**Reminder**: HEAD^ references the commit preceding HEAD.

git status shows that the files are still present in your workspace but are now unstaged (with the default --mixed option).

This is the default behavior of git reset.

### Warning about reset --hard!

The --hard mode of git reset goes further in going back, combining git reset with a synchronization of the working directory (like git checkout does). However, there's an essential difference with git checkout: the synchronization is forced, all modifications on tracked files are deleted (git checkout cannot be executed if there are uncommitted modifications).

This mode should be used with full knowledge: **this is one of the rare cases where you can lose data irreversibly!**

### Deleting Multiple Commits

git reset also allows you to delete multiple commits. There are several possibilities:

To delete the last 'n' commits, simply suffix the '^' character n times to the 'HEAD' reference. For example, to delete the last 5 commits:
```bash
$ git reset HEAD^^^^^
```

Compressed notation:
```bash
$ git reset HEAD~5
```

To delete all commits after the commit with id 'f1fa39c':
```bash
$ git reset f1fa39c
```

To delete the commit with id 'f1fa39c' and those that follow it (and thus go back before commit 'f1fa39c'):
```bash
$ git reset f1fa39c^
```

**Note**: This notation can also be used with other commands, such as git show, git checkout, etc.

### Key Takeaways

The git checkout and git reset commands might seem equivalent at first glance since they can produce the same apparent result on your working directory.

However, they are fundamentally different in their purpose:

- **git checkout** acts on the working directory: the working directory is restored to the state recorded in the selected commit. To do this, Git can modify your files, and add or remove others (Git doesn't touch untracked files, fortunately). This command doesn't modify the history recorded in the repository (the master reference isn't modified). So we can return to the latest version with git checkout master.

- **git reset** acts on the history: the head reference (master) is moved, which removes commits from the history.
  - With the **--soft** option: the working directory content isn't modified: differences between the working directory and the new head commit are considered as modifications placed in the index, but not yet validated. Result: we go back to just after we did git add but before doing the commit.
  - In its basic version (**--mixed** option by default): the working directory content still isn't modified: differences between the working directory and the new head commit are considered as not indexed. Result: we go back one step earlier, just after we modified the files but before doing git add.
  - In its **--hard** version: the working directory is also synchronized with the new head commit. Result: we go back one more step, before we modified the files.

This difference makes their usage frequency very different:

- git checkout <commit_id> is a command used very regularly when working with branches, as you'll see soon. This is the main use of this command.
- git checkout <a_file> is occasionally used to delete modifications just added to a file.
- git reset is rarely used. It only serves, a priori, when deciding to abandon work in progress and go back.

**WARNING**: Like any command modifying history, git reset should not be used on histories shared with other contributors.

## Undoing a Commit with git revert

Sometimes, we want to undo the modifications of a commit, but we can't use git reset because the history has already been shared with others.

In this case, git revert is the solution! This command creates a new commit that undoes the modifications of a previous commit, without touching the existing history.

Let's create a new file to test this:
```bash
$ echo "Important line" > important.txt
$ git add important.txt
$ git commit -m "Added an important file"
```

Now, suppose this commit was a mistake. Let's use git revert:
```bash
$ git revert HEAD
```

Your editor opens with a default commit message. Validate it, Git creates a new commit that undoes the modifications of the previous commit.

```bash
$ git lg
* a1b2c3d (HEAD -> master) Revert "Added an important file"
* d4e5f6g Added an important file
* fd5a68a Merge branch 'develop'
...
```

The important.txt file has been deleted, but the history clearly shows what happened!

**Note**: git revert can also be used to undo an older commit. In this case, conflicts can occur if other commits have modified the same files.

---

**Previous:** [← Branches and the HEAD Position](04-branches-and-head.md) | **Next:** [Sharing Your Repository →](06-sharing-repositories.md)

