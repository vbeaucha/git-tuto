# Tags

## What are Tags?

Tags are references to specific commits in your history. Unlike branches, tags don't move when you create new commits. They're mainly used to mark important versions of your project (v1.0, v2.0, etc.).

## Creating Tags

There are two types of tags in Git:

**Lightweight tags** (simple pointers to a commit):
```bash
$ git tag v1.0
```

**Annotated tags** (complete objects with author, date, and message):
```bash
$ git tag -a v1.0 -m "Version 1.0 of the project"
```

Annotated tags are recommended for releases because they contain more information.

## Listing Tags

To see all tags:
```bash
$ git tag
v1.0
v1.1
v2.0
```

To see tag details:
```bash
$ git show v1.0
```

## Tagging an Old Commit

You can tag a commit after the fact by specifying its ID:
```bash
$ git tag -a v0.9 -m "Version 0.9" 878cffa
```

## Pushing Tags

By default, git push doesn't send tags to the remote repository. You need to explicitly push them:

Push a specific tag:
```bash
$ git push origin v1.0
```

Push all tags:
```bash
$ git push origin --tags
```

## Deleting Tags

Delete a local tag:
```bash
$ git tag -d v1.0
```

Delete a remote tag:
```bash
$ git push origin --delete v1.0
```

## Checking Out a Tag

To view the state of the project at a specific tag:
```bash
$ git checkout v1.0
```

**Warning**: This puts you in "detached HEAD" state. If you want to make modifications, create a new branch:
```bash
$ git checkout -b version-1.0-fixes v1.0
```

---

**Previous:** [← Stashing](09-stashing.md) | **Next:** [Remote Branches →](11-remote-branches.md)

