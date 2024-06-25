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
``` bash
# 1st Parameter
/login.php

# 2nd Parameter
/login.php:[user parameter]=^USER^&[password parameter]=^PASS^

# 3rd Parameter
/login.php:[user parameter]=^USER^&[password parameter]^PASS^:[FAIL/SUCCESS]=[success/failed string]
```

### Fail/Success String
For Hydra to distinguish between success and failed attempts, we need to specify a *unique string* from source code of the page we're using to login. *Hydra will look at code of response page after each attempt to look for this string*. 

To find a string that you can distinguish against others for finding success, are any strings that will not appear on the page after logging in. In the example, it would be the *login button*. 

If in the code we see the HTML for the login button:
``` HTML
<form name='login' autocomplete='off' class='form' action='' method='post'>
```

We do not have to provide the entire string, so we use "form name='login'", should be distinct enough and probably not exist after a successful login. 

The final syntax would look like:
``` bash
/login.php:[user parameter]=^USER^&[password parameter]=^PASS^:F=<form name='login'
```