#Git #GitRefs

When moving around Git, specifying a commit can take a lot of effort. 
``` bash
# Use git log to see hashes
git log
```
Git is smart and requires you to specify enough characters of the hash until it uniquely identifies the commit. 

**Relative refs** allow you to start somewhere memorable like branch names or HEAD. *Relative commits*: use **^** to move upwards 1 commit at a time, or move upwards a number of times with      **~<.num>**.
``` bash
# Specifies to checkout the parent of main
git checkout main^
```

To move a branch to a commit, use the option:
``` bash
# -f option reassigns a branch to a commit
# The cmd moves the main branch to 3 parents behind HEAD
git branch -f main HEAD~3
```