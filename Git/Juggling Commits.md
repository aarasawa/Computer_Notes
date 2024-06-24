#Git 

If there are changes you need to make to a prior commit, stacked on top of another one. To do this:
	1. Re-order commits so the one we want to change is on top <code>git rebase -i</code>
	2. <code>git commit --amend</code> to make a slight change
	3. Re-order again to how they previously were
	4. Move *main* to updated part of the tree