# Atomic Commits!

## Breaking Down Your Commits

A good practice with Git is to break down the modifications to be recorded in the repository into atomic (or unitary) entities.

This practice allows you to:
- Better track and understand the modifications made
- More easily find a modification
- Reverse a modification without touching the rest (when possible)

But how do you do this if all your modifications are in the same file?

## Interactive Add with git add -p

The -p (--patch) option of the git add command allows you to interactively select the pieces of code you want to add to the index!

Let's create an example. Modify your script.js file to add a new function and use it:

```js
function multiply(a,b){
        console.log("we're going to multiply "+a+" and "+b)
        return a*b
}

function additionner(a,b){
        console.log("we're going to add "+a+" and "+b)
        return a+b
}

console.log("multiplication result: "+ multiply(7,4));
console.log("addition result: "+ additionner(5,3));
```

Now, let's use git add -p to add only the new function:
```bash
$ git add -p script.js
```

Git will break down the modifications into chunks (hunks) and ask you what you want to do with each one:
```
Stage this hunk [y,n,q,a,d,/,s,e,?]?
```

Answer **?** to see the available options:
- **y**: add this chunk to the index
- **n**: don't add this chunk
- **s**: split the chunk into smaller chunks
- **e**: manually edit the chunk
- **q**: quit

If the modifications are too close together, use **s** to separate them, then **y** for the function and **n** for its usage!

You can now create two separate commits:
```bash
$ git commit -m "Added the additionner function"
$ git add script.js
$ git commit -m "Using the additionner function"
```

## Interactive Unstaging with git reset -p

Sometimes, we realize after the fact that a modification was added to the index by mistake.

The git reset -p command allows you to selectively unstage modifications:
```bash
$ git reset -p
```

This command works like git add -p, but in reverse!

## Interactive Cancellation with git checkout -p

To selectively cancel modifications in your working directory (without having added them to the index), use:
```bash
$ git checkout -p
```

**Warning**: This command permanently deletes the selected modifications!

---

**Previous:** [← Rebase: An Alternative to Merge](07-rebase.md) | **Next:** [Stashing →](09-stashing.md)

