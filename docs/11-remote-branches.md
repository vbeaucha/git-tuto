# Remote Branches

## Understanding Remote Branches

When you clone a repository, Git creates local references to the remote branches. These references are named `origin/<branch_name>`.

To see all branches (local and remote):
```bash
$ git branch -a
* master
  develop
  remotes/origin/master
  remotes/origin/develop
```

## Tracking Remote Branches

When you create a local branch from a remote branch, Git automatically sets up tracking:
```bash
$ git checkout -b develop origin/develop
```

Or more simply (Git automatically finds the remote branch):
```bash
$ git checkout develop
```

## Updating Remote References

To update your local references to remote branches:
```bash
$ git fetch origin
```

This downloads new commits from the remote repository but doesn't modify your working branches.

## Deleting Remote Branches

To delete a branch on the remote repository:
```bash
$ git push origin --delete branch_name
```

---

**Previous:** [← Tags](10-tags.md) | **Next:** [The Reflog: Git's Safety Net →](12-reflog.md)

