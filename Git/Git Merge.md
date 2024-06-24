#Git #GitMerge

To combine the work from different branches together, we can use:
``` bash
git merge
```
Merging creates a special commit with two unique parents. Saying it wants to include all the work from both these parents and the set of all their parents. For example, if you have a branch bugFix and main. You make changes on bugFix, commit the changes; and have committed work on main. Running a merge will combine the work on both branches, so bugFix merges into main. 