#HydraSoftware #BruteForcing #BurpSuite

### Using Browser
You can capture form parameters using Network Tools on most browsers. It will show HTTP requests. Another option is to copy as a cURL to see how the request is structured. 

### Using Burp Suite
Easier to use Burp Suite to go through the HTTP requests for a webpage that sends multiple and pick the ones we need. 
``` bash
# In the example intercepted HTTP request, what we need is this line
username=admin&password=admin

# To use in hydra-post-form, use as is and replace the corresponding fields
/login.php:username=^USER^&password=^PASS^:F=<form name='login'
```