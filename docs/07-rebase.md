# Rebase: An Alternative to Merge

## What is Rebase?

Rebase is an alternative to merging for integrating changes from one branch into another. Instead of creating a merge commit, rebase rewrites history by moving your commits to the top of the target branch.

## Difference Between Merge and Rebase

Let's revisit our previous example with the master and develop branches. Instead of merging, we're going to rebase!

Make sure you're on the develop branch:
```bash
$ git checkout develop
```

Now, instead of merging master into develop, we're going to rebase develop onto master:
```bash
$ git rebase master
```

This command does several things:
1. Temporarily saves all commits from develop that aren't in master
2. Moves the develop branch to the same level as master
3. Reapplies the saved commits one by one

The result is a linear history, without a merge commit!

```bash
$ git lg
* a1b2c3d (HEAD -> develop) changed numbers to multiply by 7 and 4
* 0f24fb4 (master) changed numbers to multiply
* d1d19e0 added script.js file
* 250fe34 Added gitignore
* 6b6a4c8 Added lines to readme.md file
* 878cffa My first commit
```

## Resolving Conflicts During Rebase

Like with merge, conflicts can occur during a rebase. Git will ask you to resolve them before continuing.

When a conflict occurs:
1. Resolve the conflict in the affected file
2. Add the resolved file to the index: `git add <file>`
3. Continue the rebase: `git rebase --continue`

If you want to abort the rebase:
```bash
$ git rebase --abort
```

## When to Use Rebase vs Merge?

**Use merge**:
- To integrate completed feature branches into the main branch
- When working on branches shared with other developers
- When you want to preserve the complete history of modifications

**Use rebase**:
- To maintain a linear and clean history
- Before pushing your local commits to a remote repository
- To update your working branch with the latest changes from the main branch

**WARNING**: Never rebase commits that have already been pushed to a shared repository! This rewrites history and can cause problems for your collaborators.

## Interactive Rebase

Interactive rebase is a powerful tool for cleaning up your history before sharing it!

```bash
$ git rebase -i HEAD~3
```

This command opens your editor with the list of the last 3 commits:
```
pick a1b2c3d First commit
pick d4e5f6g Second commit
pick h7i8j9k Third commit

# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into previous commit
# f, fixup = like "squash", but discard this commit's log message
# d, drop = remove commit
```

You can do several things:
- **pick**: keep the commit as is
- **reword**: modify the commit message
- **edit**: modify the commit content
- **squash**: merge the commit with the previous one keeping both messages
- **fixup**: merge the commit with the previous one ignoring its message
- **drop**: delete the commit

Example: merge the last two commits:
```
pick a1b2c3d First commit
pick d4e5f6g Second commit
squash h7i8j9k Third commit
```

Save and close the editor. Git will then ask you to modify the message of the merged commit!

---

**Previous:** [← Sharing Your Repository](06-sharing-repositories.md) | **Next:** [Atomic Commits →](08-atomic-commits.md)

