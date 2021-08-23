
## Bolt walkthrough

A hero is unleashed.
This room is designed for users to get familiar with the Bolt CMS and how it can be exploited using Authenticated Remote Code Execution. You should wait for at least 3-4 minutes for the machine to start properly.
1. Let’s start by enumerating the services running on the machine with Nmap:
![1 nmapscan](https://user-images.githubusercontent.com/71917246/130395056-a8f2c859-36b4-42d1-a6cf-21f7f301c6cf.png)
2. Browsing the CMS on port 8000.
![2 cms](https://user-images.githubusercontent.com/71917246/130395106-ea260891-daf5-48ae-b8d1-3b25fc4136c2.png)
3. A message from Jake (Admin) that discloses his username:
![3 username](https://user-images.githubusercontent.com/71917246/130395153-f2e5060a-1c8b-4941-8402-ce73ab2a29ee.png)
4. In another post, the password is also revealed:
![4  password](https://user-images.githubusercontent.com/71917246/130395222-df6d57e8-6560-43b6-9423-54fe3a4fae2b.png)
5. Let’s authenticate against the admin interface (http://10.10.177.138:8000/bolt/login) with the credentials gathered previously.
The version is disclosed in the bottom left corner.
![5 cmsversion](https://user-images.githubusercontent.com/71917246/130395287-396dad1c-09d5-4a9d-a990-ee31cbe0ccd6.png)
6. Lets find the exploit in exploit-db.this exploit is authenticated remote code execution.
![6 exploitdb-search](https://user-images.githubusercontent.com/71917246/130395355-84f2ffe0-f754-4670-b1b8-d1102dfcf5b2.png)
7. This exploit added in metasploit.first run metasploit and search this exploit.
![7 msfboltsearch](https://user-images.githubusercontent.com/71917246/130395408-1076dee4-883f-43e8-b536-292289103f58.png)
8. In this exploit set lhost,rhost,username,password then run this exploit and got the shell.
![8 gotshell](https://user-images.githubusercontent.com/71917246/130395453-bdc860e0-4dce-4132-a889-7914f8d95453.png)
9. After getting shell run pwd command to see the current working directory then change directory back to see the final flag.
![9 flag](https://user-images.githubusercontent.com/71917246/130395499-3a4e23da-3379-424a-ba16-d43cadb598e9.png)






