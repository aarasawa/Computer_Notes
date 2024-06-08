#OpenLibrary #OpenSource #Development #Guide

#### Code Organization
*core* : core openlibrary functionality, imported and used by www
*plugins* : other models, controllers, and view helpers
*views* : views for rendering web pages
*templates* : all the templates used in the website
*macros* : templates but can be called from wikitext

#### Architecture
##### Backend
Developed using [[Infogami]] wiki system on top of a *web.py* Python web framework and [[Infobase]] database framework. 
##### Running Tests
OpenLibrary test can be run using docker. 
``` ubuntu
docker compose run --rm home make test
```

#### Initial Installation
These steps are after the initial fork and clone. It is easier to do these through *GitHub Desktop*. Verifying that your remote git settings are correct:
``` bash
$ git remote -v
origin git@github.com:USERNAME/openlibrary.git (fetch)
origin git@github.com:USERNAME/openlibrary.git (push)
upstream https://github.com/internetarchive/openlibrary.git (fetch)
upstream https://github.com/internetarchive/openlibrary.git (push)
```
*First*:
	Download Docker, and test using <code>docker run hello-world</code>. Check the output to make sure Docker is *working correctly*.
*Second*: 
``` bash
// Move into the project root directory i.e. where compose.yaml is
cd .../openlibrary/

// Build the openlibrary image
docker compose build

// Start the application
docker compose up # CTRL + C to stop
docker compose up -d # Detached (silent) mode
```
*Third*:
	At this point, you should be able to access the development version of the application on *port 8080*. You can use the login credentials: 
```
	email: openlibrary@example.com
	password: admin123
```

#### Development Commands
##### Starting the Environment
*Make sure your version is up to date*:
``` bash
	// For master to stay up-to-date
	git switch master
	git pull upstream master
	git push origin master
```
Start the docker server:
``` bash
docker compose up
```
Then open: https://localhost:8080

##### Pulling from Prod
``` git
git switch master
git pull -ff-only upstream master
git push origin master

git switch 8829/fix/redesign-sort-ui
```

##### Out-of-Sync Branches
``` bash
# MASTER is behind upstream master
git switch master
git pull upstream master
git push origin master

# MASTER is behind and ahead of upstream master
git switch master
git reset --hard HEAD~[number of commits ahead by]
git pull --ff-only upstream master
git push -f origin master
```
A **"hard" reset** will permanently undo your changes, make sure you are on the master branch before resetting. *Master is always supposed to be identical to upstream version*. 

If you have accidentally committed something your master, reset it with as many commits as you like <code>git reset --hard HEAD~100</code> is a good way to get a clean slate. Then pull in the upstream version. 

``` bash
# Working branch is behind upstream master
git switch master
git pull --ff-only upstream master
git push origin master
git switch [branch-name]
git rebase master
```
If rebasing fails or provokes merge conflicts: [here](https://github.com/internetarchive/openlibrary/wiki/Git-Cheat-Sheet#troubleshooting-your-pull-request)
