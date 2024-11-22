# Modern Operating Systems 5th edition
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


### General computer Architecture
It goes as follows,
the Central Processing Unit is doing all the  lifting in term of instruction execution.
It's internal memory is fast to keep up with, and layered in slower but bigger chunks called cache level. Since processor' memory is fast, it is
prohibitively expensive and thus, limited. More memory is available albeit a bit slower,
as the main memory, accessible by the processor  through a memory management unit (MMU).


This is half the story, but a computer is not just a processor and  it's memory, it is also peripherals, lots of them !
- graphic cards
- keyboard
- printers
- sound card
- network modules
- hard drives for even more memory
- ...
They are all connected together on a same line called a bus, and they speak in turn. There are different
types of bus for different types of devices,
- SATA for hard drives
- USB for many plug n play devices like keyboard and printers
- PCI Express for very fast and demanding  peripherals like sound card, graphic cards, network interfaces.
This Bus architecture allows to have a much more compact computer and to mutualize management resources, since anyway
the processor can only talk to so many peripherals simultaneously at any given time. 

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


#### User Space and Kernel Space
Actions which aren't "dangerous" for the operating system (understand the ones that does not need further resources
than the one already available) are running in user space. This is the mode where most programs work.

Actions which interact with the resources of the operating system send a request and get their request 
worked on for them by the operating system. The code of the operating system which is performing the work
needed to satisfy the request is privileged, it is code of the operating system runnin with elevated privileges,
in Kernel space.


#### System Calls 
Hook accessed by a process when it wants the Operating System
to perform an action for it (like opening a file, getting more memory or communicate with someone).
At the other side of the hook lies code that WILL run in kernel mode as it needs it to perform it's task.
Note that while there "always" is code that will run in kernel mode in standard system calls, 
there can also be code that does not requires it and thus will be ran in user space like any "normal" code.


### Various Type of operating systems

#### Monolithic kernel systems
In monolithic systems, everything pertaining to the os is packed together in one giant program running.
Only user programs are running in user mode.
Very practical from a development standpoint, it is also the most dangerous,
as a faulty driver could bring to a halt the whole system.
Caution though, it doesn't mean that the operating system is in one big source code file and that their can't be code module,
but in the end everything is running as one single program.

#### Layered kernel Systems
The Operating system is split into layers, each one depending on the one below and
providing service to the one above.
| Level | Layer name |
|---|----------------------|
| 5 | The User             |
| 4 | User Program         |
| 3 | IO Management        |
| 2 | Process Management   |
| 1 | Memory Management    |
| 0 | Processor Management |

Code on level 1 does not think too much about cpu cores, cache synchronization and race conditions.
Code on level 2 doesn't care if the next instruction to be loaded is in a memory page still in the hard drive
and not in the RAM.
Code on level 3 doesn't care about how process memory is split an their state of execution.
code on level 4 isn't concerned about the nasty details of networking, video output, USB, and file reading from disk
On level 5, the user, doesn't need to know how to code !


#### Micro Kernel
Micro kernels are a subcategory of layered systems, where only the most vital pieces of software of the operating system
are running in kernel Mode, everything else (including piece of the OS ) are running in user space mode.
They can be slower than monolithic systems though, as even part of the OS  are now also running back and forth between
user mode and kernel mode. Embedded critical systems are fond of this kind of OS since they offer
better safety guarantees than a monolithic kernel.

| User Programs | Shell, Make,gcc, firefox,Doom,minecraft,blender                         |
|---------------|-------------------------------------------------------------------------|
| Services      | File System, Processes, Process scheduling                              |
| Drivers       | Audio, Networking,TTY,Graphical driver,USB,...                          |
| Micro Kernel  | Clock, RAM, Processor,Threading,Interrupts, Inter Process Communication |



#### Virtual machines, hypervisor containers and co. ...
All abstraction engines adding more or less abstraction between the real hardware
and a hypthetical one on which another operating system, a  "guest OS" works.





## Processes and Threads

##  Memory Management
### Why is good memory management so important 
Let's say we have three places for a processor to access needed data 
- 95% of the time the data is located in  processor's cache, it takes 1 nano second to retrieve it.
- 4 % of the time the data is located in  RAM, it takes 10 nano second to retrieve
- 1 % of the time the data is located in disk, it takes 10 milliseconds to to retrieve it 
What is the mean time to retrieve data ?
0.95 * 1 + 0.04 * 10 + 0.01 * 10,000 = 100 nano seconds !
You can have a processor that can execute instructions at a 1 nano second rate  (1Ghz)
and it will be as fast as a processor  running at a 100 nano second rate (10 Mhz)
during data heavy period of times ! and processor always joggle with lots of data !
  


## File Systems

## Input / Output

## Deadlocks

## Virtualization and the cloud

## Multiple Processor Systems

## Unix Peculiarities 

## Windows Peculiarities

## Operating System Design
