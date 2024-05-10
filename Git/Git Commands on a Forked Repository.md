#Git #Development 

#### Questions
*Does origin refer to the master branch of MY fork of a repository?*
	Yes. After cloning a fork of a repository, Git sets up a remote named *origin* pointing to the fork *not the original repo*. So commands like <code>git push</code> or <code>git fetch</code> are for your own forked repo. 
*How does fetch affect my forked repository?*
	It downloads *new data including updates to all branches*, updates a local copy of these branches.  Running <code>git fetch</code> does not alter local branches, it only *updates information* of changes on remote
*What is the difference between git pull & git fetch?*
	<code>git pull</code> : updates the current local branch with latest changes from a *corresponding branch* on a remote repo. Essentially a combo between *git fetch* and *git merge*. 
	<code>git fetch</code> : only brings the latest changes without merging
*What does git fetch origin do?*
	It fetches all updates from a remote *origin* including all branches even the ones you are not currently on. *Without* updating the working files. 
*What does git merge origin/master?*
	Assuming you are on the master branch, this merges the changes from the master branch of the remote repo into the local master. 