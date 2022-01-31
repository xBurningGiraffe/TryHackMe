![overpass1](https://user-images.githubusercontent.com/86382301/151735356-f4badbc9-e866-455f-86b8-9f887d4c7b4f.png)

https://tryhackme.com

### Objectives:

![overpass2](https://user-images.githubusercontent.com/86382301/151735374-361b7d00-a8d4-42f3-b3a5-8db85559d69f.png)

## IP = 10.10.67.235 

## Scanning/Enumeration 

### Nmap  

#### To avoid a massive amount of nmap output for this write up, I figured I'd start without the –sC trigger on my first scan 

![overpass3](https://user-images.githubusercontent.com/86382301/151735427-47779142-8c7c-419b-8fa3-9243a9d009a4.png)

### Interesting....port 80 suggests a Golang web server with possibly an InfluxDB API to query its data.  

### To be thorough, I ran another syn scan to check all the ports. Why? Because enumeration. However, it found no additional ports. So ran nmap with –sC on ports 22 and 80 
 
 ![overpass4](https://user-images.githubusercontent.com/86382301/151735454-ee670427-e039-4581-a303-6656e79789dd.png)

## Lets check out the web page

![overpass5](https://user-images.githubusercontent.com/86382301/151735477-9c0ecb23-8112-4016-ad6a-742ad9eb4e50.png)

### After clicking around the site, there's not much to it other than the Downloads page having links to different builds of the "Overpass" password manager. However, I did take note of the names listed in the "About Us" page, in case they came in handy later on. 

![overpass6](https://user-images.githubusercontent.com/86382301/151735563-3ebec9b7-97e5-4262-af34-d7da717d3fed.png)

### Alas, on to Gobuster 

### Gobuster 

### Gobuster gave me a few results pretty quickly, one of them being the /admin login page  

![overpass7](https://user-images.githubusercontent.com/86382301/151735624-626cb892-79dc-4aca-9a9f-125767b92de8.png)

## Initial access/Exploitation 

### I tried a few standard logins on the /admin page, but no dice. I jumped into Firefox's web dev tools, and checked out how the page was sending its request. Before I could set off BurpSuite or hydra to brute-force the login, I reloaded the page via the dev tools and got this:


![overpass8](https://user-images.githubusercontent.com/86382301/151735807-633c5ada-146b-45d0-bed6-081226459e82.png)

### This page also included an RSA Private Key, which I've redacted it for the sake of the challenge. Once I've gotten the RSA key, we need to get its hash and crack it, which I used John the Ripper to do. 


![overpass9](https://user-images.githubusercontent.com/86382301/151735836-941dcebc-e260-4916-84ba-456e1bd03d66.png)

![overpass10](https://user-images.githubusercontent.com/86382301/151735847-f4c166b7-89cc-4357-9cbf-031b6f4ba8df.png)

### Cool, so now I've gotten credentials for initial access to the target. I log in to the target and grab the first flag for our first objective. 

![overpass11](https://user-images.githubusercontent.com/86382301/151735863-1d1f7951-9ee1-48a6-acc2-fb7d4e2fa08f.png)

# Privilege Escalation 

### In the same folder where I found our first objective, there's a text file called 'todo.txt,' so I checked it out.  

![overpass12](https://user-images.githubusercontent.com/86382301/151735894-8ec42a7e-79f2-4bcb-854c-f41e3e20f3be.png)

### This tells me that there's an automated build script on the machine, which could possibly be exploited to gain root access.

### I check my sudo privileges, but no dice there. Next, I check crontab to see if there's something related to the automated script mentioned in the todo.txt file mentioned previously. 

![overpass13](https://user-images.githubusercontent.com/86382301/151735923-ec5d0151-7390-4666-bde8-9c2fddefcccb.png)

### First, I ran linpeas and put the findings in the /tmp folder on the target system. Before reviewing the results, I checked to see if I could edit the hosts file to point the target at my own machine.

![overpass14](https://user-images.githubusercontent.com/86382301/151735973-a8a87b9b-5e9d-4e3b-adea-4170cf83d456.png)

### Bingo. With the target pointing at my machine's IP, I can have it download a script to spawn a reverse shell with root access.

![overpass18](https://user-images.githubusercontent.com/86382301/151736111-9c2ff8bf-0160-4539-bfb0-1bb2097595e1.png)

### Within a folder labeled "www" , I created the directories to match that’s listed in the crontab script, then created the reverse shell bash script within the 'src' directory, and changed its permissions to be executable.

![overpass15](https://user-images.githubusercontent.com/86382301/151736140-f03355d6-f28d-466e-97c4-58d5145745d7.png)

### Lastly, its time to get that sweet root access. I started a simple Python web server over port 80 from within the 'www' folder I had created, then spawned a netcat session on port 5555.

![overpass16](https://user-images.githubusercontent.com/86382301/151736167-11eb59a0-81e9-4661-b385-11aa9e5e8dfc.png)

### Boop, we are root! I collected the root flag to complete the last objective.

![overpass17](https://user-images.githubusercontent.com/86382301/151736195-f0e1677e-76b3-48bb-98ba-824b234bd340.png)

## Final 

### This was a fun, simple challenge that I enjoyed. I chose it specifically to make this write up (which is my second write up now) so I could continue improving my notetaking skills (and taking hella screenshots) 

 
 
 ## Happy Hacking! 










































