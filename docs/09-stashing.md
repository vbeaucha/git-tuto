# Stashing

## What is Stashing?

Stashing allows you to temporarily save your work in progress without creating a commit. It's very useful when you need to quickly change branches or fix an urgent bug while you're in the middle of work!

## Basic Stash Usage

Imagine you're working on a feature, but you need to fix an urgent bug on the master branch.

Modify the script.js file:
```bash
$ vim script.js
# Add a line: console.log("Work in progress...");
```

You don't want to commit this unfinished work. Use git stash:
```bash
$ git stash
Saved working directory and index state WIP on master: a1b2c3d Last commit message
HEAD is now at a1b2c3d Last commit message
```

Your modifications have been saved and your working directory is clean:
```bash
$ git status
On branch master
nothing to commit, working tree clean
```

You can now change branches, fix the bug, then return to your work!

## Listing Stashes

To see the list of saved stashes:
```bash
$ git stash list
stash@{0}: WIP on master: a1b2c3d Last commit message
stash@{1}: WIP on develop: b2c3d4e Other work in progress
```

To see the content of a stash:
```bash
$ git stash show -p stash@{0}
```

## Recovering a Stash

To recover the last stash and remove it from the stack:
```bash
$ git stash pop
```

To recover a specific stash:
```bash
$ git stash pop stash@{1}
```

To recover a stash without removing it from the stack:
```bash
$ git stash apply stash@{0}
```

## Managing Stashes

To delete a stash without applying it:
```bash
$ git stash drop stash@{0}
```

To delete all stashes:
```bash
$ git stash clear
```

## Advanced Stash Options

**Stash with a message**:
```bash
$ git stash save "Descriptive message of my work in progress"
```

**Stash only unstaged files**:
```bash
$ git stash --keep-index
```

This option is useful if you've already added some modifications to the index and want to keep them!

**Interactive stash**:
```bash
$ git stash -p
```

Like git add -p, this command allows you to interactively choose which modifications to stash.

**Stash including untracked files**:
```bash
$ git stash -u
```

By default, git stash doesn't include untracked files. This option includes them!

## Use Case: Transferring Modifications Between Branches

Even though it's not its initial purpose, stashing can be used to transfer modifications from one branch to another:

```bash
$ git stash
$ git checkout other_branch
$ git stash pop
```

## Use Case: Urgent Commit

You have several modifications in progress, but you need to urgently send only one of them:

```bash
$ git add -p  # Add only the urgent modification
$ git stash --keep-index  # Stash everything else
$ git commit -m "Urgent fix"
$ git push
$ git stash pop  # Recover your work in progress
```

---

**Previous:** [← Atomic Commits](08-atomic-commits.md) | **Next:** [Tags →](10-tags.md)

