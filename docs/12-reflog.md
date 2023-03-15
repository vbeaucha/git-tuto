# The Reflog: Git's Safety Net

## What is the Reflog?

The reflog (reference log) is a local history of all movements of HEAD and branch references. It's like a safety net that allows you to recover "lost" commits.

## Viewing the Reflog

To see the reflog:
```bash
$ git reflog
a1b2c3d HEAD@{0}: commit: Latest commit
d4e5f6g HEAD@{1}: commit: Previous commit
h7i8j9k HEAD@{2}: reset: moving to HEAD^
k0l1m2n HEAD@{3}: commit: Deleted commit
```

Each entry shows:
- The commit ID
- The HEAD position
- The action performed

## Recovering a Lost Commit

Imagine you did a `git reset --hard` and want to recover the deleted commits:

1. Find the commit in the reflog:
```bash
$ git reflog
```

2. Create a new branch from this commit:
```bash
$ git branch recovery HEAD@{3}
```

Or directly checkout the commit:
```bash
$ git checkout HEAD@{3}
```

## Reflog Limitations

The reflog is local to your repository and is not shared with others. Entries are kept for 90 days by default (30 days for unreachable commits).

---

**Previous:** [← Remote Branches](11-remote-branches.md) | **Next:** [Git Workflows →](13-workflows.md)

