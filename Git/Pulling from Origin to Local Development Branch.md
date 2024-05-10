#Git #GitHub #Development 

#### How to "git pull" from master into development branch
*Source*: [link](https://stackoverflow.com/questions/20101994/how-to-git-pull-from-master-into-the-development-branch)
Given: 
	Development branch: *development*
	Master branch: *master*
*What is happening in the poster's Git commands?*
``` bash
git checkout development # get into branch "development"
git fetch origin         # get you up to date with origin
git merge origin/master
```
In order:
1. It switches the current working branch to *development*, if this branch does not exist locally then Git tries to find a remote one with the same name and checks out as a new local branch. 
2. Fetch *updated information* from *origin*, usually main upstream repo without changing working files. 
3. Merges changes to *master* from the *origin* on your machine into local checkout branch *development*. 
*Information about these commands to know*:
	<code>fetch</code> can be done any time before a <code>merge</code> since because fetch goes to origin, takes any updates and *copies* it to *origin/branch* for any branch *named branch* in remote. 
	*My questions*
		*Does origin mean the original repository that you have forked or cloned?*
			
		*When updates are copied to "origin/branch" is this a branch on my machine?*