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
			Origin in the context of the *forked* repo refers to the forked master branch. So any fetches or pushes remain in the context of the forked repo.
		*When updates are copied to "origin/branch" is this a branch on my machine?*
			Yes. Fetching or pulling updates information from the original repository and *in the case of fetch* updates information for respective branches. 
##### Recommended process
``` bash
git fetch origin
git checkout master
git merge --ff-only origin/master
git checkout development
git merge --no-ff origin/master
```
*First Impressions*:
	So a first guess about what is being done here: get updated information from the original repository, change to local master branch, merge updates to the local master, change to development branch, merge updates with do not conflict
*What actually happens*: