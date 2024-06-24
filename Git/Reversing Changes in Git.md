#Git #ReverseChanges

There are two primary ways to undo changes in Git:
``` bash
# Moves branch backwards to an older commit, as if the commit had never been made
# Good for local branches on own machine
git reset

# Reverse changes and share reversions with others use revert
git revert
```