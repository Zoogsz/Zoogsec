---
description: 139 labs???? any%
---

# Program Interaction

## Program Interaction: Binary Files

Lets start with cat, what is cat?

* It is a 64 bit ELF file.

What is an ELF then?\
ELF is a binary file format that contains the programs and its data.

2 Main components

1. ELF Program Headers - The source of information used when loading a file
   1. Define the segments aka the parts of the file that are loaded into memory.
   2. INTERP: defines the library that should be used to load this ELF into memory
   3. LOAD: defines a part of the file that should be loaded into memory.
2. ELF Section Headers - Section headers are not a necessary part of the ELF. Segments (defined via the program headers) are needed for loading and operation. Headers are just metadata
   1. .text: the executable code of your program
   2. .plt and .got: used to resolve and dispatch library calls
   3. .data: used for pre-initialized global writable data (global arrays with initial values)
   4. .rodata: global read-only data (like string constants)
   5. .bss: uninitialized global writable data (global arrays without initial values)

Then there are **Symbols** - Binaries and libraries that use dynamically loaded libraries rely on symbols (names) to find libraries, resolve function calls into those libraries etc.

How do we interact with ELF?

* gcc - to make your elf
* readelf - to parse the header
* objdump - to parse the ELF header and disassemble the src code
* nm - to view ELF symbols
* patchelf - to change some ELF's symbols
* objcopy - to swap out ELF sections
* strip - to remove otherwise-helpful information (such as symbols)
* kaitai struct to look through ELF interactively
  * [https://ide.kaitai.io/](https://ide.kaitai.io/)

## Linux Process Loading

Lets take /bin/cat

When we run cat /flag

1. A process is created
2. Cat is loaded
3. Cat is initialized
4. Cat is launched
5. Cat reads its arguments and environment
6. Cat does its thing
7. Cat terminates

#### Portrait of a process

Every Linux process has:

* state (running, waiting, stopped, zombie)
* priority (and other scheduling information)
* parents, siblings, children
* shared resources (files, pipes, sockets)
* virtual memory space
* security context
  * effective uid and uid
  * saved uid and gid
  * capabilities

Where do these process come from though?\
fork (and more recently) clone are system calls that create a nearly exact copy of the calling process: a parent and a child.\
Later, the child process usually uses the execve syscall to replace itself with another process

Example:

* you type /bin/cat in bash
* bash forks itself into the old parent process and the child process
* the child process execves /bin/cat becoming /bin/cat

Can we load? Before anything is loaded the kernel checks for executable permissions. If a file isn;t executable execve will fail.

But what do we load?\
To figure this out the kernel reads the begging of the file and makes a decision;

1. If the file starts with #! the kernel extracts the interpreter from the rest of that line and executes this interpreter with the original file as an argument.
   1. **This interpreter also totally could be a shell script/alternative binary.**
2. If the file matches a format in **/proc/sys/fs/binfmt\_misc** - the kernel executes the interpreter specifically for that format with the original file as an argument.
3. If the file is a dynamically-linked ELF, the kernel reads the interpreter/loader defined in the ELF, loads the interpreter and the original file and lets the interpreter takes control
4. If the file is a statically linked ELF the kernel will load it
5. Other legacy file formats are checked for

It is looking for magic bytes at offset 0 in order to figure out what format to use.

Note: These can totally be recursive.

#### Dynamically linked ELFs: the interpreter

Process loading is done by the ELF interpreter specified in the binary.

```
readelf -a /bin/cat | grep interpret

Will show the "loader"
```

This can be overriden

```
lib64/ld-linuxx86-64.so.2 /bin/car /flag
```

Or even changed permanently

```
patchelf --set-intepreter
```

Now the loading process

1. The program and its interpreter are loaded by the kernel
2. The interpreter locates the libraires
   1. LD\_PRELOAD env variable, and anything in /etc/ld.so.preload
   2. LD\_LIBRARY\_PATH env variable (can be set in the shell)
   3. DT\_RUNPATH or DT\_RPATH specified in the binary (both can be modified with patchelf)
   4. system-wide configs (/etc/ld.so.conf)
   5. /lib and /usr/lib
3. The interpreter loads the libraries
   1. These can depend on other libraries causing more to be loaded
   2. relocations are updated

Where is all this getting loaded too?

* Each Linux proceess has a virtual memory space that contains
  * the binaries
  * the libraries
  * the "heap" (for dynamically allocated memory)
  * the "stack" (for function local variables)
  * any memory specifically mapped by the program
  * some helper regions
  * kernel code in the "upper half" of memory (above 0x8000000000000000 on 64-bit architectures)

Virtual memory is dedicated to your process\
Physical memory is shared among the whole system

You can see this whole space by looking at /proc/self/maps

#### The Standard C Library

* libc.so is linked by almost every process.
* This provides many of the main functionalities
  * printf()
  * scanf()
  * socket()
  * atoi()
  * malloc()
  * free()

First the binary is loaded, then **initialized (3).** In example again: Cat.

* Every ELF binary can specify constructors, which are functions that run before the program is actually launched
* For example, depending on the version - libc can initialize memory regions for dynamic allocations (malloc/free) when the program launches.

```
__attribute__((constructor)) void haha()
{
	puts("Hello world!");
}
```

## Linux Process Execution

Still focusing on cat, lets move onto the **launching step (4)**\
A normal ELF automatically calls `__libc_start_main()` in libc which in turn calls the program's main() function.

Step 5: **Cat reads its arguments and environment**\
`int main(int argc, void **argv, void **envp);`

Your process's entire input from the outside world at launch comprises of:

* the loaded objects (binaries and libraries)
* command-line arguments in argv
* "environment" in envp\
  However, processes need to keep interacting with the outside world

Step 6: Cat does the thing

The binary's _import symbols_ have to be resolved using the libraries _export symbols_\
In the past this was on-demand process and carried great peril. In modern times this is all done when the binary is loaded and is much safer.

So back to it how does it interact with the environment? This is primarily done via systemcalls (syscalls). Each system call is well-documented in section 2 of the man pages. We can trace these processes using **strace**

#### System Calls

System calls have a well defined interface that rarely changes.\
While there are over 300 syscalls in linux here are some important ones.

```
int open(const char *pathname, int flags) - returns a file new file descriptor (also shows up in /proc/self/fd!)
ssize_t read(int fd, void *buf, size_t count) - reads data from the file descriptor 
pid_t wait(int *wstatus) - wait child termination, return its PID, write its status into *wstatus
long syscall(long syscall, ...) - invoke specified syscall.
```

Typical signal combinations:

* fork, execve, wait (think: a shell)
* open, read, write (cat)

#### Signals

System calls are a way for a process to call into the OS. What about the other way around?\
This is what signals are used for. Some relevant calls:

```
sighandler_t signal (int signum, sighandler_t handler) - regoster a signal handler
int sigacation(int signum, const struct sigaction *act, struct sigaction *oldact) - more modern way of registering a signal handler

int kill(pid_t pid, int sig) - send a signal to a process
```

Signals pause process execution and invoke the handler. Handlers are functions that only take one argument - the signal number.\
Without a handler for a signal the default action is used (typically this is kill)\
SIGKILL (signal 9) and SIGSTOP (signal 19) cannot be handled.

The full list of these are in section 7 of man (man 7 signal) and kill -l.

#### Shared memory

Another way of interacting with the outside world is by sharing memory with other processes. This requires system calls to establish and once it is established communication happens without system calls.

The easy way is to use a shared memory-mapped file in /dev/shm

#### Process termination

The last thing cat does **(6) Cat terminates**

Terminate is processed in 1 of 2 ways

1. Receiving an unhandled signal
2. Calling the exit() system call: `int exit(int status)`

All processes must be "reaped"

* After termination they will remain in a zombie state until they are wait()ed on by their parent
* When this happens their exit code will be returned to the parent and the process will be freed.
* If their parent dies without wait()ing on them they are re-parented to PID 1 and will stay there until they're cleaned up.





## BONUS: Unix Shell: The Art of I/O Redirection

An absolutely fantastic writeup by Benjamin Cane going over helpful tips/tricks for I/O redirection within the Linux/Unix shell. Full article can be found here.

{% embed url="https://web.archive.org/web/20220629044814/http://bencane.com:80/2012/04/16/unix-shell-the-art-of-io-redirection/" %}

#### Input and Output

There are always 3 streams open

* stdin
* stdout
* stderr

These streams are used for interacting with the user input and program output within the shell environment. These have reserved file descriptors attached to them which means we can interact with them from command line.

stdin - Standard Input

* This stream is used to get input for commands from the user keyboard. stdin has the file descriptor of 0 and a file of /dev/stdin

stdout - Standard Output

* This stream is used for non-error output from programs. stdout has the file descriptor of 1 and a file of /dev/stdout.

stderr - Standard Error

* This stream is used for error output from programs. stderr has a file descriptor of 2 and a file of /dev/stderr

#### Examples of input and output

Example reference

```
**stdin**
-stdout-
_stderr_
```

Cat without a filename opens the cat program and expects user input

```
cat
**input here**
--input here--
```

When a program prints errors or diagnostic info it uses the Standard error stream rather then Standard Ouput. This keeps it from mixing a commands errors with the same commands outputs.

```
cat ./program
_cat: ./program no such file or directory_
```

#### Redirection

What if we want to take the stdout of one program and write it to a file?

```
program > file
```

The > is used to redirect to a file.

* A single left carror will truncate then enter the redirected data into the file (replacing) if it doesn't exist it will be created\
  The > symbol will redirect stdout by default however you can specify whether to redirect stdout or stderr by putting the appropriate file descriptor in front of the redirect symbol

```
1> redirects stdout (default)
2> redirects stderr
```

2 > symbols are used to append the output to a file rather than overwriting the file entirely. This can once again be done with the file descriptor to specify if you want stdout or stderror.

< is used to redirect input from a file instead

```
program < file
```

It can be used to redirect stdin from a file to a program

```
cat < /tmp/filename
test
```

#### Piping from one procces to another

The | pipe redirects stdout from one command to stdin for another. The pipe is not considered a redirect operator but rather a control operator; while pipe is used to redirect ouput not all controll operators have this function

We can also write to a file and stdout using tee

```
program | tee filename
```

Tee is neither a control or redirection operator but it is a command that will take the stdin given to it and write that both to a file specified and stdout. The -a flag will append the output rather than overwriting
