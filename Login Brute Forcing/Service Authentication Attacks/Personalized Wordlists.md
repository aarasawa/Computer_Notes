#BruteForcing #Wordlists #HydraSoftware 

**Personalized wordlists** require prior information collection, for example, checking Wikipedia or a Google search. 
### CUPP
The tool **cupp** is what we are going to use to create a custom password wordlist based on certain information. We can run cupp in interactive mode by specifying *-i* argument.
```shell-session
SwampFIsh@htb[/htb]$ cupp -i

___________
   cupp.py!                 # Common
      \                     # User
       \   ,__,             # Passwords
        \  (oo)____         # Profiler
           (__)    )\
              ||--|| *      [ Muris Kurgas | j0rgan@remote-exploit.org ]
                            [ Mebus | https://github.com/Mebus/]


[+] Insert the information about the victim to make a dictionary
[+] If you don't know all the info, just hit enter when asked! ;)

> First Name: William
> Surname: Gates
> Nickname: Bill
> Birthdate (DDMMYYYY): 28101955

> Partners) name: Melinda
> Partners) nickname: Ann
> Partners) birthdate (DDMMYYYY): 15081964

> Child's name: Jennifer
> Child's nickname: Jenn
> Child's birthdate (DDMMYYYY): 26041996

> Pet's name: Nila
> Company name: Microsoft

> Do you want to add some key words about the victim? Y/[N]: Phoebe,Rory
> Do you want to add special chars at the end of words? Y/[N]: y
> Do you want to add some random numbers at the end of words? Y/[N]:y
> Leet mode? (i.e. leet = 1337) Y/[N]: y

[+] Now making a dictionary...
[+] Sorting list and removing duplicates...
[+] Saving dictionary to william.txt, counting 43368 words.
[+] Now load your pistolero with william.txt and shoot! Good luck!
```
Generating a custom wordlist with cupp looks like this.
### Password Policy
If there are password conditions such as: *8 characters or longer, contains special characters, and contains numbers*. Since *hydra* does not support filtering passwords based on rules, we can do:
``` shell-session
sed -ri '/^.{,7}$/d' william.txt            # remove shorter than 8
sed -ri '/[!-/:-@\[-`\{-~]+/!d' william.txt # remove no special chars
sed -ri '/[0-9]+/!d' william.txt            # remove no numbers
```
### Mangling
Basically creating as many permutations of each word in the list. There are tools like **rsmangler** and **The Mentalist** for mangling wordlists. 
### Custom Username Wordlist
Tools like **Username Anarchy** can create potential variations for usernames. After downloading from GitHub we can use it.
``` bash
./username-anarchy Bill Gates > bill.txt
```