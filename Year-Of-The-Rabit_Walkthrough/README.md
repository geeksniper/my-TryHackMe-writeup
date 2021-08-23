## Year Of The Rabbit_Walkthrough

`Year of the Rabbit is an easy level box on THM created by MuirlandOracle. I definitely had a lot of fun hacking this box, and it also has a cute surprise that I’m sure everyone will enjoy! It’s got a good mix of different CTF elements such as steganography, web app, and others.`

1. First do nmap scan using machine ip.We’re going to omit the -p flag so nmap will do a quicker scan of the most common ports, we should get some results back relatively quickly that includes most scan info.

![task 1](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/0262db8f58e8e50000e2720ff86536ff313761be/Year-Of-The-Rabit_Walkthrough/yearoftherabit-img/1.%20nmap-scan.png)

The results show us that it’s got a web service, FTP, and SSH enabled on the machine. Let’s start off by looking at the web page.

2. Looks like the default Apache2 landing page, nothing too exciting on the main page and the page source doesn’t reveal much either.

![task 1](https://github.com/geeksniper/my-TryHackMe-Writeups/blob/81d426b322701c188782f2914ba8166ae28b51a9/Year-Of-The-Rabit_Walkthrough/yearoftherabit-img/2.%20default-siteview.png)




