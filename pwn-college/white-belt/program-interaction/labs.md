---
description: >-
  I did start to devolve back into an animalistic state more then once here.
  Pardon my Fr*nch
---

# Labs

<pre data-overflow="wrap" data-full-width="false"><code>Level 1: was just checking for a standard bash shell so dropped it in the VDI instead

pwn.college{QwOjdbdP8ERN3bFd62AxsTsMF0I.dFDL3QzMzUzW}

------------------------------------------------------------
Level 5:
WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : bash
- the challenge will check that input is redirected from a specific file path : /tmp/cwxhwa
- the challenge will check for a hardcoded password over stdin : hxhxyvux


hacker@program-interaction~level5:/challenge$ touch /tmp/cwxhwa
hacker@program-interaction~level5:/challenge$ echo "hxhxyvux"
hxhxyvux
hacker@program-interaction~level5:/challenge$ echo "hxhxyvux" > /tmp/cwxhwa 
hacker@program-interaction~level5:/challenge$ ./embryoio_level5 &#x3C;/tmp/cwxhwa

------------------------------------------------------------
Level 6:
WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : bash
- the challenge will check that output is redirected to a specific file path : /tmp/tzdetd

hacker@program-interaction~level6:/challenge$ ./embryoio_level6 > /tmp/tzdetd
hacker@program-interaction~level6:/challenge$ cat /tmp/tzdetd 
pwn.college{87tQdxvAPYY3cawKawo1e0hxZHH.dZDL3QzMzUzW}
------------------------------------------------------------

Level 7:
WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : bash
- the challenge will check that the environment is empty (except LC_CTYPE, which is impossible to get rid of in some cases)

hacker@program-interaction~level7:/challenge$ env -i embryoio_level7 

pwn.college{IkmOxw8HJek1qlb5lQ_S_es-mWQ.ddDL3QzMzUzW}
------------------------------------------------------------

Level 8:

WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : shellscript

#!/bin/bash

# Path to the ELF file
ELF_FILE="/challenge/embryoio_level8"

# Check if the file exists
if [ ! -f "$ELF_FILE" ]; then
    echo "Error: ELF file not found at $ELF_FILE"
    exit 1
fi

# Execute the ELF file
"$ELF_FILE"

pwn.college{Mv0-JdPP7wIALVJzvYU1WOI6njj.dhDL3QzMzUzW}
------------------------------------------------------------

Level 9:

WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : shellscript
- the challenge will check for a hardcoded password over stdin : uajzvqia



#!/bin/bash

# Path to the ELF file
ELF_FILE="/challenge/embryoio_level9"

# Check if the file exists
if [ ! -f "$ELF_FILE" ]; then
    echo "Error: ELF file not found at $ELF_FILE"
    exit 1
fi

# Execute the ELF file with stdin "uajzvqia"
echo "uajzvqia" | "$ELF_FILE"

------------------------------------------------------------
Level 10:
hacker@program-interaction~level10:/challenge$ ./embryoio_level10 
WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : shellscript
- the challenge will check that argv[NUM] holds value VALUE (listed to the right as NUM:VALUE) : 1:zbzmaqopdr

#!/bin/bash

# Path to the ELF file
ELF_FILE="/challenge/embryoio_level10"

# Check if the file exists
if [ ! -f "$ELF_FILE" ]; then
    echo "Error: ELF file not found at $ELF_FILE"
    exit 1
fi

# Execute the ELF file with stdin "uajzvqia"
echo "uajzvqia" | "$ELF_FILE" "zbzmaqopdr"


pwn.college{stPmuqD6vHAy8dfrro4LzV9X6Hf.QXwEDL3QzMzUzW}
------------------------------------------------------------
Level 11:

hacker@program-interaction~level11:/challenge$ ./embryoio_level11 
WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : shellscript
- the challenge will check that env[KEY] holds value VALUE (listed to the right as KEY:VALUE) : jinbxc:uuzezdplfx


!/bin/bash

# Path to the ELF file
ELF_FILE="/challenge/embryoio_level11"

# Check if the file exists
if [ ! -f "$ELF_FILE" ]; then
    echo "Error: ELF file not found at $ELF_FILE"
    exit 1
