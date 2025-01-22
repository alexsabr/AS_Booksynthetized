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


### Terminology that doesn't fit in any other category
#### POSIX
TODO
#### UNIX
TODO
#### LINUX
TODO
#### GNU


## Processes and Threads

### Why process and what they really are
If you aren't stuck with a mainframe in the 1950's
your computer has to perform multiple tasks simultaneously,
or seemingly so (if you are unfortunate enough to have one single core).
It might juggle with hundreds of them for example :
- a web browser is playing a song in your speakers
- while you draw on a painting program,
- all of this during a daily system backup on your external drive
- finally your mail daemon (program running in the background) checks periodically if you have new mails.
That's not even taking account all the drivers that may be running too as independant
tasks if  you have a layered / micro kernel system.
Maybe even these tasks have to communicate with each other during their execution,
take the example of a video game that talks with the driver of your keyboard
to make it light up when something happens.
All of this to say operating system need a way to organized task and to manage them.
Enter processes.

### Memory in processes 
Their memory is separated in four distinct parts
- the text area, where all hard coded values lie, things like images and icons displayed inside the app,
  text for the user to read, ... .
- the instruction area
  Where all the code to be executed lies 
- the stack
  which is memory allocated each time a new function is called, holding
  all the processor context (the state of all the variables) inside a function.
  It is deallocated each time a function finishes.
- the heap
  which is memory dynamically allocated by the program in a somewhat irregular pattern

Now this is for what is strictly inside a process,
but there are also things that the operating system manages that are gravitating around it.

### side information on processes managed by the operating system

The operating system for each process keeps track of the following:
- the unique id  of the process to identify it among others.
- the user who launched the process
- a table of file descriptors (what files is the process currently using)
- a table of signals, communication switches to indicate a process or the OS that something is happening
- a status,
    - currently running
    - dead but has not been cleaned yet also called "zombie"
    - not running, blocked  because it is waiting for a resource from the OS
    - not running, but ready to run (the OS has currently decided that some other process is more worthy of cpu time.)
- in UNIX, the id of the parent process who gave birth to it using the **"fork"** system call.
  all UNIX processes take part in hierarchies of processes called **Process Group**,
  all of them in the end being children of the first  process **init** running as long as
  the operating system is online. (not the case in windows)

### Signals and interruptions
#### Signals
Sometimes a process needs to be notified of something in a timely fashion.
So this notification is so critical in fact that the process
should stop everything it is doing  to treat this notification.
these are **signals**. 
They are exclusively ***software based***, born from the mind of software engineers 
and implemented in the OS.
Processes can bind to them signal handlers, which are piece of code 
executed anytime a particular signal reaches the process.
As signal can happen anytime during the normal execution of the process,
they should be carefully crafted as little (if any) assumption can be made
about the state of the process.
When a process receives a signal,
- if it doesn't have any signal handler for it, 
the signal will be armed in the  signal table waiting for the process to manually check on it.
- if  the process has subscribed earlier a signal handler to receive this type of signal,
  the process context will be immediately stopped, saved and signal-handler instructions will be
  loaded instead. At the end of the execution of the signal handler, the process former context
  will be loaded back and previous execution resumed


####  Interruptions
Sometimes a piece of hardware needs to notify the processer of something in a timely fashion.
It can be even be the cpu notifying itself with the example of division by zero error.
This notification is so critical in fact that the cpu should stops  everything it is doing
to handle it. Theyre are **interruptions**  exclusively ***hardware based***, implemented
in the sillicia of the CPU. The OS / the CPU is responsible for managing them,
and sometimes they can be the source of signals for processes.
For example you are running a program which attempts to divide something by 0
A hardware interruption will be generated by the Arithmetic Logic Unit of the processor.
The kernel will then witness it and send a SIGFPE signal to the program
Here because a hardware interruption happened, the kernel sent a signal to a program,
but there are hardware interruption which do not result in a signal being sent to a program.
Also there isn't a 1 to 1 match between interrupts and signals,
for example SIGFPE could have been sent because  of a integer overflow, or a floating point
error, 4 interrupts, one signal. Also it could have been just a user 
asking the OS to send the signal via the "kill" command.



