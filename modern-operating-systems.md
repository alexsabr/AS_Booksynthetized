# Modern Oerating Systems 5th edition
Andrew Tanenbaum, Herbert Bos


## Introduction
### The purpose of an operating system 
An operating system has two main goals
- Providing a logical, predictable, unique, ordered (i.e. beautiful) interface
    for programs and user to access the hardware,
    when said hardware is messy,variable , and filled with caveats.
- Ensuring a fair share of the resources a computer provides among all the users
    (definition of fair may vary)

### Very Brief history of operating systems 
#### 1945-1955
Operating system do not exist. Programmers are completely knowledgeable
about the hardware and write all their program either
- in machine code,
- hardwire it with electronics and copper inside the computer itself !
These programs run on very big computers : mainframes.

#### 1955-1965
With the apparition of the first IC's, starting to replace vacuum tubes,
An embryo of operating system starts to emerge.
It runs on magnetic tapes.
It is closer to a "bootloader/shell" for one program only at any given time though.
The programming languages of the time which reached us to this day are Fortran and Cobol.
Mainframes are still the only type of computer to exist.

#### 1965-1980
We know start to see full fledged operating systems,with
- multiple programs sharing memory
- file systems 
- multi CPU support
- shell (not really at the time, but could be thought of today)
One famous operating system of the time is 
MULTICS (MULTIplexed Information and Computing Service)

Now the access to computers
starts to widen, with one main frame and many access terminals.
They start to be found in small numbers in
universities, banks and other businesses.

Some food for thought: 
The first official release of MULTICS dates 1969,
who could have predicted that 40 years later, anyone could get
for under 1000$ a computer 10.000 times faster ?


#### 1980-20XX (Today)
In this period of times are born
Minix (1987)
Linux (1991) "just a hobby, won't be big and professional like GNU"
Windows (it's ancestor MS-DOS in 1981)
OSX (2001)
Free-BSD (1993)

### 7 types of devices which all need an operating system
#### Main Frames
The biggest of computers. Think supercomputers with
a few hundred cores (coming from multiple cpu !),
hard drive memory expressed in hundred of terabytes if not petabytes,
networking between peers in fiber optics end to end.

#### Server 
Can be repurposed mainframes, just like very powerful personal computer
with something like 32 cores coming from 4 cpu, 128 Gigabytes of RAM
and 20 Terabytes of Data. Running Linux, FreeBSD, or Windows Server.

#### Personal Computer
The workhorse of everyday humans, even though they tend to be shadowed 
by their pocket version, the smartphone.
Contains maybe the most variety of operating systems
Linux, Windows,FreeBSD,OSX,Solaris, TempleOS ...

#### Smartphone and handheld computer
It is estimated that around 7.20 Billions smartphones exist on earth today,
all this market share is mostly in the hands of two players
Google with Android, a Linux-based OS
and Apple with iOS.

#### Internet of Things and Embedded systems
What is the commong denominator between your CCTV,
your watch and your washing machine ? They are all now intelligent !
Very low footprint operating systems, for very low power machines.
Energy consumption in the Watt or even the milliWatt, memory counted in
kiloBytes, processor speed in MHZ or even slower, kHz !
Operating system includes RIOT, QNX, Embedded Linux, Embedded Windows

#### Real Time Operating Systems
When life and property are on the line, when a physical process
happening in milliseconds or less must be managed, 
Realtime Operating System are the right tool for the job.
With hard time and safety requirements, nothing is left to interpretation,
and thee operating systems are often tailor-made and stripped down
to the absolute bare minimum.

We can only encourage you to check out the playlist
of Shawn Hymel explaining RTOS, freely accessible on youtube.

#### SmartCards
You think Internet of things comes with way too much memory or power
and want a tougher challenge ? Seek no further,
operating system running on credit cards is as bare bones as one can get.
Funnily enough some card holds a Java Virtual Machine, running some java code.

### User Space and Kernel Space


### General computer Architecture

### Some fundamental abstractions provided by operating systems 
They are here explained briefly, check each of their own respective section down this file for 
a more thorough study.
####  Process
Part or totality of a running program,
made of among other things :
- instructions to be executed by the processor
- memory to store informations (heap and stack)
- a list of file currently used by the process
- a list of alarms to communicate with the process
- a list of related process
- the id of the user who launched the process
- the id of the process

#### Address Space
The main memory of the computer where currently (or will be shortly) running
program are stored. In a multi program OS, the address space must be protected
so process cannot modify memory of other process without explicit authorization.

#### Files
 Blocks of Data stored somewhere which can be accessed by users and processes.
 Usually file persist between normal computer shutoff and reboot.
 They are ordered in a tree like structure.
 Among other things, they have a name, an id, some access rights,
 and memory blocks they occupy.
 
#### Filesystem
The Complete hiearchy of all files.
There is usually one main file system, to which other can be added,
they are "mounted".
An example is a USB stick being plugged to a running computer.

#### Shell 
Read Eval Print Loop (REPL) program which allows
the user to interact with the operating system.
Was the main (if not the only way) for a human to interact with a computer
before the advent of GUI.

#### System Calls 
Code called by a process when it wants the Operating System
to perform an action for it (like opening a file, getting more memory or communicate with someone).


#### Various Type of Kernel in operating systems

### Monolithic systems

### Micro Kernel

### Layered System





## Processes and Threads

##  Memory Management

## File Systems

## Input / Output

## Deadlocks

## Virtualization and the cloud

## Multiple Processor Systems

## Unix Peculiarities 

## Windows Peculiarities

## Operating System Design