fi

export jinbxc="uuzezdplfx"

# Execute the ELF file with stdin "uajzvqia"
echo "uajzvqia" | "$ELF_FILE" "zbzmaqopdr"

------------------------------------------------------------
Level 12
WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : shellscript
- the challenge will check that input is redirected from a specific file path : /tmp/bnitsh
- the challenge will check for a hardcoded password over stdin : ndalulxw

#!/bin/bash

# Path to the ELF file
ELF_FILE="/challenge/embryoio_level12"

# Path to the input file
INPUT_FILE="/tmp/bnitsh"

# Check if the ELF file exists
if [ ! -f "$ELF_FILE" ]; then
    echo "Error: ELF file not found at $ELF_FILE"
    exit 1
fi

# Check if the input file exists
if [ ! -f "$INPUT_FILE" ]; then
    echo "Error: Input file not found at $INPUT_FILE"
    exit 1
fi


# Execute the ELF file with input from file
"$ELF_FILE" &#x3C; "$INPUT_FILE"

pwn.college{Y32Ue22qoMZBX7fiED6Z8XL2bEO.QXyEDL3QzMzUzW}

------------------------------------------------------------
Level 13:

WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : shellscript
- the challenge will check that output is redirected to a specific file path : /tmp/xtnsry

I just added a redirect at the end of the script here easy enough

pwn.college{oKcTTlH5Y7bUqdutXNeSMFQgbl3.QXzEDL3QzMzUzW}

------------------------------------------------------------

Level 14

WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : shellscript
- the challenge will check that the environment is empty (except LC_CTYPE, which is impossible to get rid of in some cases)


#!/bin/bash

# Path to the ELF file
ELF_FILE="/challenge/embryoio_level12"

# Check if the file exists
if [ ! -f "$ELF_FILE" ]; then
    echo "Error: ELF file not found at $ELF_FILE"
    exit 1
fi

# Execute the ELF file with no environmental variables
env -i "$ELF_FILE"


pwn.college{skVh9qm_0HD6fDZK_JogY8yDo1O.QX0EDL3QzMzUzW}
------------------------------------------------------------

Level 15

- the challenge checks for a specific parent process : ipython

ONWARDS TO GREATNESS!

[INFO] This challenge will now perform a bunch of checks.
[INFO] If you pass these checks, you will receive the flag.
[TEST] Performing checks on the parent process of this process.
[TEST] We will now check that that the process is an interactive ipython instance.

[INFO] Since ipython runs as a script inside python, this will check a few things:
[INFO] 1. That the process itself is python.
[INFO] 2. That the module being run in python is ipython.
[INFO] If the process being checked is just a normal 'ipython', you'll be okay!

[INFO] The process' executable is /usr/bin/bash.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be python3.8.
[FAIL] You did not satisfy all the execution requirements.
[FAIL] Specifically, you must fix the following issue:
[FAIL]    Executable must be 'python'. Yours is: bash

In [2]: subprocess.run(["/challenge/embryoio_level15"])
WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : ipython

pwn.college{0LeB8Uc6XAyWrK-E8eMiEehB7DR.QX1EDL3QzMzUzW}

------------------------------------------------------------
Level 16
- the challenge checks for a specific parent process : ipython
- the challenge will check for a hardcoded password over stdin : itbbkzft

In [1]: import subprocess
   ...: 
   ...: input_data = b"itbbkzft\n"
   ...: subprocess.run(["/challenge/embryoio_level16"], input=input_data)

pwn.college{0PvlNykngtyQMEoOpuvxsUnCGci.QX2EDL3QzMzUzW}

------------------------------------------------------------
Level 17:

In [1]: import subprocess

In [2]: argv_argument="woblfjdnxf"

In [3]: ELF_FILE="/challenge/embryoio_level17"

In [4]: subprocess.run([ELF_FILE, argv_argument])

pwn.college{4jUm5wWNYbH_KmXAIq-dRaG1Aez.QX3EDL3QzMzUzW}

------------------------------------------------------------
Level 18

