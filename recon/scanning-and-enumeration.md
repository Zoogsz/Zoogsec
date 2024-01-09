---
description: >-
  Brief Dump of useful scanning tools and useful scripts. Heavily network
  focused, web application scanning and testing will be covered in another
  section
---

# Scanning and Enumeration

## Useful NMAP Commands

<pre class="language-bash"><code class="lang-bash">nmap -p- -A -T4 -iL &#x3C;input file> -oA &#x3C;output file>

# -p- all ports
# all scripts


grep for &#x3C;text> in &#x3C;file> | cut on the delimiter "Space" and grab the 2nd field | sort unique + natural sort of (version) numbers within text | put &#x26; append into &#x3C;file>
	
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


# NMAP
<strong># Just for LDAP Account managers
</strong>nmap 10.20.10.4 -p80,443,389,636 -sC -sV -Pn -n

# Turn a file of CIDR IP's into a full IP list
nmap -sL -n -iL internalTargets.txt | grep "Nmap scan report" | awk '{print $NF}'

</code></pre>



{% embed url="https://github.com/vulnersCom/nmap-vulners" %}
Vulners is included by default in MOST kali linux distributions. 50/50 on blackarch depending on the build
{% endembed %}



## RustScan

{% embed url="https://github.com/RustScan/RustScan" %}
Cause I wanna go fast
{% endembed %}

### Multiple IP Scanning

You can scan multiple IPs using a comma separated list like so:

```
rustscan -a 127.0.0.1,0.0.0.0
```

### Host Scanning

RustScan can also scan hosts, like so:

```
➜ rustscan -a www.google.com, 127.0.0.1
Open 216.58.210.36:1
Open 216.58.210.36:80
Open 216.58.210.36:443
Open 127.0.0.1:53
Open 127.0.0.1:631
```

### CIDR support

RustScan supports CIDR:

```
➜ rustscan -a 192.168.0.0/30
```

### Hosts file as input

The file is a new line separated list of IPs / Hosts to scan:

**hosts.txt**

```
192.168.0.1
192.168.0.2
google.com
192.168.0.0/30
127.0.0.1
```

The argument is:

```
rustscan -a 'hosts.txt'
```

### Individual Port Scanning

RustScan can scan individual ports, like so:

```
➜ rustscan -a 127.0.0.1 -p 53
53
```

### Multiple selected port scanning

You can input a comma separated list of ports to scan:

```
➜ rustscan -a 127.0.0.1 -p 53,80,121,65535
53
```

### Ranges of ports

To scan a range of ports:

To run:

```
➜ rustscan -a 127.0.0.1 --range 1-1000    
53,631
```

### Adjusting the Nmap arguments

RustScan, at the moment, runs Nmap by default.

You can adjust the arguments like so:

```
rustscan -a 127.0.0.1 -- -A -sC
```

To run:

```
nmap -Pn -vvv -p $PORTS -A -sC 127.0.0
```

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

## Random Commands

These are a bunch of bash one liners I use to organize scanning results and format them into something useful



Cut just the usernames from dehashed api results

```
awk -F'@' '{print $1}' your_file.csv | cut -d',' -f1 | sort -u

```

Pull passwords from dehashed API results

```
awk -F',' '{print $7}' your_file.txt

```

Cut out the usernames from linkedin dumper results

```
awk -F';' '{print $3}' your_file.csv | cut -d'@' -f1 | sort -u

```

Cut out valid usernames from kerberos\_enumusers

```
grep '^\[+\]' your_file.txt | awk '{print $5}' | cut -d'"' -f2 | sort -u
```

Combine 2 files with only the unique lines

```
cat file1.txt file2.txt | sort -u > combined_users.txt
```

Turn a file of CIDR IP's into a full IP list
