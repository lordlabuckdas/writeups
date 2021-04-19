# [OWASP Top10 from TryHackMe](https://tryhackme.com/room/owasptop10)

## Task 5 - [Severity 1] Command Injection Practical

1. What strange text file is in the website root directory?

	`ls -al` gives us this

	![list of files](/assets/thm/files.png)

	so, the weird text file is `drpepper.txt`

2. How many non-root/non-service/non-daemon users are there?

	careful inspection of the `etc/passwd` file tells us that there no such users - `0`

	![/etc/passwd](/assets/thm/passwd.png)

3. What user is this app running as?

	`whoami` gives us `www-data`

	![whoami](/assets/thm/whoami.png)

4. What is the user's shell set as?

	this can again be found from `/etc/passwd/`

	it is `/usr/sbin/nologin`

5. What version of Ubuntu is running?

	`lsb_release -a` will tell us that Ubuntu `18.04.4` is running

	![lsb](/assets/thm/lsb.png)

6. Print out the MOTD. What favorite beverage is shown?

	i went out on a limb to try `Dr Pepper` and it was right
