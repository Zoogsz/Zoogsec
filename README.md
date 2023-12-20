---
cover: >-
  https://preview.redd.it/cool-cyber-backgrounds-3840x2160-v0-9tyix97n4mea1.jpg?width=3840&format=pjpg&auto=webp&s=dd358af681ecb9657ba12d0d7611ac37f2409b7b
coverY: 0
---

# 💻 Intro

## Quick disclaimer

{% hint style="info" %}
**This is just a way for me to organize the resources I have found:**

I in no way advocate for the malicious use of any of these techniques, tools, and software. I am not a writer, many sections of this gitbook may be paraphrased or copied from other resources. I do my best to cite the original sources of this material but general rule of thumb. "If it seems like it is professionally written, I did not write it"
{% endhint %}

Huge shoutout to **HackTricks** at [https://book.hacktricks.xyz/welcome/readme](https://book.hacktricks.xyz/welcome/readme) and **TCM Security** at [https://tcm-sec.com/](https://tcm-sec.com/).

Many of the resources/techniques/etc listed in the following are from them, they are both objectively better resources then this.

#### Other quick notes

Many of these tools are written in python and the dependencies get messy quickly. I highly recommend setting up virtualenvs for each tool before installing the requirements.



```bash
## Installing virtualenv on Deb-Based systems

sudo apt update
sudo apt install virtualenv

## Installing virtualenv on Arch based systems

sudo pacman -Syu virtualenv

## Usage
## I normally will do this in the folder/repo that the project was installed in.
## BE CAREFUL DOING THIS AS A ROOT USER, running pip as root can cause permissions issues later down the line

cd <repo>
virtualenv <virtualenvName>
source <virtualenvName>/bin/activate
pip install -r <requirements>

```
