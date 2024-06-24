#Git #GitBranch

**Branches** are pointers to a specific commit. There is no storage or memory overhead with making a bunch of branches. *It is easier to logically divide up work than to have big beefy branches.* A branch says you want to include the work of this commit and all parent commits. 
``` bash
git checkout <name>
```
Will move the current branch to the one referred to as "name". 