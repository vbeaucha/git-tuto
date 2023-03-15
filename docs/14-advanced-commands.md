# Advanced Commands

## git cherry-pick: Apply a Specific Commit

Sometimes you want to apply a specific commit from one branch to another without merging the entire branch.

```bash
$ git cherry-pick a1b2c3d
```

This command creates a new commit on your current branch with the same changes as commit a1b2c3d.

**Use case**: You fixed a bug on the develop branch and want to apply the same fix to master without merging all of develop.

## git worktree: Work on Multiple Branches Simultaneously

Git worktrees allow you to have multiple working directories for the same repository, each checked out to different branches. This is incredibly useful when you need to work on multiple branches at the same time without constantly switching contexts.

### Why Use Worktrees?

Instead of stashing your work or committing incomplete changes when you need to switch branches, you can simply switch to a different worktree. Each worktree has its own working directory, but they all share the same repository (commits, branches, tags).

### Creating a Worktree

To create a new worktree for an existing branch:
```bash
$ git worktree add ../project-hotfix hotfix-branch
```

To create a new worktree and a new branch at the same time:
```bash
$ git worktree add ../project-feature -b feature/new-feature
```

This creates a new directory `../project-feature` with the `feature/new-feature` branch checked out.

### Listing Worktrees

To see all worktrees associated with your repository:
```bash
$ git worktree list
/Users/you/project        a1b2c3d [master]
/Users/you/project-hotfix d4e5f6g [hotfix-branch]
/Users/you/project-feature h7i8j9k [feature/new-feature]
```

### Removing a Worktree

When you're done with a worktree, remove it:
```bash
$ git worktree remove ../project-hotfix
```

Or, if you've already deleted the directory manually:
```bash
$ git worktree prune
```

The `prune` command cleans up worktree information for directories that no longer exist.

### Real-World Use Case

Imagine you're working on a new feature when an urgent bug report comes in:

```bash
# You're currently working on a feature with uncommitted changes
$ cd ~/project
$ git status
# ... lots of modified files ...

# Create a worktree for the hotfix
$ git worktree add ../project-hotfix master
$ cd ../project-hotfix

# Fix the bug, commit, and push
$ vim bug-file.js
$ git add bug-file.js
$ git commit -m "Fix critical bug"
$ git push

# Go back to your feature work - your changes are still there!
$ cd ~/project
$ git status
# ... your uncommitted changes are untouched ...

# Clean up the hotfix worktree when done
$ git worktree remove ../project-hotfix
```

### Important Notes

**Limitations**:
- You cannot check out the same branch in multiple worktrees simultaneously
- Each worktree needs its own disk space for the working directory

**Best Practices**:
- Use descriptive directory names for your worktrees
- Clean up worktrees when you're done with them to avoid clutter
- Remember that all worktrees share the same repository, so commits made in one worktree are immediately visible in others

**Tip**: Worktrees are especially useful for:
- Code reviews (check out the PR branch in a separate worktree)
- Running tests on one branch while developing on another
- Comparing implementations across branches side-by-side

## git bisect: Find the Commit That Introduced a Bug

git bisect uses binary search to find which commit introduced a bug.

Start the bisect session:
```bash
$ git bisect start
$ git bisect bad  # Current version is bad
$ git bisect good a1b2c3d  # This old commit was good
```

Git will checkout a commit in the middle. Test it and tell Git:
```bash
$ git bisect good  # If the commit is good
# or
$ git bisect bad  # If the commit is bad
```

Repeat until Git finds the problematic commit. Then end the session:
```bash
$ git bisect reset
```

## git blame: Find Who Modified a Line

To see who last modified each line of a file:
```bash
$ git blame script.js
```

Output:
```
878cffad (John Doe 2023-03-15 11:24:04 +0100 1) function multiply(a,b){
878cffad (John Doe 2023-03-15 11:24:04 +0100 2)     console.log("we're going to multiply "+a+" and "+b)
878cffad (John Doe 2023-03-15 11:24:04 +0100 3)     return a*b
878cffad (John Doe 2023-03-15 11:24:04 +0100 4) }
```

To see only lines 5-10:
```bash
$ git blame -L 5,10 script.js
```

## git diff: Compare Changes

Compare working directory with index:
```bash
$ git diff
```

Compare index with last commit:
```bash
$ git diff --staged
```

Compare two commits:
```bash
$ git diff a1b2c3d d4e5f6g
```

Compare two branches:
```bash
$ git diff master develop
```

## git clean: Remove Untracked Files

To see which files would be deleted:
```bash
$ git clean -n
```

To delete untracked files:
```bash
$ git clean -f
```

To also delete untracked directories:
```bash
$ git clean -fd
```

**Warning**: This permanently deletes files!

## git archive: Create a Project Archive

To create a zip archive of your project:
```bash
$ git archive --format=zip --output=project.zip master
```

To create a tar.gz archive:
```bash
$ git archive --format=tar.gz --output=project.tar.gz master
```

## Useful Git Aliases

Add these aliases to your Git configuration for faster commands:

```bash
$ git config --global alias.co checkout
$ git config --global alias.br branch
$ git config --global alias.ci commit
$ git config --global alias.st status
$ git config --global alias.unstage 'reset HEAD --'
$ git config --global alias.last 'log -1 HEAD'
$ git config --global alias.visual 'log --oneline --graph --decorate --all'
```

Now you can use:
```bash
$ git co master  # instead of git checkout master
$ git st  # instead of git status
$ git visual  # beautiful graph of all branches
```

---

**Previous:** [← Git Workflows](13-workflows.md) | **Next:** [Best Practices →](15-best-practices.md)