### Threads
Threads comes from the following observation,
sometimes a program is performing multiple tasks for the user,
and while a tasks hangs because it is waiting for disk for example,
another task of the same program could be performed.
Or the hardware has multiple cores which the program could benefit of
to do more work in the same amount of time.
It could indeed fork and collaborate with it's children,
but communication between processes  involves the kernel each time a message is sent or received.
It greatly hinders communication speed.
Also inter process communication is very rigid and involves a bit of overhead.
moreover you need the kernel everytime you spawn a process, again slowing things down.

What if instead we could have multiple instruction set running in the same program,
thus sharing the same memory space, greatly simplifying communication, and removing the kernel from the equation ?
Enter threads.

Initially, conceptualizing threads is really easy,
you need one program counter per thread indicating at which instruction
it stands, and one stack area per thread to save function context.
but after that things start to get messy, the hardware  gets involved and tough choices have to be made.
- what happens when a program with multiple thread is forked ?
- how do we ensure that if two threads read/write the same bit of heap memory, they have
  a coherent picture on what is happening ? That there aren't any deprecated copy lying around in CPU cache ?
- are software librairies re-entrant ? that is if a threads calls a function, then freezes in the middle of it,
  and then another threads executes and also calls the same function, the memory heap of the library hasn't been left in an incoherent state
  from the previous unfinished still pending execution ?
  An example is errno, a variable that indicates what kind of error happened on some system calls.
  A thread execute a system call which fails, the reason is written in errno. But before it can read it,
  the execution is handled to another thread which makes a system call that fails for another reason.
  errno is overwritten, and when the first thread will come back, it will see an errno value that has nothing to do with him.
- which threads handles signals for the process i.e. where the signal handlers executes ?
- are all threads frozen while a signal handler is running in one thread ?
- can another thread execute while one is waiting for a system call to finish ?

To answer these questions, threads can be implemented in user-space (keeping many of the blocking system calls problems),
in kernel space (increasing the overhead of making new threads) or both, that is one or more user space thread  
running on one or more kernel space threads (kind of the best of both worlds).


### Event driven programming, finite State Machine and Non blocking system calls
An alternative to process splitting and threading is
Having in your operating system non blocking system calls.
Let's say for example you are a web server.
When someone connects it requests a web page, if the file is on the disk
you can make the call to open and read it. Because it is non blocking,
you can start listening for another connection and see what is the request,
while the operating system is hard at work to get the file from the disk.
At a later time you can check to see if the operating system has granted you the content of the file
( you can check via an interrupt for example),
and send the content to the recipient  on the network (via another system call which may also be ran in the background).
This is called Event driven as systems events are driving forward your execution.
This method can seem a bit special, yet it is implemented in nginx, a very serious web server 
used in industrial grade settings.


### Concurrent programming  peculiarities for threading and high performance computing
#### Definitions
__Critical Region__
 Part of Code where access to a shared ressource between multiple concurrent entities is made.
 
__Race Condition__
A situation where the result of work between concurrent entities with the same input yields
different results based on when each has executed and how they managed to share (or fight for) resources.
Usually generates wrong/catastrophic results

__Mutual exclusion__
When multiple concurrent entites cannot execute in parallel a same action and must wait their turn.
Method used to control access to a shared resource.


#### Removing race conditions
Three part strategy
- Mutual exclusion on critical regions (for obvious reasons)
- no assumptions made about speed and number of CPU (otherwise you're just making a gimmick of who does what when,
   this is then  bad scheduling, not good race condition prevention)
- A concurent entity  outside of a critical region cannot hinder/stop a concurrent entity inside a critical region
- No concurent entity shall be starved forever of access to a critical region, we must guarantee that everyone
  who requires will, one day have access to a critical region.

##### The Peterson Algorithm
This algorithm prevents two concurent entities to suffer from a race condition.
This algorithm does not violate the "no assumption about number of processor",
here we "force" number of entities, regardless of the number of processor available.
If you have more than two concurrent entities, you can organize a tournament made of multiple duel,
since this algorithm provides you a way to choose a "winner" and a "looser".

``` pseudocode 
bool interestedflag[2] = [False, False] # shared resource by both entities
int turn # shared resource by both entities
MY_ID= XXX
OTHER_ID = XXX # this information is of course reversed for the other entity
interestedflag[MY_ID] = true;
turn = MY_ID;
# trying to enter critical section 
 while (interestedflag[OTHER_ID] is True  and turn == MY_ID)
 {
  # busy waiting while the other is in the critical resource, 
 }
  # Now inside the critical region
.....
  # Now leaving the  critical region
 turn = OTHER_ID;
 flag_interested[MY_ID] = false;
```
This algorithm works because there are two indicators which allows to 
- know if the other entity is already in the critical region
- know who goes first if both entities wishes to enter the critical region