- the challenge checks for a specific parent process : ipython
- the challenge will check that env[KEY] holds value VALUE (listed to the right as KEY:VALUE) : rjyrkk:ciivztebra

In [1]: import subprocess

In [2]: env_variables = {"rjyrkk":"ciivztebra"}

In [3]: subprocess.run([ELF_FILE,], env=env_variables)
---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
Cell In[3], line 1
----> 1 subprocess.run([ELF_FILE,], env=env_variables)

NameError: name 'ELF_FILE' is not defined

In [4]: ELF_FILE="/challenge/embryoio_level18"

In [5]: subprocess.run([ELF_FILE,], env=env_variables)

pwn.college{4tgZAeMtiXr00WAvgmk9kYVmY80.QX4EDL3QzMzUzW}

------------------------------------------------------------
Level 19:

- the challenge checks for a specific parent process : ipython
- the challenge will check that input is redirected from a specific file path : /tmp/eaofyu
- the challenge will check for a hardcoded password over stdin : pbfciiku


In [1]: import subprocess

In [2]: subprocess.run(["/challenge/embryoio_level19"]), stdin=open('/tmp/eaofyu', 'r'))
  Cell In[2], line 1
    subprocess.run(["/challenge/embryoio_level19"]), stdin=open('/tmp/eaofyu', 'r'))
                                                                                   ^
SyntaxError: unmatched ')'


In [3]: subprocess.run(["/challenge/embryoio_level19"], stdin=open('/tmp/eaofyu', 'r'))

------------------------------------------------------------
Level 20:

hacker@program-interaction~level20:/challenge$ cat /tmp/xxmlmzz 
WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : ipython
- the challenge will check that output is redirected to a specific file path : /tmp/xxlmzz
- 
In [1]: import subprocess

In [2]: subprocess.run([/challenge/embryoio_level20], stdout=open('/tmp/xxlmzz', 'w'))
  Cell In[2], line 1
    subprocess.run([/challenge/embryoio_level20], stdout=open('/tmp/xxlmzz', 'w'))
                    ^
SyntaxError: invalid syntax


In [3]: subprocess.run(["/challenge/embryoio_level20"], stdout=open('/tmp/xxlmzz', 'w'))
Out[3]: CompletedProcess(args=['/challenge/embryoio_level20'], returncode=0)

In [4]: exit

pwn.college{MQ-u46CVaxzfKMFXp_d-Nqb0VOm.QXwIDL3QzMzUzW}


hacker@program-interaction~level21:/challenge$ ./embryoio_level21 
WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : ipython
- the challenge will check that the environment is empty (except LC_CTYPE, which is impossible to get rid of in some cases)

In [5]: subprocess.run(["/challenge/embryoio_level21"], env={})

pwn.college{oDRc3C5qzrBmHj44V_sZTyvnjxh.QXxIDL3QzMzUzW}

------------------------------------------------------------
level 22:
WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : python

did the basic subprocess but with python

pwn.college{I7a6Pbz59PFRulh6p4lcYCqlDi0.QXyIDL3QzMzUzW}

------------------------------------------------------------
Level 23:
WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : python
- the challenge will check for a hardcoded password over stdin : kfyvshok

import subprocess

# Input data
input_data = b"kfyvshok\n"

# Execute the ELF file with input data and in an environment empty of all other environment variables
with open('/dev/null', 'w') as devnull:
    subprocess.Popen(["/challenge/embryoio_level23"], stdin=subprocess.PIPE).communicate(input=input_data)
    
------------------------------------------------------------
Level 24:
WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : python
- the challenge will check that argv[NUM] holds value VALUE (listed to the right as NUM:VALUE) : 1:urbjnyuygs

import subprocess

# Input data
input_data = b"kfyvshok\n"
argv_arg = "urbjnyuygs"

# Execute the ELF file with input data and in an environment empty of all other environment variables
# with open('/dev/null', 'w') as devnull:
subprocess.run(["/challenge/embryoio_level24", argv_arg])

pwn.college{wqG16eC0H6lt5IHsC0xLZfJhinZ.QX0IDL3QzMzUzW}

Level25:

WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : python
- the challenge will check that env[KEY] holds value VALUE (listed to the right as KEY:VALUE) : lbztka:dikqwcvlej

  GNU nano 4.8                                           /home/hacker/programInteraction/knockknock.py                                                     
import subprocess

# Input data
input_data = b"kfyvshok\n"
argv_arg = "urbjnyuygs"


env_vars = {"lbztka": "dikqwcvlej"}

# Execute the ELF file with input data and in an environment empty of all other environment variables
# with open('/dev/null', 'w') as devnull:
subprocess.run(["/challenge/embryoio_level25"], env=env_vars)

------------------------------------------------------------
Level26:

- the challenge checks for a specific parent process : python
- the challenge will check that input is redirected from a specific file path : /tmp/lcghdf
- the challenge will check for a hardcoded password over stdin : hpvlhbyn


import subprocess

# Input data
input_data = b"kfyvshok\n"
argv_arg = "urbjnyuygs"


#env_vars = {"lbztka": "dikqwcvlej"}

# Execute the ELF file with input data and in an environment empty of all other environment variables
# with open('/dev/null', 'w') as devnull:

# Execute the ELF file with input redirected from the file
subprocess.run(["/challenge/embryoio_level26"], stdin=open('/tmp/lcghdf', 'rb'))

------------------------------------------------------------
Level 27:

WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : python
- the challenge will check that output is redirected to a specific file path : /tmp/kerdjy

subprocess.run(["/challenge/embryoio_level27"], stdout=open('/tmp/kerdjy', 'w'))

pwn.college{UBq-z1LtqYC86qSFPixluKha1q5.QX3IDL3QzMzUzW}

------------------------------------------------------------
Level 28:
WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : python
- the challenge will check that the environment is empty (except LC_CTYPE, which is impossible to get rid of in some cases)

pwn.college{ILRKw9ZPb6aR2zDrkxBcUb_Ajz5.QX4IDL3QzMzUzW}

------------------------------------------------------------
Level 29:

WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : binary

ONWARDS TO GREATNESS!

[INFO] This challenge will now perform a bunch of checks.
[INFO] If you pass these checks, you will receive the flag.
[TEST] Performing checks on the parent process of this process.
[TEST] Checking to make sure that the process is a custom binary that you created by compiling a C program
[TEST] that you wrote. Make sure your C program has a function called 'pwncollege' in it --- otherwise,
[TEST] it won't pass the checks.
[HINT] If this is a check for the *parent* process, keep in mind that the exec() family of system calls
[HINT] does NOT result in a parent-child relationship. The exec()ed process simply replaces the exec()ing
[HINT] process. Parent-child relationships are created when a process fork()s off a child-copy of itself,
[HINT] and the child-copy can then execve() a process that will be the new child. If we're checking for a
[HINT] parent process, that's how you make that relationship.
[INFO] The executable that we are checking is: /usr/bin/bash.
[HINT] One frequent cause of the executable unexpectedly being a shell or docker-init is that your
[HINT] parent process terminated before this check was run. This happens when your parent process launches
[HINT] the child but does not wait on it! Look into the waitpid() system call to wait on the child!


#include &#x3C;stdio.h>
#include &#x3C;stdlib.h>
#include &#x3C;unistd.h>

void pwncollege() {
    // Path to the ELF binary
    char *binary_path = "/challenge/embryoio_level29";

    // Check if the binary exists
    if (access(binary_path, X_OK) == -1) {
        fprintf(stderr, "Error: ELF binary not found at %s\n", binary_path);
        exit(EXIT_FAILURE);
    }

    // Fork a new process
    pid_t pid = fork();

    if (pid &#x3C; 0) {
        perror("Error forking process");
        exit(EXIT_FAILURE);
    } else if (pid == 0) {
        // Child process
        // Prepare arguments for execve
        char *argv[] = {binary_path, NULL};
        char *envp[] = {NULL};

        // Execute the ELF binary
        if (execve(binary_path, argv, envp) == -1) {
            perror("Error executing ELF binary");
            exit(EXIT_FAILURE);
        }
    } else {
        // Parent process
        // Wait for the child process to finish
        wait(NULL);
    }
}

