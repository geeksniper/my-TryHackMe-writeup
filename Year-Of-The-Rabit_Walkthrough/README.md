## Year Of The Rabbit_Walkthrough

Year of the Rabbit is an easy level box on THM created by MuirlandOracle. I definitely had a lot of fun hacking this box, and it also has a cute surprise that I’m sure everyone will enjoy! It’s got a good mix of different CTF elements such as steganography, web app, and others.

1. First do nmap scan using machine ip.We’re going to omit the -p flag so nmap will do a quicker scan of the most common ports, we should get some results back relatively quickly that includes most scan info.

![task 1](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/0262db8f58e8e50000e2720ff86536ff313761be/Year-Of-The-Rabit_Walkthrough/yearoftherabit-img/1.%20nmap-scan.png)

The results show us that it’s got a web service, FTP, and SSH enabled on the machine. Let’s start off by looking at the web page.

2. Looks like the default Apache2 landing page, nothing too exciting on the main page and the page source doesn’t reveal much either.

![task 2](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/81d426b322701c188782f2914ba8166ae28b51a9/Year-Of-The-Rabit_Walkthrough/yearoftherabit-img/2.%20default-siteview.png)

3. Use go buster for directory bruteforce.

![task 3](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/5b4b28b78db2622295c1262d0088841a6c47d765/Year-Of-The-Rabit_Walkthrough/yearoftherabit-img/3.%20got-hidden-directory.png)

I used a pre-made list “common.txt” file from the dirb directory and it proved sufficient in this case.we got assets directory.lets jump into it.

4. We’ll go to the assets directory and take a look at the style.css file there. There’s a hint hidden within the file.

![task 4](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/f56ab7216e2b15f827b8243e5243787bf9a2e640/Year-Of-The-Rabit_Walkthrough/yearoftherabit-img/4.%20got-hidden-directory-in-css-comment.png)

Nice! We got another lead to work with. Let’s go the page next.

5. When we load into it, there’s a pop-up with a prompt to turn off your Javascript. A quick web search should take care of that.

![task 5](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/f56ab7216e2b15f827b8243e5243787bf9a2e640/Year-Of-The-Rabit_Walkthrough/yearoftherabit-img/5.%20its-popup-js-error.png)

Once it’s off, we’ll be taken to a page with a hint embedded within the video. Make sure to watch the entire video because you never know…. could be more clues at the end right??With the clue we got from the video, let’s dig deeper and see what’s hidden on web page.

6. We inspect this page and got a hidden directory in response header location.

![task 6](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/f56ab7216e2b15f827b8243e5243787bf9a2e640/Year-Of-The-Rabit_Walkthrough/yearoftherabit-img/6.%20we-inspect-this-phpfile-and-got-hidendirectory-in-response-header.png)





