---
description: Get ready for a lot of tool troubleshooting
---

# Attacking VOIP - Intro

## Sources and additional research



{% embed url="https://medium.com/vartai-security/practical-voip-penetration-testing-a1791602e1b4" %}
The beginning explanation sourced heavily from here
{% endembed %}

{% embed url="https://book.hacktricks.xyz/network-services-pentesting/pentesting-voip" %}

First a little explanation about VOIP and the SIP protocol.

SIP is an application layer protocol using UDP/TCP over port 5060. TLS encrypted traffic occurs on port 5061. Initially this default use of unencrypted traffic opens up to a handful of MITM attacks, but that will be covered later.



Lets look at how this protocol works

<figure><img src="../.gitbook/assets/1 T-7EYkavSdNgTvwtyx1ulw-1.gif" alt=""><figcaption><p>SIP Protocol</p></figcaption></figure>

The SIP interaction typically goes like this

1. Sender initiates via INVITE request
2. Receiver sends back a 100 (trying) request
3. Sender starts rining sending a 180 (ringing)
4. Receiver picks up the phone and a 200 is sent (OK response)
5. ACK is sent by initator
6. Call begins
7. BYE request sent to end the call.



So that covers the uses of 4 of the 7 protocols, what about the others?

* REGISTER - Registering the user against the SIP server
* OPTIONS - Shows the options the caller has (this will be important)
* REFER - Shows the receiver needs to communicate through a 3rd party by the info attached to the request



## Initial scanning and enumeration

Nmap using the -A (all detection's and scripts) flag will shoot out an OPTIONS request to show what of these protocols can be accessed.

{% hint style="info" %}
Do NOT take this at face value. The Viproy toolkit built into Metasploit does the same thing, just because these options are AVAILABLE externally does NOT mean that they are accessible. The report from options will not tell you if proxy authentication is required to use any of these protocols.
{% endhint %}

Extra Network Enumeration&#x20;

* The PBX could also be exposing other network services such as:&#x20;
  * 69/UDP (TFTP): Firmware updates&#x20;
  * 80 (HTTP) / 443 (HTTPS): To manage the device from the web&#x20;
  * 389 (LDAP): Alternative to store the users information&#x20;
  * 3306 (MySQL): MySQL database&#x20;
  * 5038 (Manager): Allows to use Asterisk from other platforms&#x20;
  * 5222 (XMPP): Messages using Jabber&#x20;
  * 5432 (PostgreSQL): PostgreSQL database And others...



So how do we find out what we can _actually_ use as an attack vector?



### Sippts

{% embed url="https://github.com/Pepelux/sippts" %}
The only SIP tools I have found that have been updated since 2018
{% endembed %}

```bash
# Quick install dump
# USE PYENVS - This tool uses some old libraries that will 100% cause conflicts
# Or problems in the future, you can see how to do this in Intro


git clone https://github.com/Pepelux/sippts.git
cd sippts/
# Do your pyenv stuff here
pip install -r requirements.txt
```

#### SIPscan

Sipscan works sending and waiting well-formed SIP packages. It is posible to scan several IP addresses or network ranges, over UDP, TCP or TLS.

```bash
# Basic Usage
# -p all says try with all protocols
# -ua sippts by default uses a useragent called pplsip which is typically blocked. -ua lets you change this

python sipscan.py -i <ip Address> -p all -r 5060-5080 -ua <User Agent>
```

There is a large number of other flags that pass specific names, users, domains, threads used etc but this is a basic one liner to get started.



### SipVicious

{% embed url="https://github.com/EnableSecurity/sipvicious" %}
Another solid toolkit
{% endembed %}

{% embed url="https://github.com/enablesecurity/sipvicious/wiki" %}
Wiki for SipVicious
{% endembed %}

```bash
# This one is installed by default on kali or can be installed
sudo apt install sipvicious

# or
## USE YOUR VENVS
git clone https://github.com/EnableSecurity/sipvicious.git
cd sipvicious/
python setup.py install
```

#### Svmap

Another scanning tool for SIP protocols, this allows us to choose what type of SIP request we would like to enumerate with rather then just what network protocol

```
## Example usage

# Use --fp to fingerprint the services
svmap 10.10.0.0/24 -p 5060-5070 [--fp]
```







### Methods enumeration with sipenumerate

