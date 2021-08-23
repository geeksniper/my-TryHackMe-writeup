## Bolt Walkthrough

`A hero is unleashed.
This room is designed for users to get familiar with the Bolt CMS and how it can be exploited using Authenticated Remote Code Execution. You should wait for at least 3-4 minutes for the machine to start properly.`

### `1. Let’s start by enumerating the services running on the machine with Nmap:`


![task 1](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/a8f049e70953850ae0a662ea8cd1d60c52125980/Bolt-walkthrough/bolt-img/1.nmapscan.png)


### `2. Browsing the CMS on port 8000.`


![task 2](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/eddb5c5a59ed82de67c04d6993fcba9feb83db6d/Bolt-walkthrough/bolt-img/2.cms.png)


### `3. A message from Jake (Admin) that discloses his username:`


![task 3](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/eddb5c5a59ed82de67c04d6993fcba9feb83db6d/Bolt-walkthrough/bolt-img/3.username.png)


### `4. In another post, the password is also revealed:`


![task 4](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/eddb5c5a59ed82de67c04d6993fcba9feb83db6d/Bolt-walkthrough/bolt-img/4.%20password.png)


### `5. Let’s authenticate against the admin interface (http://10.10.177.138:8000/bolt/login) with the credentials gathered previously.The version is disclosed in the bottom left corner.`


![task 5](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/eddb5c5a59ed82de67c04d6993fcba9feb83db6d/Bolt-walkthrough/bolt-img/5.cmsversion.png)


### `6. Lets find the exploit in exploit-db.this exploit is authenticated remote code execution.`


![task 6](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/eddb5c5a59ed82de67c04d6993fcba9feb83db6d/Bolt-walkthrough/bolt-img/6.exploitdb-search.png)


### `7. This exploit added in metasploit.first run metasploit and search this exploit.`


![task 7](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/eddb5c5a59ed82de67c04d6993fcba9feb83db6d/Bolt-walkthrough/bolt-img/7.msfboltsearch.png)


### `8. In this exploit set lhost,rhost,username,password then run this exploit and got the shell.`


![task 8](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/eddb5c5a59ed82de67c04d6993fcba9feb83db6d/Bolt-walkthrough/bolt-img/8.gotshell.png)


### `9. After getting shell run pwd command to see the current working directory then change directory back to see the final flag.`


![task 9](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/eddb5c5a59ed82de67c04d6993fcba9feb83db6d/Bolt-walkthrough/bolt-img/9.flag.png)


## finished









