#HydraSoftware #PasswordCracking #UsernameCracking 

### Brute Forcing Forms
Hydra has 2 types of *http* modules for brute forcing forms: 
	**http[s] -{head|get|post}** - basic HTTP authentication
	**http[s] -post-form** - login forms .php, .aspx, etc
If inputs of the form are pasted into the URL, the application uses a GET, otherwise it is a POST.

For example, if we use *http-post-form*, there are 3 parameters separated by colons:
	1. **URL path** - path of login form
	2. **POST parameters** - for login creds
	3. **failed/successful login string** - hydra to recognize login attempt was successful or not

### Fail/Success String