int main() {
    // Call the pwncollege function
    pwncollege();

    return 0;
}

pwn.college{Ymy8wcsFH_8W7-zbU4TGnM1XsMt.QX5IDL3QzMzUzW}

------------------------------------------------------------
Level 30:

WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : binary
- the challenge will check for a hardcoded password over stdin : pfepfajn

#include &#x3C;stdio.h>
#include &#x3C;stdlib.h>
#include &#x3C;unistd.h>
#include &#x3C;fcntl.h>
#include &#x3C;string.h>

void pwncollege() {
    // Path to the ELF binary
    char *binary_path = "/challenge/embryoio_level29";

    // Create a pipe
    int pipe_fd[2];
    if (pipe(pipe_fd) == -1) {
        perror("Error creating pipe");
        exit(EXIT_FAILURE);
    }

    // Fork a new process
    pid_t pid = fork();

    if (pid == 0) {
        // Child process
        // Close the write end of the pipe
        close(pipe_fd[1]);

        // Set up stdin for the child process
        dup2(pipe_fd[0], STDIN_FILENO);
        close(pipe_fd[0]);

        // Execute the ELF binary
        execl(binary_path, binary_path, NULL);
        // exec functions do not return unless there's an error
        perror("Error executing ELF binary");
        exit(EXIT_FAILURE);
    } else if (pid > 0) {
        // Parent process
        // Close the read end of the pipe
        close(pipe_fd[0]);

        // Write the string to the pipe
        char *input_data = "pfepfajn\n";
        write(pipe_fd[1], input_data, strlen(input_data));
        close(pipe_fd[1]);

        // Wait for the child process to finish
        wait(NULL);
    } else {
        perror("Error forking process");
        exit(EXIT_FAILURE);
    }
}

int main() {
    // Call the pwncollege function
    pwncollege();

    return 0;
}


pwn.college{gshLb0z7ScDcIHF0jd9O116ml1Q.QXwMDL3QzMzUzW}
Level 31:

WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : binary
- the challenge will check that argv[NUM] holds value VALUE (listed to the right as NUM:VALUE) : 1:jbxnucvjoe

hacker@program-interaction~level31:~$ cat bangbang.c 
#include &#x3C;stdio.h>
#include &#x3C;stdlib.h>
#include &#x3C;unistd.h>
#include &#x3C;fcntl.h>
#include &#x3C;sys/wait.h> // Include this for wait()

