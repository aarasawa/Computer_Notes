#pre-commit #testcases #OpenLibrary #OpenSource 

[Link to Wiki](https://github.com/internetarchive/openlibrary/wiki/Git-Cheat-Sheet#pre-commit-and-the-github-ci)
For the purpose of enforcing formatting practices in the codebase, incoming PRs have to pass a set of JS and Py checks. 
### Running pre-commit Locally
Since you have pre-commit installed, it is apparent that it runs every time you add a commit to the branch. If a *commit fails and of the checks*:
1. Check will initially fail and staged commits will not be committed, pre-commit auto-adds changes to fix problem. Then a new unstaged git change will appear. 
2. Check fails and staged commits will not go through, an error message will appear. 