We will draw a simple truth table to know what each combination of indicator states means:

"O" means the other  entity has raised it's flag_interested in the array, not "O" means it's set to False.
"T" means your ID is in the turn variable, "not T" means the other ID is in the turn variable.
"Not O" and "Not T" : Impossible state but even if it occurs the other entity does not wish to enter the critical region, you can go.
"Not O" and "T" : The other entity does not want to enter the critical region ,you can enter safely.
"O" and "T" : The other entity is either already in the critical region, or about to give you the way to enter
critical region by changing the state of indicators to "O" and "not T".
"O" and "not T" : The other entity is also interested in entering the critical section but you can go, it will wait. 

Note that this algorithm only works with two concurrent entities  because there isn't enough 
states in the truth table to allow at all to depict the state of more than two concurrent entities.

#### TSL Test and Set Instruction Lock; when the hardware comes to the rescue
TSL is a CPU command which allows a program to test and set the value of a register in memory 
atomically. It gives the guarantee that the reading of a register, and writing in it if it contains
a certain value will happen with another core stepping in and also writing to same register.
Effectively given the programmer a hardware lock which greatly eases the establishment
of locks to access a shared resource.



Both of these solutions to race conditions make the process waiting for the resource in active waiting.
This wastes energy and CPU time, which can lead to a problem called priority inversion.


#### Priority inversion , or why ensuring the absence of race condition does not guarantee  that a concurrent system works smoothly.
Given two task, High and Low with High and Low priority in execution respectively,
If Low gets a hold a of a shared resource, then is sent to sleep for the High task to be executed,if the High
task also needs the shared resource, it wont be able to obtain it until the Low task has resumed operation
and released it. If it is busy waiting it can wait like this until the CPU preemptively stops it and gives way to another task.
This is wasted CPU time. In a scenario where the scheduler is nonpreemptive, the system is blocked.
Even though the Low task is of Low priority, it is stopping the High priority task from executing.
Priority has been inversed. This problem is a special kind of deadlock where the problem comes from priority level.


##### The random boosting solution
From time to time, a random process sees it's a priority greatly raised temporarily.
A non-deterministic way to solve the problem.

##### The Priority ceiling solution
Forbids entities with a priority higher than a given threshold to acquire a lock
allowing low priorities tasks to continue it's work.

##### The priority inheritance
If a low priority task holds a resource that a high priority task requests,
the low priority taks gains temporarily high priority.


#### Semaphores
If Busy waiting with the peterson algorithm and or through a dumb use  of TSL locks work,
it is far from optimal and wastes valuable CPU time. Introducing semaphores:
A counter which has two atomic operations
- Try to decrement the counter. If it is already to zero, I go to sleep
  and it is to the semaphore to wake up the concurrent entity when the decrementation operation can be performed.
- increment the counter
This is very used in POSIX to synchronize threads and/or processes.
It is mainly used in this form to avoid a producer-consumer problem where a producer
floods the consumer with too much data.

#### Mutex
Semaphores with only two states: locked and unlocked.
Used to lock access to resources.

#### Futex "Faster User Space Mutex"
Using Mutex and semaphores is good with a lot of contention,
but when there is little contention it generates 
unnecessary kernel calls. Instead,
by a clever use of the TSL instruction to first try to grab a lock without going into kernel mode,
we can minimize the kernel calls in period of small contentions and have a robust mechanism
in period of high contention.

#### Condition Variables
Allows to release an owned mutex,
go to sleep and wake up with the mutex llocked again, all atomically.

The atomic feature is important as it helps to protect against deadlock.
For example when you need multiple locks but only managed to acquire a few,
you can relinquish those which you have acquired for a time, for other to uses.
This is in the hope that when you wake up, other will have had time to finish their work and 
release the locks that you need so you will
be able acquire them.
Java as well as C++ have condition variables. 

#### Monitors
Programming language feature where variables and methods to interact with said variables are grouped
together such as only on concurrent entity at a time can interact with them.
Effectively giving protection for critical region, at the discretion of the programmer.
One example of this feature is  "synchronized" keyword of Java


