---
description: >-
  Brief Dump of useful scanning tools and useful scripts. Heavily network
  focused, web application scanning and testing will be covered in another
  section
---

# Scanning and Enumeration



## Useful NMAP Commands

```bash
nmap -p- -A -T4 -iL <input file> -oA <output file>

# -p- all ports
# all scripts


grep for <text> in <file> | cut on the delimiter "Space" and grab the 2nd field | sort unique + natural sort of (version) numbers within text | put & append into <file>
	
grep '/open/' ./nmap/s_u_live.gnmap | cut -d " " -f2 | sort -uV | tee -a ./nmap/hosts-live.txt
	
grep 'Host'

smb
grep '445/open/tcp//' ./nmap/s_u_live.gnmap | cut -d " " -f2 | sort -uV | tee -a ./nmap/hosts-smb.txt

https
grep '443/open/tcp//' ./nmap/s_u_live.gnmap | cut -d " " -f2 | sort -uV | tee -a ./nmap/hosts-ssl.txt

ssh
grep '22/open/tcp//' ./nmap/s_u_live.gnmap | cut -d " " -f2 | sort -uV | tee -a ./nmap/hosts-ssh.txt

Telnet
grep '23/open/tcp//' ./nmap/s_u_live.gnmap | cut -d " " -f2 | sort -uV | tee -a ./nmap/hosts-telnet.txt
++common ports + vulns

```



{% embed url="https://github.com/vulnersCom/nmap-vulners" %}
Vulners is included by default in MOST kali linux distributions. 50/50 on blackarch depending on the build
{% endembed %}

## Exploit Research

My go to search for quick wins is searching the reported technology using searchsploit.

{% embed url="https://github.com/Err0r-ICA/Searchsploit" %}

```bash
git clone https://www.github.com/Err0r-ICA/Searchsploit
cd Searchsploit 
bash install.sh
./Searchsploit

Usage
searchsploit <keyword>
```
