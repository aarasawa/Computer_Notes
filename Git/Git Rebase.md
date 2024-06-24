#Git #GitRebase

**Rebase** takes a set of commits, copies them, and moves them somewhere else. It is used to create a *linear sequence of commits*, the commit log/history of the repo will be a lot cleaner if rebasing is allowed. 
``` bash
# Starting with main and a branch bugFix
c0 -> c1 -> c2 [main]
		 -> c3 [*bugFix]

# Run git rebase main
# Move work from bugFix directly onto the work from main, so it looks like
# features were developed sequentially rather than in parallel
c0 -> c1 -> c2 [main] -> c3~ [*bugFix]

# Checkout main then run git rebase bugFix
# Main is moved to c3~ (rebase node of c3)
c0 -> c1 -> c2 -> c3~ [*main, bugFix]
```