#### Message Passing
Instead of locks and mutex and condition variables,
concurrent entities send and receive message through the intermediary of
the operating system to synchronize on who does what when.
Allows for concurrent operation across network (unlike semaphores and mutex).
The Message Passing Interface or MPI, is a standard 
designed specially to deliver this service in high performance computing.
Implemented in many well known language like Python, Java,R, Matlab ... .


#### Synchronization Barrier
Concept of concurrent programming where multiple concurrent entity have to wait each other
at some milestone before continuing execution. Particularly useful again in
High Performance Computing.
Also useful in Operating System, for example with Super Scalar CPU where 
multiple instructions of a program are executed out of order,
to ensure everyone has finished computing it's instruction before reassembling the result
into a coherent result for the program.


#### Read-Copy Update
Is it possible to have multiple concurrent entities operate on a shared
data structure like a list, a tree or a table,
concurrently, without locks, or mutexes on **the whole structure** (allowed on a smaller sample)
and still be able to operate without race condition and inconsistent results ?
After all we have listed earlier it should seem impossible yet it is
enter the world of Read-Copy Update.

Some  operations do need to be atomic, wether through the use of algorithm,
mutexes, locks, monitors ... but only on a very small scale.
Let's say the data structure is a stree, only the reading and writing operations of a
single node need to be atomic.

Here we have a  concurrent entity which wishes to implement an update on a node. 
Leaf or node with children, does not matter.
It firsts copies atomically  the part of the data structure concerned by the change (a node in this example).
It then perform the modification it wishes on the copy (updating a value changing a child, even deleting the node
and making all children unreachable).
Then it reintroduces the modified part, again atomically.

After the part has been re-introduced other concurrent entities navigating the structure are now either in one of three state:

- not yet reached the part modified, they will see it already updated when they encounter it if they do.
- was just about to encounter the part  our concurrent entity was updating but had to wait for the lock while our entity was writing.
    Just like the not yet reached part.
- On a part related to the changed part but beyond it  (for example a child of the updated node wether direct child or very down the tree):
  + the change either does not affect their work and all is good (example of a value update inside the node)
  + they are now unknowingly working for nothing (example if parent node was deleted and child were not rattached)
    their work will be lost but it is deemed acceptable.
    
One small detail to manage though is when to free part of the data structure
which are no longer reachable by newer concurrent entities (i.e parts are old).
They are maybe still being browsed by older concurrent entities who weren't aware of the change as they had
already passed the modified part of the data structure when it was updated.

One solution is to have **a grace period**. If you know how much time concurrent entity can spend at maximum in any part of
the data structure, you can simply wait until this time has elapsed. You are now sure that all concurrent entities
which had to work are now no longer browsing the part which is about to be deleted.
You can thus delete it safely.

This data structures trades space efficiency  for faster speed
This data structure is very used in the linux Kernel, and in my opinion 
has it's place in databases system and some AI training shenanigans.

### Scheduling
Making process internal and processes compete and cooperate with one another is good and all,
but CPU time is not a free-access resource, it is the operating system that allocates it.
Enter the world of scheduling. This subject became a bit archaic for todays user confort on a regular pc,
but it still plays a significiant role in smartphones, IOT and critical systems.

#### CPU bound and IO bound tasks
when talking about scheduling, it is important to first notice something,
all tasks aren't created equally.
Some tasks will spend a lot of their lifetime crunching data 
with relatively little IO in comparison. These tasks which benefit 
the most from more CPU time or a faster CPU are called **CPU-BOUND**.
An example of IO-bound task could be a physical simulation,
where the input parameters fit in a little file,
but the calculations are quite complexe.

On the other side we have tasks whic spend the majority of their lifetime
waiting for IO operations to happen, wether it be network,user action,disk ... .
These tasks are called **IO-bound**. They will not benefit very much 
from more CPU time or a faster CPU, the main thing that speeds them up is 
alloting them CPU time just after an IO they were waiting for has finished.
By doing so, the task can immediately react and start doing something else.
An example of IO-bound task could be a disk shredder, or a program sending
massive amounts of data through the network.

Scheduling algorithm comes in many flavour but first we have to discuss,
how the operating system behaves when a task has used up it's alloted CPU time so far.

