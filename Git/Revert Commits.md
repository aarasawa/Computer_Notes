#Git #Commit #RevertChanges

Source: [here](https://stackoverflow.com/questions/4114095/how-do-i-revert-a-git-repository-to-a-previous-commit)

``` bash
# Destroy local modifications
# Don't do if you have uncommitted work you want to keep
git reset --hard #commit-tag

# If you want to keep work
git stash
git reset --hard $#commit-tag
git stash pop
```