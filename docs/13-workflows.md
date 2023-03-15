# Git Workflows

## Centralized Workflow

The simplest workflow, similar to SVN:
- A single master branch
- Everyone works on master
- Regular pull/push

**Advantages**: Simple to understand
**Disadvantages**: Risk of conflicts, no isolation of features

## Feature Branch Workflow

Each new feature is developed in a dedicated branch:
```bash
$ git checkout -b feature/new-feature
# Work on the feature
$ git checkout master
$ git merge feature/new-feature
```

**Advantages**: Isolation of features, easier code review
**Disadvantages**: Can lead to long-lived branches

## Gitflow Workflow

A more structured workflow with specific branches:
- **master**: production code
- **develop**: integration branch
- **feature/**: feature branches
- **release/**: release preparation branches
- **hotfix/**: urgent fix branches

**Advantages**: Very structured, suitable for scheduled releases
**Disadvantages**: Can be complex for small projects

## Forking Workflow

Used in open-source projects:
- Each developer has their own remote repository (fork)
- Modifications are proposed via pull requests
- Maintainers review and merge

**Advantages**: No need to give write access to everyone
**Disadvantages**: More complex to set up

---

**Previous:** [← The Reflog: Git's Safety Net](12-reflog.md) | **Next:** [Advanced Commands →](14-advanced-commands.md)