#### Cooperative scheduling
The scheduler decides which process has a right to CPU time and starts it.
It is up to the process then to voluntarily yield to allow the sheduler to run another process.
Alternatively it can also yield automatically when waiting for an IO.
Mainly seen in embedded and critical applications where a tight control loop
is made on what is running at any given time because if  a bugged / rogue process
came into execution, it could hold up the CPU forever and stall the whole computer.
Embedded systems have a hardware component called a Watch dog to rest the hardware
in case such thing would happen, but this is far from optimal.

#### preemptive scheduling 
The scheduler decides for how long each process can hold up CPU time.
Once the time is up, the CPU is forcibly taken away from the process
and given to another one, according to the used scheduling algorithm.


#### Scheduling in an environment 
Scheduling algorithm do not operate in a vacuum,
they are dependant on the kind of environment they take place,
and the accepted balance beween responsiveness and "stability".

####  Process turnaround Time  and mean process turnaround time
One way of measuring performance of a scheduling algorithm is to study the Mean Turnaround Time.
Turnaround time is the time needed by process when it first becomes ready until it has completed it's 
task and can be discarded from memory.
It includes time spent waiting to be alloted some CPU time as well as time spent executing.
The mean turn around time is the sum of turnaround timmes of all process, divided by the number of process.
This is only A way and not THE way of measuring scheduling algorithm performance,
because sometimes other criterion also have importance like responsiveness (see the interactive environment example)

#### Responsiveness
Responsiveness can be defined as the duration between the moment a process is forced to release the CPU,
and when it gains again control of it.

##### Batch work
No human interaction, CPU and IO bound operation are possible.
Longer time between process switch, better turnaround time because fewer time lost on context switching.
Worse responsiveness as one process can be running for a "long" time.

##### Interactive environment, with a human on the other end of the line 
There is a human interacting with process at work.
A human which can get easily bored, and maybe jumps around doing multiple things.
Here we aim for more frequent process switching, giving an overall
worse turnaround time but better responsiveness.

##### in a realtime system.
Highly  specialized environment when task must finish within tight time constraints,
or else ... .
Sometimes events can be predicted in advance and thus the selection of certain task
will be dependant on this.
Scheduling take advantage of events coming at a regular time interval is called **periodic scheduling**,
and if events are random it is then **aperiodic scheduling**




#### First Come First Served
Simplest algorithm to implement. 
Non preemptive it has some  major flaws, it  does not
give way to a short task if it comes after a very long one 
even if it could be completed very fast and then reduce the number 
of pending task waiting for CPU time.


#### Shortest Job First and Shortest Remaining time 
Typical of bacth work evironment as time of execution required to complete a task
must be known in advance.

The difference between shortest job first and shortest remaining time is that
in shortest remaining time, if a short task comes but a long task
has already being executing from a while and would finish in less time than what is needed
to complete the short task, the long task will continue to execute until completion.


#### Round Robin Scheduling 
Really First come First served but preemptive,
after a process has used up it's alloted time,
CPU is withdrawn from it  and said process goes to the back
of the queue, until CPU is given to it once again.
Here all process are equally important


#### Priority Scheduling
Unlike round robin, Priority scheduling does not assume that all process are equal.
They are instead segregated in level of priorities and process with higher priority 
are either given more CPU time, more frequently, or both.
One main issue with this kind of algorithm  is to ensure that low priority
process don't starve of CPU time.


#### Guaranteed scheduling and the "completely fair scheduler"
Simple Guarantee "your process will get as much CPU time as everyone else"
Just pick the process which had so far the least amount of execution time alloted
and give it some CPU time. Rinse and repeat everytime you need to choose a process.

#### Lottery Scheduling
Non deterministic scheduling, each process has one or more "lottery tickets".
Every time CPU time slice must be alloted, a ticket is picked and the process
holding it is granted the CPU time.
This system offers priority, as the more "tickets" a process has, the
more he is likely to get a CPU time slice.
This system offers also "priority boosting"
as other process of a pool can lend their ticket to a process of their choice
to increase temporarily it's change to get picked and run.
For example a master process and multiple workers process, when one worker is finished,
it can send it's tickets to the master process in the hope of getting more work or an answer.



Some words of wisdom before going into the next chapter,
"Threads are meant to cooperate. Processes are made to compete"

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
