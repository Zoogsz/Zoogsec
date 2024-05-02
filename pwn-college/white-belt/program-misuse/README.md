---
description: >-
  All credit for these notes go to the wonderful lecturer's that host
  pwn.college
---

# Program Misuse

First things first lets define some fundamental aspects of the Linux operating system.



#### Environment Variables

Environment variables are a set of Key/Value pairs passed into every process when it is launched.

Critical variables

* `PATH`: a list of directories to search for programs in
* `PWD`: the current working directory
* `HOME`: The path to your home directory
* `HOSTNAME`: name of your system

You can print environment variables with the `env` command and set them with shell syntax.

#### Symbolic (Soft links)

* Type of file that references another file. Created with `ln -s` (-s stands for symbolic)
* symbolic links to relative paths are relative to the directory containing the link

#### Hard Links

* Created by ln without the -s argument reference the original file directly. A hard link is an equally valid reference to the original file.

#### Pipes

1. Unnamed pipes channel information between processes. Most commonly used to direct data from one command to another
2. Named pipes, also known as FIFO's created using the `mkfifo` command. Also used to help facilitate data flow in certain situations.

#### I/O Redirection (This will be referenced much heavier in following notes)

```
<infile: redirect in_file into the command's input
>out_file: redirect the command's output into out_file overwritting it
>>out_file: redirect output into out_file appending to it.
2>error_file: redirect the command's errors into error_file overwriting it
2>>error_file: redirect the command's errors into error_file, appending to it.
```

## Privilege Escalation

<figure><img src="../../../.gitbook/assets/Pasted image 20240424223906.png" alt=""><figcaption><p>Linux Permissions Model (From pwn.college)</p></figcaption></figure>

UID 0 is the Linux admin user, root. You need root for:

* Installing software
* Loading device drivers
* Shutting down, rebooting
* Changing system-wide settings

But if we are UID 1000 how do we become 0?

One method is to elevate your privileges by running an suid binary. These work using a few permission bits we havent talked about. The (Set)UID bit, and (SET)GID bit.

SUID is a bit in the Linux permissions model:

* SUID: execute with the eUID of the file owner rather than the parent process
* SGID: execute with the eGID of the file owner rather than the parent process
* Sticky: used for shared directories to limit file removal to file owners.

Common examples of SUID binaries: `sudo, su, newgrp`

So what is the effective UID? There are 3 different type of user and group IDs

1. Effective (eUID, eGID): the UID/GID used for most access checks.
2. Real (UID,GID): the "real" UID (or GID) of the process owner, used for things such as signal checks
3. Saved: a UID/GID that your process could switch its eUID/eGID to. Used for temporarily dropping privileges
   1. Can lead to vulnerabilities if your unprived settings can reset to a prived setting.

eUID 0 is powerful. By default you can

* Open any file
  * Including things in the special /proc filesystem (dump memory of a file)
  * And device-backed files
* Execute any program
* Assume any other UID or GID
* Debug any program
