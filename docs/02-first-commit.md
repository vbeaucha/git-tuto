# My Very First Commit

For your first commit, we're going to create a readme.md file:
```bash
$ touch readme.md
```

You can check the status of your repo with the command:
```bash
$ git status

On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	readme.md

nothing added to commit but untracked files present (use "git add" to track)
```

From the *git status* command output, we can clearly see that there are no commits, and that there's a new file in the folder called readme.md.

Add the readme.md file and check the status of the *git status* command:

```bash
$ git add readme.md
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   readme.md
```

We've successfully added the file to the git repo! All that's left is to create our first commit:

```bash
$ git commit -> opens vim to edit your commit message
$ git commit -m "My first commit" -> write a commit message directly
```

Verify with the *git status* command that there's nothing left to commit.

You can see your 1st commit with the command:

```bash
$ git log
commit 878cffad18ea9d1b4f2a0ff24a1dd61f258a0af3 (HEAD -> master)
Author: John Doe <John@doe.com>
Date:   Wed Mar 15 11:24:04 2023 +0100

    My first commit
```

---

**Previous:** [← Configuring Git](01-configuring-git.md) | **Next:** [Understanding Git's Tree Structure →](03-git-tree-structure.md)

