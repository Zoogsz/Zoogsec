---
description: >-
  Credit to https://tcm-sec.com/ and https://github.com/jivoi for many of the
  tools in this section
---

# OSINT



## Huge List of Tools

{% embed url="https://github.com/jivoi/awesome-osint" %}

This repo is amazing ^ I have barely scratched the surface of the number of tools listed in there. Highly recommend checking it out.

## IP - Domain OSINT

Sometimes you want to get some information on an IP/Domain without actually scanning and drawing the attention to yourself. That's what these tools are for

{% embed url="https://exchange.xforce.ibmcloud.com/" %}
IP/Domain Lookup Tool
{% endembed %}

{% embed url="https://spur.us/" %}
Data on VPN/Proxys
{% endembed %}

{% embed url="https://urlscan.io/" %}
Want to see a sketchy website but not actually open the link? Bingo
{% endembed %}

{% embed url="https://www.shodan.io/" %}
Huge search engine for Internet Connected Devices
{% endembed %}

{% embed url="https://viewdns.info" %}
DNS info, self explanatory
{% endembed %}

{% embed url="https://crt.sh/" %}
SSL certificate search tool
{% endembed %}

## Email Address OSINT

#### Discovering Email Addresses

[hunter.io](http://hunter.io)&#x20;

* It will give you 50 to 100 free searchers per month and can be signed up to free with a google account

[phonebook.cz](http://phonebook.cz)

* does domains, emails, and URLs

[voilanobert.com](http://voilanobert.com)

* same as [hunter.io](http://hunter.io)



#### Scraping emails with LinkedInDumper

{% embed url="https://github.com/l4rm4nd/LinkedInDumper" %}

Python tool to scrape company emails from a linkedin page + fill in the blanks if given a set format. Works by using your `li_at` session cookie value which can be grabbed from the developer tools

Additional usage information here:

{% embed url="https://www.kitploit.com/2023/06/linkedindumper-tool-to-dump-company.html" %}

Verify Email Addresses

[tools.verifyemailaddress.io](http://tools.verifyemailaddress.io)

[email-checker.net/validate](http://email-checker.net/validate)

#### Verifying O365 Emails with UhOh365

{% embed url="https://github.com/Raikia/UhOh365" %}

Super useful tool for taking a list of emails and verifying if they are active or not. What is unique about this tool is it uses Microsoft's built-in Autodiscover API which is invisible to the person/company who owns said email address

<pre><code><strong>git clone https://github.com/Raikia/UhOh365.git
</strong><strong>cd UhOh365/
</strong><strong>
</strong>Usage: UhOh365.py [-h] [-v] [-t THREADS] [-o OUTPUT] file

positional arguments:
  file                  Input file containing one email per line

optional arguments:
  -h, --help            show this help message and exit
  -v, --verbose         Display each result as valid/invalid. By default only displays valid
  -s, --suffix	    Add a domain suffix to every input line from file (e.g: contoso.com)
  -t THREADS, --threads THREADS
                        Number of threads to run with. Default is 20
  -o OUTPUT, --output OUTPUT
                        Output file for valid emails only
  -n, --nossl           Turn off SSL verification. This can increase speed if
                        needed
  -p PROXY, --proxy PROXY
                        Specify a proxy to run this through (eg: 'http://127.0.0.1:8080')
</code></pre>

#### (alternative tool)

{% embed url="https://github.com/dievus/Oh365UserFinder" %}



#### Verifying Gmail accounts with geeMailUserFinder

{% embed url="https://github.com/dievus/geeMailUserFinder" %}

Where there is microsoft, there is google. Same concept as Oh365 but for gmail.

***

## Social media OSINT

#### Finding Usernames with WhatsMyName

{% embed url="https://github.com/WebBreacher/WhatsMyName" fullWidth="true" %}

WhatsMyName has been abandoned as a solo tool, it can however be integrated into multiple OSINT frameworks like Spiderfoot or visited via a web portal here

{% embed url="https://whatsmyname.app/" %}

#### Finding Usernames with Sherlock

{% embed url="https://github.com/sherlock-project/sherlock" %}

Another great tool for discovering usernames used across multiple sites. There are some false positives (some sites it pulls from will report a username for any request whether it exists or not) but overall a super easy to use tool.

```bash
python3 sherlock <username> #check one username
python3 sherlock <user1> <user2> <user3> #check multiple usernames
```



### Twitter OSINT (Or X depending on the day)

{% embed url="https://tinfoleak.com/#page-top" %}
Search for leaks related to that user, useful for basic account info
{% endembed %}

A really useful vector for social media OSINT is to leverage tools typically used for marketing. The tools listed below can be used to create a map of the users habits and interactions by using tools typically used to track account impression

{% embed url="https://socialbearing.com/" %}
Breaks down reach, impressions, tweets by sentiment sources etc.
{% endembed %}

{% embed url="https://www.twitonomy.com/" %}
Very similar to Social Bearing
{% endembed %}

{% embed url="https://spoonbill.io/" %}
Tracks account and user data changes - useful for long term targets
{% endembed %}



#### Twitter Dorking

Did you know you can treat the twitter search bar very similar to google dorking?&#x20;

<pre><code>we can use specific strings within the search ex: “nba draft pick”

<strong>from:&#x3C;username> - tweets from a user
</strong>
to:&#x3C;username> - see who is sending tweets at them/replying to them

@ symbol - anyone who tags the target

since: &#x3C;date> until:&#x3C;date> set timeframe

If you go to google maps and grab a specific geo coordinate

geocode: &#x3C;geo coordinate> , &#x3C;range> 
</code></pre>



#### Instagram OSINT

[instadip.co](https://instadp.io/)

* Lets you fullsize and download the image to try and hunt it down somewhere else

## Now for the super creepy parts

{% embed url="https://pimeyes.com/en" %}

Hands down the best facial reverse engineering tool out there. The results are highly truncated on the free tier but it is _super fun_ for scammers.



## Phone-sint (see what I did there)

Phone number OSINT is honestly a PITA. I am actively looking for suggestions for better free tools there. I refuse to "pay 99 cents to unlock this users full record".



## Credential Hunting

Such an important part of proper OSINT is hunting for leaked credentials. The "industry standard" tool for this right now is dehashed. This is a paid subscription, and the API credits (a need) are a couple extra bucks on top of the monthly subscription.&#x20;

{% embed url="https://github.com/hmaverickadams/DeHashed-API-Tool" %}
Super useful tool from the TCMsec guys for pulling from dehashed API.
{% endembed %}

```
usage: dehashed_parser.py [-h] [-a ADDRESS] [-e EMAIL] [-H HASHED_PASSWORD] [-i IP_ADDRESS] [-n NAME] [-p PASSWORD]
                 [-P PHONE_NUMBER] [-u USERNAME] [-v VIN] [-o OUTPUT] [-oS OUTPUT_SILENTLY] [-s SIZE]
                 [--only-passwords]

Query the DeHashed API

options:
  -h, --help            show this help message and exit
  -a ADDRESS, --address ADDRESS
                        Specify the address
  -e EMAIL, --email EMAIL
                        Specify the email
  -H HASHED_PASSWORD, --hashed_password HASHED_PASSWORD
                        Specify the hashed password
  -i IP_ADDRESS, --ip_address IP_ADDRESS
                        Specify the IP address
  -n NAME, --name NAME  Specify the name
  -p PASSWORD, --password PASSWORD
                        Specify the password
  -P PHONE_NUMBER, --phone_number PHONE_NUMBER
                        Specify the phone number
  -u USERNAME, --username USERNAME
                        Specify the username
  -v VIN, --vin VIN     Specify the VIN
  -o OUTPUT, --output OUTPUT
                        Outputs to CSV. A file name is required.
  -oS OUTPUT_SILENTLY, --output_silently OUTPUT_SILENTLY
                        Outputs to CSV silently. A file name is required.
  -s SIZE, --size SIZE  Specify the size, between 1 and 10000
  --only-passwords      Return only passwords
```

Outside of this, the most commonly used tool for your own "ethically sourced" databases is most likely breach parse. Its a super simple bash tool that is built for the old megabreach and COMB leaks.

{% embed url="https://github.com/hmaverickadams/breach-parse" %}

There are also some "specialty" parsers out there for some other breaches. I am not going to provide the magnet link too them however the hint I will give is "AntiPublic" and "Collection 1-5". Consider this a little OSINT practice and go figure that out.

{% embed url="https://github.com/philipperemy/3.7-billion-passwords-tools" %}
