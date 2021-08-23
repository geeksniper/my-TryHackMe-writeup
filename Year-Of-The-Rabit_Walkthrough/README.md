## Year Of The Rabbit_Walkthrough

Year of the Rabbit is an easy level box on THM created by MuirlandOracle. I definitely had a lot of fun hacking this box, and it also has a cute surprise that I’m sure everyone will enjoy! It’s got a good mix of different CTF elements such as steganography, web app, and others.

1. First do nmap scan using machine ip.We’re going to omit the -p flag so nmap will do a quicker scan of the most common ports, we should get some results back relatively quickly that includes most scan info.

![task 1](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/0262db8f58e8e50000e2720ff86536ff313761be/Year-Of-The-Rabit_Walkthrough/yearoftherabit-img/1.%20nmap-scan.png)

The results show us that it’s got a web service, FTP, and SSH enabled on the machine. Let’s start off by looking at the web page.

2. Looks like the default Apache2 landing page, nothing too exciting on the main page and the page source doesn’t reveal much either.

![task 2](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/18000fea3a413dfd63f51dd5ecf267fe36f70cd6/Year-Of-The-Rabit_Walkthrough/yearoftherabit-img/2.%20default-siteview.png)

3. Use gobuster for directory bruteforce.

![task 3](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/5b4b28b78db2622295c1262d0088841a6c47d765/Year-Of-The-Rabit_Walkthrough/yearoftherabit-img/3.%20got-hidden-directory.png)

I used a pre-made list “common.txt” file from the dirb directory and it proved sufficient in this case.we got assets directory.lets jump into it.

4. We’ll go to the assets directory and take a look at the `style.css` file there. There’s a hint hidden within the file.

![task 4](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/f56ab7216e2b15f827b8243e5243787bf9a2e640/Year-Of-The-Rabit_Walkthrough/yearoftherabit-img/4.%20got-hidden-directory-in-css-comment.png)

Nice! We got another lead to work with. Let’s go the page next.

5. When we load into it, there’s a pop-up with a prompt to turn off your Javascript. A quick web search should take care of that.

![task 5](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/f56ab7216e2b15f827b8243e5243787bf9a2e640/Year-Of-The-Rabit_Walkthrough/yearoftherabit-img/5.%20its-popup-js-error.png)

Once it’s off, we’ll be taken to a page with a hint embedded within the video. Make sure to watch the entire video because you never know…. could be more clues at  the end right??With the clue we got from the video, let’s dig deeper and see what’s hidden on web page.

6. We inspect this page and got a hidden directory in response header `location`.

![task 6](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/f56ab7216e2b15f827b8243e5243787bf9a2e640/Year-Of-The-Rabit_Walkthrough/yearoftherabit-img/6.%20we-inspect-this-phpfile-and-got-hidendirectory-in-response-header.png)

7. Goto this hidden directory.

![task 7](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/6f9a6be88bf657fd2b273f68eafbe2abebd96045/Year-Of-The-Rabit_Walkthrough/yearoftherabit-img/7.%20goto-this-directory-got-a-picture-download-it.png)

The hidden directory contains a `PNG image` file named Hot_Babe.png. Sounds like a stego challenge, so go ahead and download the file to analyze offline.

8.0 Analyze this image with `string` command.

![task 8.0](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/6f9a6be88bf657fd2b273f68eafbe2abebd96045/Year-Of-The-Rabit_Walkthrough/yearoftherabit-img/8.0%20see-the-string-value-of-this-image.png)

8.1 We got a viable `username` and also a list of potential `passwords`.

![task 8.1](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/6f9a6be88bf657fd2b273f68eafbe2abebd96045/Year-Of-The-Rabit_Walkthrough/yearoftherabit-img/8.1%20got-ftp-user-name-and-password.png)

9. Copy all the passwords into a text file and let’s run through the passwords list using Hydra to find our way into the machine.

