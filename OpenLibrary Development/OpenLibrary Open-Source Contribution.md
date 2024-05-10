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