void pwncollege() {
    // Path to the ELF binary
    char *binary_path = "/challenge/embryoio_level31";

    // Fork a new process
    pid_t pid = fork();

    if (pid == 0) {
        // Child process

        // Set up stdin for the child process
        int fd = open("/dev/null", O_RDONLY);
        dup2(fd, STDIN_FILENO);
        close(fd);

        // Execute the ELF binary
        execl(binary_path, binary_path, "jbxnucvjoe", NULL);
    } else if (pid > 0) {
        // Parent process
        int status;
        wait(&#x26;status); // Wait for the child process to finish
    }
}

int main() {
    // Call the pwncollege function
    pwncollege();

    return 0;
}

pwn.college{gTvi6uV2NalrzDkUneMk2rHziu-.QXxMDL3QzMzUzW}

------------------------------------------------------------
Level 32:

hacker@program-interaction~level32:/challenge$ ./embryoio_level32 
WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : binary
- the challenge will check that env[KEY] holds value VALUE (listed to the right as KEY:VALUE) : dzsioq:fqenenoweh

Grabbed this note from the github [pwncollege.github.io/modules/interaction.md at master · hale2024/pwncollege.github.io · GitHub](https://github.com/hale2024/pwncollege.github.io/blob/master/modules/interaction.md)

I can also use `env` to set environment variables.

$ env -i NAME=Yan JOB=Professor ./countenv

hacker@program-interaction~level32:~$ env -i dzsioq=fqenenoweh ./bangbang

pwn.college{wPqFwKekHx6Jk9v1iD-sAm-l-aj.QXyMDL3QzMzUzW}

------------------------------------------------------------
Level 33:

WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : binary
- the challenge will check that input is redirected from a specific file path : /tmp/pempyr
- the challenge will check for a hardcoded password over stdin : zyorkqoc

pwn.college{sFQLEGupQo-SCqDBEZkEKgT-fSO.QXzMDL3QzMzUzW}

#include &#x3C;stdio.h>
#include &#x3C;stdlib.h>
#include &#x3C;unistd.h>
#include &#x3C;fcntl.h>
#include &#x3C;sys/wait.h> // Include this for wait()

void pwncollege() {
    // Path to the ELF binary
    char *binary_path = "/challenge/embryoio_level33";

    // Fork a new process
    pid_t pid = fork();

    if (pid == 0) {
        // Child process

        // Set up stdin for the child process
        int fd = open("/tmp/pempyr", O_RDONLY); // Change this line
        dup2(fd, STDIN_FILENO);
        close(fd);

        // Execute the ELF binary
        execl(binary_path, binary_path, "jbxnucvjoe", NULL);
    } else if (pid > 0) {
        // Parent process
        int status;
        wait(&#x26;status); // Wait for the child process to finish
    }
}

int main() {
    // Call the pwncollege function
    pwncollege();

    return 0;
}

------------------------------------------------------------
Level 34:

- the challenge will check that output is redirected to a specific file path : /tmp/egadhw

pwn.college{M8u72v8Lay85EPxJoHbzYgKI5E9.QX0MDL3QzMzUzW}

freopen("/tmp/egadhw", "w", stdout);

        execl(binary_path, binary_path, NULL);
        
------------------------------------------------------------
Level 35:

WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : binary
- the challenge will check that the environment is empty (except LC_CTYPE, which is impossible to get rid of in some cases)

Also from the github
env -i will run it with an empty env
$ env -i ./countenv
There are 0 environment variables.

pwn.college{kWJGHXpa0c6umvvmsXhMKPRCkED.QX1MDL3QzMzUzW}

------------------------------------------------------------
Level 36:

Back to bash babyyy

ELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : bash
- the challenge checks for a specific process at the other end of stdout : cat

ONWARDS TO GREATNESS!

[INFO] This challenge will now perform a bunch of checks.
[INFO] If you pass these checks, you will receive the flag.
[TEST] Performing checks on the parent process of this process.
[TEST] Checking to make sure the process is the bash shell. If this is a check for the parent process, then,
[TEST] most likely, this is what you do by default anyways, but we'll check just in case...
[INFO] The process' executable is /usr/bin/bash.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be bash.
[FAIL] You did not satisfy all the execution requirements.
[FAIL] Specifically, you must fix the following issue:
[FAIL]    The shell process must be running in its default, interactive mode (/bin/bash with no commandline arguments). Your commandline arguments are: ['/bin/bash', '--init-file', '/usr/lib/code-server/lib/vscode/out/vs/workbench/contrib/terminal/browser/media/shellIntegration-bash.sh']

So one thing of note is to get it to not use the bin/bash in the arg len it has to be called like

. ./bangbang.sh

#!/bin/bash

# Call the binary and redirect its output to a file
binary_path="/challenge/embryoio_level36"

# Wait for the binary to finish
$binary_path | cat


pwn.college{Qa8GxxBF9hJECil45xkkhDg1ovn.QX2MDL3QzMzUzW}

------------------------------------------------------------
Level 37

WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : bash
- the challenge checks for a specific process at the other end of stdout : grep

Light work change the cat to grep

pwn.college{k3BJPsFPWpULz5DGdt4uLsLGDQ9.QX3MDL3QzMzUzW}

------------------------------------------------------------
Level 38

- the challenge checks for a specific parent process : bash
- the challenge checks for a specific process at the other end of stdout : sed

So the VS code term barely f***in works which is a PITA but its all good ig.

pwn.college{o_5g5NC9pq0Co18Ku9WAWXElDIn.QX4MDL3QzMzUzW}
Level 39:

- the challenge checks for a specific parent process : bash
- the challenge checks for a specific process at the other end of stdout : rev
Just double rev pipe light work

------------------------------------------------------------
Level 40:

I beat at this for a while and found a yputube video. The command was like

cat | ./embryowhatever

Then i entered the input after it asked for it? not totally sure how this works need to do more research here.

pwn.college{ACiwHhDvIPZLplHpkP0j-UHSbU1.QXwQDL3QzMzUzW}

------------------------------------------------------------
Level 41: f*** u i finished it

WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : bash
- the challenge checks for a specific process at the other end of stdin : rev
- the challenge will check for a hardcoded password over stdin : vnyeyriu

This seems straight forward

here's the password backwards

uiryeynv

So this one just seems to be broken I know its being done right but lets mark this as a come back later thing ig. If its super broken I make a second account and have a new env

pwn.college{YFF0DMI47QIKnNehyCrq5IZca0P.QXxQDL3QzMzUzW}

Figured it out. Ctrl+D for the EOF signal
Level 42:

hacker@program-interaction~level42:/challenge$ ./embryoio_level42 
WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : shellscript
- the challenge checks for a specific process at the other end of stdout : cat

So apparently I was doing some real weird sh*t before that lol and shouldn't have been writing a script.. Basic script just call binary and | cat
<strong>
</strong>------------------------------------------------------------
<strong>Level 43:
</strong>
- the challenge checks for a specific process at the other end of stdout : grep

I did weird sh*t to get to work earlier
pwn.college{81oJ-MRO8LC4Aq-susOsnNMTPGW.QXzQDL3QzMzUzW}

------------------------------------------------------------

Level 44:

- the challenge checks for a specific parent process : shellscript
- the challenge checks for a specific process at the other end of stdout : sed

#!/bin/bash

# Path to the binary
binary_path="/challenge/embryoio_level44"

# Hardcoded input
#input="kzblkgqh"

# Create a named pipe
#mkfifo mypipe

# Start a loop in the background that continuously echoes a line into the pipe
#(cat &#x3C; mypipe; tail -f /dev/null) &#x26;

# Call the binary with stdin redirected from the pipe

$binary_path | sed 'p'


pwn.college{E81GD467HYhmY9SVeulrg47yMz4.QX0QDL3QzMzUzW}

------------------------------------------------------------
Level 45:

It was the double rev pipe again

pwn.college{Ahvn0vUKFDzvoT1EENBeB6Vj_ju.QX1QDL3QzMzUzW}

------------------------------------------------------------

Level 46:

This was the empty cat module again

hacker@program-interaction~level46:/challenge$ ./embryoio_level46 
WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : shellscript
- the challenge checks for a specific process at the other end of stdin : cat
- the challenge will check for a hardcoded password over stdin : hukyaqik

pwn.college{0ijZCMcRJvilG_AaMW5PG8lAzs1.QX2QDL3QzMzUzW}

Level 47:

WELCOME! This challenge makes the following asks of you:
- the challenge checks for a specific parent process : shellscript
- the challenge checks for a specific process at the other end of stdin : rev
- the challenge will check for a hardcoded password over stdin : abbarrpj

Oh god

So ctrl+D sends the EOF signal to end the rev process. Now I can go back and fix what I missed

pwn.college{gCdgPqQ00CHKBDUqSPjEc_YErW9.QX3QDL3QzMzUzW}

------------------------------------------------------------
Level 48: COME BACK AND REWRITE

Holy Nightmare fuel

Out[4]: b"WELCOME! This challenge makes the following asks of you:\n- the challenge checks for a specific parent process : ipython\n- the challenge checks for a specific process at the other end of stdout : cat

pwn.college{sRiqlr7LFTR8qaxcqgqjnRKr3hf.QX4QDL3QzMzUzW}

What worked
import subprocess

  

o = subprocess.Popen(["/challenge/embryoio_level48"], stdout=subprocess.PIPE, stderr=subprocess.PIPE)
out = subprocess.Popen(['cat'], stdin=o.studout, stdout=subprocess.PIPE)
r, e = out.communicate()

What I would like to work
from pwn import *


p1 = process(["/challenge/embryoio_level48"], stdout=PIPE,stderr=PIPE)
p2 = process("/usr/bin/cat", stdin=p1.stdout, stdout=PIPE)
r2,e2=p2.communicate()
print(r2)


</code></pre>
