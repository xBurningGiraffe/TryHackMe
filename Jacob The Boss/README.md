# Jacob The Boss

## This is my first TryHackMe writeup. :]

### IP = 10.10.50.155
#### /etc/hosts 10.10.50.155    jacobtheboss.box

![jacobtheboss](https://user-images.githubusercontent.com/86382301/151686588-a83449ea-0cfe-45a2-933c-58702be650f2.png)

## Scanning/Enumeration

#### First things first; Nmap

nmap -sC -sV -Pn -T4 jacobtheboss.box -oN nmap.txt

Discovered open port 4446/tcp on 10.10.50.155   
Discovered open port 1099/tcp on 10.10.50.155   
Discovered open port 4445/tcp on 10.10.50.155   
Discovered open port 1098/tcp on 10.10.50.155   
Discovered open port 8009/tcp on 10.10.50.155   
Discovered open port 1090/tcp on 10.10.50.155   
Discovered open port 8083/tcp on 10.10.50.155   
Discovered open port 80/tcp on 10.10.50.155   
Discovered open port 111/tcp on 10.10.50.155   
Discovered open port 22/tcp on 10.10.50.155   
Discovered open port 8080/tcp on 10.10.50.155   
Discovered open port 3306/tcp on 10.10.50.155   
Discovered open port 4444/tcp on 10.10.50.155   
Completed SYN Stealth Scan at 18:33, 29.28s elapsed (1000 total ports)   
Nmap scan report for jacobtheboss.box (10.10.50.155)   
Host is up, received user-set (0.21s latency).   
Scanned at 2022-01-29 18:32:56 CST for 29s   
Not shown: 987 closed tcp ports (reset)   
PORT     STATE SERVICE       REASON   
22/tcp   open  ssh           syn-ack ttl 61   
80/tcp   open  http          syn-ack ttl 61   
111/tcp  open  rpcbind       syn-ack ttl 61   
1090/tcp open  ff-fms        syn-ack ttl 61   
1098/tcp open  rmiactivation syn-ack ttl 61   
1099/tcp open  rmiregistry   syn-ack ttl 61   
3306/tcp open  mysql         syn-ack ttl 61   
4444/tcp open  krb524        syn-ack ttl 61   
4445/tcp open  upnotifyp     syn-ack ttl 61   
4446/tcp open  n1-fwp        syn-ack ttl 61   
8009/tcp open  ajp13         syn-ack ttl 61   
8080/tcp open  http-proxy    syn-ack ttl 61   
8083/tcp open  us-srv        syn-ack ttl 61  
 
 

22/tcp   open  ssh         syn-ack ttl 61 OpenSSH 7.4 (protocol 2.0)   
| ssh-hostkey:    
|   2048 82:ca:13:6e:d9:63:c0:5f:4a:23:a5:a5:a5:10:3c:7f (RSA)   
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDOLOk6ktnJtucoDmXmBrc4H4gGe5Cybdy3jh1VZg+CYg+sZbYXzGi2/JO45cRqYd2NFIq7l+oTsjFgh76qAayKMU4D3+gKaC+U2VL93nCU1SywzvZLLc
 
8MEy7mTHflOm4kZCmycgtJO4tfUhuH64yEP+lv3ENFeH5jgyJcGABF/p44MMSwnvpaLMfOuEGuEhKMPA4c+XAiS3J+sErUbpx6ragGGJAKTpww+arDy11slMsyJgjN6GUjlR0y+P0E4/NsrNHe86GKXJ1G4b
 
fKEdKOPeTZ+wZMNFDCVNLPHLWUBIgWNQHIgRcXiBvPAvIrrt8gV/+td9C74Bsj0VqEEJnP   
|   256 a4:6e:d2:5d:0d:36:2e:73:2f:1d:52:9c:e5:8a:7b:04 (ECDSA)   
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBNUtPCeXKNaq6WZlT3PxbZbQmka1bb5I+yBRhUb5tzmf2GEmdDOk6R7MSUlEtzGzQ4GjAWFZG3q7ZcBahg
 
8ur8A=   
|   256 6f:54:a6:5e:ba:5b:ad:cc:87:ee:d3:a8:d5:e0:aa:2a (ED25519)   
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIJI3bQUWzwhk0iJYl+gGn09NgvRLtN4vJ4DG6SrE7/Hb   
80/tcp   open  http        syn-ack ttl 61 Apache httpd 2.4.6 ((CentOS) PHP/7.3.20)   
|_http-title: My first blog   
| http-methods:    
|_  Supported Methods: GET HEAD POST OPTIONS   
|_http-server-header: Apache/2.4.6 (CentOS) PHP/7.3.20   
111/tcp  open  rpcbind     syn-ack ttl 61 2-4 (RPC #100000)   
| rpcinfo:    
|   program version    port/proto  service   
|   100000  2,3,4        111/tcp   rpcbind   
|   100000  2,3,4        111/udp   rpcbind   
|   100000  3,4          111/tcp6  rpcbind   
|_  100000  3,4          111/udp6  rpcbind   
1090/tcp open  java-rmi    syn-ack ttl 61 Java RMI   
|_rmi-dumpregistry: ERROR: Script execution failed (use -d to debug)   
1098/tcp open  java-rmi    syn-ack ttl 61 Java RMI   
1099/tcp open  java-object syn-ack ttl 61 Java Object Serialization   
| fingerprint-strings:    
|   NULL:    
|     java.rmi.MarshalledObject|   
|     hash[   
|     locBytest   
|     objBytesq   
|     http://jacobtheboss.box:8083/q   
|     org.jnp.server.NamingServer_Stub   
|     java.rmi.server.RemoteStub   
|     java.rmi.server.RemoteObject   
|     xpw;   
|     UnicastRef2   
|_    jacobtheboss.box   
3306/tcp open  mysql       syn-ack ttl 61 MariaDB (unauthorized)   
4444/tcp open  java-rmi    syn-ack ttl 61 Java RMI   
4445/tcp open  java-object syn-ack ttl 61 Java Object Serialization   
4446/tcp open  java-object syn-ack ttl 61 Java Object Serialization   
8009/tcp open  ajp13       syn-ack ttl 61 Apache Jserv (Protocol v1.3)   
| ajp-methods:    
|   Supported methods: GET HEAD POST PUT DELETE TRACE OPTIONS   
|   Potentially risky methods: PUT DELETE TRACE   
|_  See https://nmap.org/nsedoc/scripts/ajp-methods.html   
8080/tcp open  http        syn-ack ttl 61 Apache Tomcat/Coyote JSP engine 1.1   
|_http-server-header: Apache-Coyote/1.1   
|_http-favicon: Unknown favicon MD5: 799F70B71314A7508326D1D2F68F7519   
|_http-title: Welcome to JBoss&trade;   
| http-methods:    
|   Supported Methods: GET HEAD POST PUT DELETE TRACE OPTIONS   
|_  Potentially risky methods: PUT DELETE TRACE   
8083/tcp open  http        syn-ack ttl 61 JBoss service httpd   
|_http-title: Site doesn't have a title (text/html).   
3 services unrecognized despite returning data. If you know the service/version, please submit the following fingerprints at https://nmap.org/cgi-bin/submit
 
.cgi?new-service :   
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============   
SF-Port1099-TCP:V=7.92%I=7%D=1/29%Time=61F5DCFC%P=x86_64-pc-linux-gnu%r(NU   
SF:LL,16F,"\xac\xed\0\x05sr\0\x19java\.rmi\.MarshalledObject\|\xbd\x1e\x97   
SF:\xedc\xfc>\x02\0\x03I\0\x04hash\[\0\x08locBytest\0\x02\[B\[\0\x08objByt   
SF:esq\0~\0\x01xp\xd1\x84\x9c\xaaur\0\x02\[B\xac\xf3\x17\xf8\x06\x08T\xe0\   
SF:x02\0\0xp\0\0\0\.\xac\xed\0\x05t\0\x1dhttp://jacobtheboss\.box:8083/q\0   
SF:~\0\0q\0~\0\0uq\0~\0\x03\0\0\0\xc7\xac\xed\0\x05sr\0\x20org\.jnp\.serve   
SF:r\.NamingServer_Stub\0\0\0\0\0\0\0\x02\x02\0\0xr\0\x1ajava\.rmi\.server   
SF:\.RemoteStub\xe9\xfe\xdc\xc9\x8b\xe1e\x1a\x02\0\0xr\0\x1cjava\.rmi\.ser   
SF:ver\.RemoteObject\xd3a\xb4\x91\x0ca3\x1e\x03\0\0xpw;\0\x0bUnicastRef2\0   
SF:\0\x10jacobtheboss\.box\0\0\x04J\0\0\0\0\0\0\0\0\x17\x1b3\xc4\0\0\x01~\   
SF:xa8d}\xae\x80\0\0x");   
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============   
SF-Port4445-TCP:V=7.92%I=7%D=1/29%Time=61F5DD01%P=x86_64-pc-linux-gnu%r(NU   
SF:LL,4,"\xac\xed\0\x05");   
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============   
SF-Port4446-TCP:V=7.92%I=7%D=1/29%Time=61F5DD01%P=x86_64-pc-linux-gnu%r(NU   
SF:LL,4,"\xac\xed\0\x05"); 
┌─[chase@xBurningGiraffe]─[~/Documents/THM/jacobtheboss] 
└──╼ $sudo nmap -sC -sV -Pn -T4 jacobtheboss.box -oN nmap.txt 
Starting Nmap 7.92 ( https://nmap.org ) at 2022-01-29 21:13 CST 
Nmap scan report for jacobtheboss.box (10.10.50.155) 
Host is up (0.62s latency). 
Not shown: 987 closed tcp ports (reset) 
PORT     STATE SERVICE     VERSION 
22/tcp   open  ssh         OpenSSH 7.4 (protocol 2.0) 
| ssh-hostkey:  
|   2048 82:ca:13:6e:d9:63:c0:5f:4a:23:a5:a5:a5:10:3c:7f (RSA) 
|   256 a4:6e:d2:5d:0d:36:2e:73:2f:1d:52:9c:e5:8a:7b:04 (ECDSA) 
|_  256 6f:54:a6:5e:ba:5b:ad:cc:87:ee:d3:a8:d5:e0:aa:2a (ED25519) 
80/tcp   open  http        Apache httpd 2.4.6 ((CentOS) PHP/7.3.20) 
|_http-server-header: Apache/2.4.6 (CentOS) PHP/7.3.20 
|_http-title: My first blog 
111/tcp  open  rpcbind     2-4 (RPC #100000) 
| rpcinfo:  
|   program version    port/proto  service 
|   100000  2,3,4        111/tcp   rpcbind 
|   100000  2,3,4        111/udp   rpcbind 
|   100000  3,4          111/tcp6  rpcbind 
|_  100000  3,4          111/udp6  rpcbind 
1090/tcp open  java-rmi    Java RMI 
|_rmi-dumpregistry: ERROR: Script execution failed (use -d to debug) 
1098/tcp open  java-rmi    Java RMI 
1099/tcp open  java-object Java Object Serialization 
| fingerprint-strings:  
|   NULL:  
|     java.rmi.MarshalledObject| 
|     hash[ 
|     locBytest 
|     objBytesq 
|     http://jacobtheboss.box:8083/q 
|     org.jnp.server.NamingServer_Stub 
|     java.rmi.server.RemoteStub 
|     java.rmi.server.RemoteObject 
|     xpw; 
|     UnicastRef2 
|_    jacobtheboss.box 
3306/tcp open  mysql       MariaDB (unauthorized) 
4444/tcp open  java-rmi    Java RMI 
4445/tcp open  java-object Java Object Serialization 
4446/tcp open  java-object Java Object Serialization 
8009/tcp open  ajp13       Apache Jserv (Protocol v1.3) 
| ajp-methods:  
|   Supported methods: GET HEAD POST PUT DELETE TRACE OPTIONS 
|   Potentially risky methods: PUT DELETE TRACE 
|_  See https://nmap.org/nsedoc/scripts/ajp-methods.html 
8080/tcp open  http        Apache Tomcat/Coyote JSP engine 1.1 
|_http-title: Welcome to JBoss&trade; 
| http-methods:  
|_  Potentially risky methods: PUT DELETE TRACE 
|_http-server-header: Apache-Coyote/1.1 
8083/tcp open  http        JBoss service httpd 
|_http-title: Site doesn't have a title (text/html). 
3 services unrecognized despite returning data. If you know the service/version, please submit the following fingerprints at https://nmap.org/cgi-bin/submit
.cgi?new-service : 
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)============== 
SF-Port1099-TCP:V=7.92%I=7%D=1/29%Time=61F60265%P=x86_64-pc-linux-gnu%r(NU 
SF:LL,16F,"\xac\xed\0\x05sr\0\x19java\.rmi\.MarshalledObject\|\xbd\x1e\x97 
SF:\xedc\xfc>\x02\0\x03I\0\x04hash\[\0\x08locBytest\0\x02\[B\[\0\x08objByt 
SF:esq\0~\0\x01xp\xd1\x84\x9c\xaaur\0\x02\[B\xac\xf3\x17\xf8\x06\x08T\xe0\ 
SF:x02\0\0xp\0\0\0\.\xac\xed\0\x05t\0\x1dhttp://jacobtheboss\.box:8083/q\0 
SF:~\0\0q\0~\0\0uq\0~\0\x03\0\0\0\xc7\xac\xed\0\x05sr\0\x20org\.jnp\.serve 
SF:r\.NamingServer_Stub\0\0\0\0\0\0\0\x02\x02\0\0xr\0\x1ajava\.rmi\.server 
SF:\.RemoteStub\xe9\xfe\xdc\xc9\x8b\xe1e\x1a\x02\0\0xr\0\x1cjava\.rmi\.ser 
SF:ver\.RemoteObject\xd3a\xb4\x91\x0ca3\x1e\x03\0\0xpw;\0\x0bUnicastRef2\0 
SF:\0\x10jacobtheboss\.box\0\0\x04J\0\0\0\0\0\0\0\0\x17\x1b3\xc4\0\0\x01~\ 
SF:xa8d}\xae\x80\0\0x"); 
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)============== 
SF-Port4445-TCP:V=7.92%I=7%D=1/29%Time=61F6026B%P=x86_64-pc-linux-gnu%r(NU 
SF:LL,4,"\xac\xed\0\x05"); 
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)============== 
SF-Port4446-TCP:V=7.92%I=7%D=1/29%Time=61F6026B%P=x86_64-pc-linux-gnu%r(NU 
SF:LL,4,"\xac\xed\0\x05");

## Starting with http://jacobtheboss.box:80 first

![blog](https://user-images.githubusercontent.com/86382301/151686721-c580ac58-5f70-41f5-b7ae-bc4c0989fe52.png)

### Wappalyzer gives plenty of info about the target's web server

![wapp](https://user-images.githubusercontent.com/86382301/151686759-95c5ee3e-0b11-4010-88ca-772ab66f507c.png)

## I decided to run Gobuster while checking out the web pages

sudo gobuster dir --url http://jacobtheboss.box -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt 

## Gobuster provided the directory for the blog's admin login page

http://jacobtheboss.box/admin/auth.php

![dotclear](https://user-images.githubusercontent.com/86382301/151686846-e269f4ab-62bc-4c33-a5c8-5d6dc65f1e30.png)

### Before going further with Hydra to brute-force this login page, I pivoted to enumerate port 8080

## http://jacobtheboss.box:8080


![jboss](https://user-images.githubusercontent.com/86382301/151686886-47f728f1-e9dd-411a-9d3a-44a5b46a111d.png)

## This is definitely a promising attack vector (because JBoss lol). 

# Exploitation

## The JBoss path seems promising, but before going down that path I decided to trigger Hydra on the Dotclear admin page

sudo hydra -L /usr/share/wordlists/Usernames/Names/names.txt -P /usr/share/wordlists/rockyou.txt 10.10.50.155 http-post-form "/admin/auth.php:user_id=jacob&user_pwd=^PASS^:Wrong username or password"

## While that was running, I used searchsploit to check for JBoss vulnerabilities. After skimming the results, I figured I'd do a quick Google search and found Jexboss

![jex](https://user-images.githubusercontent.com/86382301/151687108-6d8533c4-6471-4161-91a9-b307f9259292.png)

### Running the Jexboss python script against http://jacobtheboss.box:8080 found the web and JMX consoles to be vulnerable, as well as the JMXInvokerServlet. 

![jex2](https://user-images.githubusercontent.com/86382301/151687225-ed1bca74-de33-44a2-bbd9-092470a2893e.png)

## Success! I've gotten a shell as the user named jacob, so I changed into the /home/jacob directory and got the user.txt flag. Then, I went back to my running Hydra process and killed it. 

# Privilege Escalation

## After changing into the /tmp directory, I downloaded linpeas from a simple python web server hosted by my machine and ran it.

### Before I ran linpeas, I decided to test the pwnkit PoC that was recently released (CVE-2021-4034), which I compiled on my host machine then pulled it as I did linpeas.
### The pwnkit PoC got me a root shell! Since it was a bit simple, I changed back to the jacob user and ran linpeas afterward to find another exploit method.  I noticed that pingsys had SUID, so I did a search
### for exploits, which led me to "pingsys 'localhost; /bin/sh'. This method also gave me root shell.

## While this is my first writeup, I plan to do more going forward. (as well as get more screenshots of my process). Thanks for looking!