![task 9](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/2d1ea345944f16606cdeaa895fa9d33350daea5a/Year-Of-The-Rabit_Walkthrough/yearoftherabit-img/9.%20use-hydra-for-password-bruteforce-and-got-ftp-password.png)

Perfect, we found our password for `ftpuser` from the list.

10. Login with this ftp credential.there’s only one file on the FTP server called “Eli’s_Creds.txt”, juicy. Let’s download it.

![task 10](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/2d1ea345944f16606cdeaa895fa9d33350daea5a/Year-Of-The-Rabit_Walkthrough/yearoftherabit-img/10.%20login-ftp-got-a-file-download-the-file.png)

11. Let’s open this text file.

![task 11](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/2d1ea345944f16606cdeaa895fa9d33350daea5a/Year-Of-The-Rabit_Walkthrough/yearoftherabit-img/11.%20open-the-file-got-this-now-need-to-decode.png)

12. The very strange looking encoded text is actually an esoteric programming language called [Brainf**k](https://en.wikipedia.org/wiki/Brainfuck). Luckily there’s a publicly available [decoder online](https://www.dcode.fr/brainfuck-language), so it’s as simple as a clicking a button.

![task 12](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/77e7d02175015a0f9f6f8f3cb75e7c5020e6d934/Year-Of-The-Rabit_Walkthrough/yearoftherabit-img/12.%20decode-this-string-got-the-ssh-userand-password.png)

13. With the user credentials, we can login via `SSH`. Interesting MOTD message the moment we log in, so we find out immediately that there’s another user named `Gwendoline` and a hidden message on the machine.

![task 13](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/77e7d02175015a0f9f6f8f3cb75e7c5020e6d934/Year-Of-The-Rabit_Walkthrough/yearoftherabit-img/13.%20login-ssh-using-username-and-password.png)

14. There’s a word that’s spelt differently than everything else, so maybe that’s our keyword? Running a quick find command, we find that it does indeed point to a directory.

![task 14](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/77e7d02175015a0f9f6f8f3cb75e7c5020e6d934/Year-Of-The-Rabit_Walkthrough/yearoftherabit-img/14.%20find-serct-file-and-got-the-password-of-gwendoline.png)

15. The message is only for Gwendoline but it’s readable by everyone? Don’t mind if we do. The message contains Gwendoline’s password so let’s switch users and find that user flag. Running a quick find command, we find that the `user.txt` file is located on their desktop.

![task 15](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/77e7d02175015a0f9f6f8f3cb75e7c5020e6d934/Year-Of-The-Rabit_Walkthrough/yearoftherabit-img/15.%20switch-user-and-got-user-flag.png)

16. The `(ALL, !root) NO PASSWD:` portion of of the output is supposed to allow the user to run the programs as any other user besides root. That’s better safety practice than allowing full root access right? It sounds safe, but there was a major security flaw `(CVE-2019-14287)` found in all versions of `Sudo` prior to `1.8.28`. The vulnerability allows the user to bypass the security policy.

![task 16](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/77e7d02175015a0f9f6f8f3cb75e7c5020e6d934/Year-Of-The-Rabit_Walkthrough/yearoftherabit-img/16.%20sudo-permission-for-privesc.png)

17. This means that we can use the exploit along with the `vi` and `user.txt` to privilege escalate. When working with binaries in a privesc situation, the [GTFOBins page](https://gtfobins.github.io/gtfobins/vi/) works wonders in helping us leverage the binary to get root.

![task 17](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/77e7d02175015a0f9f6f8f3cb75e7c5020e6d934/Year-Of-The-Rabit_Walkthrough/yearoftherabit-img/17.%20edit-vi-for-root-permission.png)

18. Let’s get cracking then! Use the `sudo -u#-1` syntax as noted on the website and copy the other parts from the `sudo -l` command.Nice! We got our root shell working and able to open the root flag!.

![task 18](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/77e7d02175015a0f9f6f8f3cb75e7c5020e6d934/Year-Of-The-Rabit_Walkthrough/yearoftherabit-img/18.%20after-editing-vi-file-got-root-flag.png)

## finished







