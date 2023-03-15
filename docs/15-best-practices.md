# Best Practices

## Commit Messages

A good commit message should:
- Start with a short summary (50 characters max)
- Use the imperative mood ("Add feature" not "Added feature")
- Explain **why** the change was made, not just what

Example of a good commit message:
```
Add user authentication feature

Implement JWT-based authentication to secure API endpoints.
This addresses security concerns raised in issue #123.
```

Example of a bad commit message:
```
fix stuff
```

## Atomic Commits

Each commit should represent a single logical change:
- ✅ Good: "Add login validation" + "Add logout button"
- ❌ Bad: "Add login validation and logout button and fix typo in readme"

Benefits:
- Easier to review
- Easier to revert if needed
- Clearer history

## Commit Frequency

**Commit often!** Don't wait until the end of the day to commit.

- Commit after each logical unit of work
- Commit before risky operations
- Commit before switching tasks

Remember: commits are cheap and local until you push!

## Before Pushing

Before pushing your commits to a shared repository:

1. **Review your commits**:
```bash
$ git log --oneline origin/master..HEAD
```

2. **Clean up your history** (if needed):
```bash
$ git rebase -i origin/master
```

3. **Make sure tests pass**:
```bash
$ npm test  # or your test command
```

4. **Pull the latest changes**:
```bash
$ git pull --rebase origin master
```

5. **Push**:
```bash
$ git push origin master
```

## Never Rewrite Shared History

**NEVER** use these commands on commits that have been pushed to a shared repository:
- `git reset` (on shared commits)
- `git rebase` (on shared commits)
- `git commit --amend` (on shared commits)

Why? Because it rewrites history and causes problems for your collaborators.

If you need to undo a shared commit, use `git revert` instead!

## Use .gitignore

Always create a .gitignore file to exclude:
- Build artifacts (dist/, build/, *.o, *.class)
- Dependencies (node_modules/, vendor/)
- IDE files (.vscode/, .idea/, *.swp)
- OS files (.DS_Store, Thumbs.db)
- Environment files (.env, .env.local)
- Log files (*.log)

Example .gitignore for a Node.js project:
```
node_modules/
dist/
.env
.env.local
*.log
.DS_Store
```

Tips:
- Create .gitignore at the start of your project
- Use templates from https://github.com/github/gitignore
- Include common patterns for your language/framework
- Don't commit sensitive information (passwords, API keys)
- Don't commit generated files (build artifacts, dependencies)

---

**Previous:** [← Advanced Commands](14-advanced-commands.md) | **Next:** [Conclusion →](16-conclusion.md)

