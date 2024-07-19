# Networks 6th edition
Andrew Tanenbaum, Nick Feamster, David J Wetherall

## Introduction

### Network sizes 
#### PAN(Personal Area Network)
Network which allows devices in very close proximity to communicate together ,
NFC, Bluetooth

#### LAN( Local Area Network)
Devices are located in close proximity, same room, same house, same building
WiFi, Ethernet Cable, Power Line Communication.
There also exists VLAN which allows to separate traffic on a same Physical LAN 
into multiple "Virtual" LANs.

#### MAN (Metropolitan Area Network)
Network having the size of a city
example : Cable TV which spanned across a whole city
WiMax ( not well known)
fiber optic spanning through city 


#### WAN ( Wide Area Network )
Country or even Continent Sized Network
Sonet link
Fiber optic Country backbone ?
Starlink

### Brief History of networking  (or the history of internet)
#### Arpanet
The first Wide Area Network, spanning across the United states of America. 
Ordered by the Arpa, the ancestor of DARPA (Agency which decide in what defense project invest US' administration money )
Linking together 4 universities in  December 1969, 34 in September 1972.
Packet switching method  (that is data is separated in chunks (packet) before being shared on the network to be recomposed by the receiver)
was already implemented. It was composed of 2 types of machines : 
hosts which wanted to  communicate with other hosts (to retrieve data or open a distant session)
and IMP (Interface Message Processor) which where underpowered computers with the sole purpose of 
transmitting around packets of data emitted by a host.

#### NSFNET
Another network based on the success of Arpanet in the Academic world, with the main purpose
of making Super computer computing power accessible to more universities.

#### Internet
The internet as we know it more or less appeard in 1989 With the apparition of Commercial ISP in the United States of America.
the IP protocole suite which is a fundamental part of the Internet was introduced in January 1983.
Today a packet navigating will go through the following infrastructure

1 Emitted by the ISP's box of the client
2  ISP's client Point of Presence aggregating traffick in his neighbourhood.
3 Internal Network  of the ISP 
4 Backbone (Massive networking infrastructure spanning across long distances)
5 IXP (Internet eXchange Point), where two or more ISP are interconnected  to exchange packets 
And then repeat the same process in the other direction to reach the destination.
6 Optional : other backbone transition

Note : The ISP of the emitter and the receiver may not be directly interconnected by an IXP,
in this case, packets will transit by one or multiple intermediary ISP (which will make pay the transit to the ISP).

As you can see, these IXP have a key role to play in delivering packets,
that's why content provider  like Amazon, Netflix, Google ...  and data center like OVH or Cloudflare,
link themselves to these to provide faster service.

### Brief Aparte : Cellphone network Version
####1G 
Calls were transmitted in analog fashion, text message weren't even possible ! 
####2G
Calls transmitted in numeric fashion, text messages finally available
####3G
Internet accessible through cell network, at up to 42 Mbit/s Download speed
( 3G H+ DC-HSPA+) mode
####4G
up to 979 Mbit/s Download speed (4G LTE-Advanced Cat16)
####5G
up to 10 Gbit/s Download speed

###Objectives of A network Protocol
#### Reliability
A network must provide reliable service even in unreliable conditions
(spoiler alert, they are always unreliable).
Bits get flipped, protocols used by devices have a version mismatch, 
router dies,someone starts a microwave or a heavy current consuming device,
yet the network must keep offering it's service.
We find here problematics of 
- error detection
- error correction
- packet routing

#### Resource Allocation
Networks rely on limited resources,
wavelength travel only so far, can only fit so much,
routers can only process so little packet.
The Network must offer the best service possible 
within the limits of it's  allocated resources.
We find here problematics of 
- flow control 
- bandwith sharing

#### easiness of Evolution 
Network must not collapse each time you add or remove a small compoenent.
It must be able to withstand devices with various protocols and 
various rate of protocol adherence.
We find here problematics of 
- Layer model 
- Network interconnexion
- giving identities (i.e **address**)  to network devices 
- size evolution 

#### Safety
Network must not be diverted from it's purpose 
(sharing information under certain terms) to the new purpose of some
malevolent individual ( changing the terms with or without other knowings).
Here we find problematics of 
- privacy ( what I emit is only known by me and the recipient )
- identification ( Who am I and Who is my recipient)
- authentification (Proof that I am who I say and so is my recipient)
- integrity ( My message is not altered in any form) 


### Layering 

#### Basic definition 
To Satisfy the  easiness of evolution model, engineers have come up with the idea of "layering" protocols to make them  interchangeable.
The idea goes as follows, each layer represents a protocol. 
It provides guarantees to the layer above it (or the user if it is the uppermost), those guarantees are called a service.
It rely on services provided by the layer below it.
The same service can be provided by different protocols. 
(for example wiFi and low band radio both provide the service of moving your bytes from point A to point B without a need for a wire.)
Between two protocols of adjacent layer lies an interface which describes how data must be transferred between those adjacent layers.
This system is incredibly modular because each layer only knows about the layer above it and below it.

The work to replace a protocol with another used is limited to adapting interface above and below said layer.
For example an email app  does not care at all if the bytes of the email are sent through an ADSL connection,
a fiber optic, a satellite link ... . 
This is because the email app is at the top most part of the layer system, far away from the layer occupied by fiber optics / wifi ... . 
Complementary, fiber optics / WiFi will not discriminate bytes of a video or an email.


How does data navigate in this layer system ? From the upmost layer to the bottom and in reverse :
Lets say we have here data generated by our email app : \[EMAIL DATA\]
now the email gives it to the networking layer which is in charge of moving the email through the internet,
it determines the network adress of the receiver, the network adress of the sender, etc.
our data packet will now look something like this 
\[NETWORK HEADER\]\[EMAIL DATA\][\ NETWORK FOOTER\]
Now we send our data through a satelite link :
\[SATELLITE HEADER\]\[NETWORK HEADER\]\[EMAIL DATA\][\NETWORK FOOTER \]\\[  SATELLITE FOOTER\]

We see here what is called **packet encapsulation**.
The data of our email app is encapsulated between network data, which is itself encapsulated by satellite comm data 
With this example we also see that it is quite easy to replace the satellite link with for example, a fiber optic link 
without it interfering at all with the email app :
\[FIBER OPTIC HEADER\]\[NETWORK HEADER\]\[EMAIL DATA\][\ NETWORK FOOTER\] \[FIBER OPTIC FOOTER\]

Note : Here we suppose that everything could be sent in one big packet, but it is entirely possible 
that the data of the one layer is too big to be sent in one packet of an inferior in layer. 
In this case data will be cut in smaller subparts and later reassembled by said layer on the receiving end 

For example if the network decide to cut the email data in two parts, this will give us something like this :
packet one : \[FIBER OPTIC HEADER\]\[NETWORK HEADER\]\[HALF DATA\][\ NETWORK FOOTER\] \[FIBER OPTIC FOOTER\]
packet two : \[FIBER OPTIC HEADER\]\[NETWORK HEADER\]\[OTHER HALF DATA\][\ NETWORK FOOTER\] \[FIBER OPTIC FOOTER\]
It will be then the work of the network layer on the other side to reassemble the data before presenting it to the email application.

#### Connection and reliability
##### Connection
- Connection-full service locks resources needed to speak to it's distant counterparts and keeps them locked until the resource is released.
  even if no one speaks (but the link is maintained)

-  Connection-less service locks resources for the time required to emit the message only, freeing the resources immediately after

##### Reliability 
 Not to be confused with connection state
- reliable service guarantee the arrival of the correct message, in order in which it was emitted, or else throw an error
- unreliable service do not guarantee the arrival of the message, nor it's alteration state

Here lies a table  demonstrating various connection - reliability  couple
connection-full unreliable : VOIP (Voice Over IP)
connection-full reliable   : File Download (TCP)
connection-less reliable   : Cell phone  text message (SMS)
connection-less unreliable : UDP 



#### OSI Model
OSI model was designed after  TCP/IP and by different people,
with the goal of unifying the description of any and all networks,
regardless of technology employed.
it is composed of 7 distinct layers 
- Application
  Interacting with the final user : for example mail
- Presentation (obsolete)
  Ensure data sended to the remote application is understandable by it 
- Session (obsolete)
  Ensure the connection is remained between the two host
- Transport 
  Provides [# Reliability], flow control (not overflooding a slow intermediary ) and [# Connection] service
- Network
  Provides routing and adressing service across the network
- Link
  Ensures data is correctly emitted and received between direct neighbour,
  provides adressing service between neighbours ( != Adressing across network)
- Hardware
  Move bytes between emitter and receiver,
  manages radio waves, light waves, electric waves, etc.
  DSL/Color wave used in fiber optic/2.5Ghz modulation in  WiFi

This model has some flaws 
- It was designed when TCP/IP was already widely (for the time) implemented
  meaning strong leaning against it's implementation as a lot of money has already been spent
 (For a good norm to emerge the book states David Clark from the MIT the "apocalypse of the two elephant"
  A good norm is implemented after many research on a field has been done, yet before much money has  been invested, OSI was designed when TCP/IP was invested in under the form of router and implementation in computer  OS  )
- The layering is a bit strange, layer presentation and session which has been marked here obsolete
  provide almost no service, where network and link are too full 
  ( What do you get when you merge a gangster and an International Standard ?
  Someone who makes a proposal you cannot understand )
  The book states that the whole OSI norm height is about one meter height worth of paper
- First implementation were pretty bad, where TCP/IP implementation were in contrast good
- It felt paradropped by politics rather than built by researchers and developers.

#### TCP/IP Model
made of 4 layers 
Application
Transport
Internet
Link
This model also has some flaws 
- unlike OSI, implementation an specification are intermangled
  this does not fit a generic networking model. Good luck describing
  another network system with TCP/IP stack.
-  the link layer as designed in TCP/IP is way closer to an interface between
  the internet layer and hardware than a real layer
- the hardware and the link layer aren't separated

#### Hybrid IP/OSI (the one of the book)
OSI  provides a framework
TCP/IP provide a working implementation that roughly
let's merge them together !
from now on :

Application :
Any Program which use the network to communicate.

Transport : 
flow control and connection-based/ connection-less 
communication

Network :
How to communicate with entities which aren't direct neighbour,
routing,adressing

Link :
Cut a message into bigger and smaller chunks and organize the communication
between direct neighbours.

Hardware :
How to send  and receive bytes  on a physical medium

### Standards and ethics 
#### Standards
##### Norms
Norms are ratified by normalization organism, recognized internationally.
They define how different equipement interoperate when respecting the norm,
and **nothing more**. This helps keeps competition for technology enhancement,
while simultaneously ensuring different devices will work together.

##### Standards
Standards or "norms de facto" are practices that have reached 
consensus among the industry, without having beeing formalized in norms.
Usually, widespread standards are one day or another ratified into a norm ( for example HTTP).

Various Normalization and standardization organism : 
UIT  : International Union of Telecommunication 
Ageny of the united nations for telecommunication

ISO  : International Organization for Standardization
World Wide  NGO promoting International standards.

ISOC : Internet Society
American Non profit promoting the use of Internet.

IETF : Internet Engineering Task Force 
Non profit developing technical standards for Internet.

IEEE : Institute of Electrical and Electronics Engineers
Oldest professional association.
Promotes norms and research for electronics and electrics.

W3C  : World Wide Web Consortium
International Organization promoting Standards for the 
world wide web.

ICANN : Internet Corporation for Assigned Names and Numbers
NGO responsible of maintaining name spaces on the web.

#### Ethics

##### Net Neutrality 
- No blocking content
- No slowing down connection
  (for example if your customer uses another streaming service thant the one you promote)
- No favoritism among packets
- Transparency on any measure that would infringe one of the rules above


## Physical Layer

Note : As I'm no electronical engineer, 
this part really does not interests me and I've felt free to oversee many pages about the physical Layer.

### Terminology
#### simplex
Type of network link where there is 
one emitter, and one receiver.
The emitter can only emit, and the receiver can ony receive.

#### Half duplex
Type of network link where both participant 
can both emit and receive, but only one at the time 
(when one is emitting the other can only be  receiving and vice-versa).

#### full duplex
Type of network link where both participant 
can both emit and receive simultaneously.


### Means of communicating

#### Magnetic bands 
A an LTO-7 magnetic band can carry 800 Go of data.
A box of 60 by 60 by 60 centimeters can carry one thousand of those,
giving 800 Terabytes of data.
Such box can be sendby express mail in 24 hours anywhere in europe 
giving  a bitrate of almost 10 Gigabyte per second,
if the destination is only a mile away you have now a bitrate of more than
200 Gigabyte per second.
This, of course, provided that you read and write multiple tape at the same time,
otherwise your chokepoint would be the R/W speed of those tapes, 300 megabyte/s.
Never underestimate the bitrate of a semi-truck full of magnetic tapes.

#### twisted pair
Twisted pair of two copper cables. 
They are twisted to minimize their electromagnetic influence on each other.
Most common use is in telephone lines. 
Ethernet Cables are also using twisted pairs cables, made various number of  pairs of wires.

#### coaxial cable
Cable with a copper body, shieled with metal braid,
the whole in a plastic protection. Very good noise tolerance,
allowing bitrate of Gigabit/s

#### optical fiber
Cable made of glass itself wrapped in plastic, focusing a beam of 
light or laser to convey data.

It is lighter, more chemically stable, cheaper and offers far greater bandwith 
than other copper-based cables. 
There is far less risk of eaves dropping as there is no electro-magnetic noise generated
and the attenuation of  signal compared to  copper cable 
is far lesser.
It cannot be bent as freely as coper wires though, otherwise it will break.

#### electromagnetic waves
The use of electromagnetic waves is tightly regulated around the globe.
States have sliced the spectrum and sell parts of it for it's usage by 
industry or keep it for state affairs. Other slices are publicly 
available for the general public, like the Industrial Scientific Medical (ISM) band 
(where we find among other things, wiFi) or the radio amateurs slices.
Here an example of such spectrum slices :
https://en.wikipedia.org/wiki/File:United_States_Frequency_Allocations_Chart_2016_-_The_Radio_Spectrum.pdf

Some frequency are particularly useful, as they bounce on the ionosphere and can be heard
at far away distances around the globe. In some instances, the moon can even be used as a reflector !
Even by amateurs radio !
This is called Earth-Moon-Earth communication.


##### Radiowave

Easily generated they can reach a remote emitter located far away,
regardless of the of absence of a medium (they propagate in vacuum)
or it's presence (depending on frequency, they can propagate through walls and objects ).
Some frequency allow to exploit earth curvature and ionosphere as a reflector to 
extend range. 

##### Microwave

Harder to generate, they can be focused in a beam,
providing a better signal over noise ratio.
They are also absorbed by water, which is very convenient if you are building an oven or a meteorological radar,
much less if you try to transmit data in a rainy day.

##### Infrared
Easy to generate, (you can buy freely emitter and receiver on internet for a few bucks)
they don't traverse objects and have quite a short range.


##### light 
An example of application laser and it's receiver placed further away.
Beware of meteorological generated interference
such as mist, fog, rain, and even heat which can generate mass of moving air disrupting the signal !

### Theory of data transmission
The french mathematician Jean-Baptiste Fourier in early XIX th century proved that 
any periodic mathematical function (that is, with a motive which repeats itself)
can be expressed in a (possibly infinite ) number 
of sinusoid function. 
Those decomposition are called "Fourier Series"
and are widely used in electronics among other things, when talking about signal transmission, wether analogic or numeric. 
Various frequency of a given signal on a given medium aren't attenuated over distance in the same way
and thus can distort this signal. The bandwith of a given mean to transport data characterizes the width of the band of frequencies
which aren't attenuated. **NOT TO CONFUSE WITH IT'S HOMONYM WHICH DESCRIBE HOW MANY BYTES CAN BE TRANSFERRED IN A SECOND.**

[...] Some parts uninteresting to me here are left out. They concern signal multiplexing and modulation.

### Commuted Telephonic Network

At the beginning of telephone networks, voice of the user was transmitted with an analogic signal,
from one end to another by linking circuit together;
The telephone of users were all linked to local dispatch centers which themselves were linked  by **arteries** to bigger and bigger dispatch centers, etc.
Those dispatch center links the caller and the called with electric cables so an electric connection is made.
This method is called **Circuit Switching**.
If this operation was performed at first by hand by human operators, technology stepped  in at one point and replaced them.
Later on, this method of transmitting was abandonned for instead  packet switching (the voice of the user is  digitalized and transmitted in small chunks, **packets** in a digital signal. If this was at first true only for the most dense and sollicitated part of the network,
it's "heart", it spread to smaller and smaller dispatch center until even reaching the home of the user thanks to the "DSL" familly of techonologies, which job was to find a way to feed as much digital data as possible on a copper line made for analog signals.

Consequently, in the beginning of the internet, the telephone lines were (and still are in many places in the world) exploited to
bring network to the masses.


#### Commuted Circuits versus Commuted Packets 
Here is a comparison between those 2 types of networks.
Full route must be determined before connection can be established
- commuted circuits : Yes 
- commuted packets  : No
  
Data packets follows the same route 
- commuted circuits : Yes 
- commuted packets : not mandatory
  
Data Packets arrive in order they are sent 
- commuted circuits : Yes 
- commuted packets : no guarantee
  
Failure of one of the link between the sender and the receiver stops the transmission
- commuted circuits : Yes 
- commuted packets : No
  
Available BandWith for communication
- commuted circuits : Fixed
- commuted packets : Varies with network congestion

Bandwith can be needlessly spent
- commuted circuits : Yes
- commuted packets : No

Congestion and subsequently wait time occurs 
- commuted circuits : When trying to access the network
- commuted packets : When using the network

Data can be transmitted at a later time  / with variable latency 
- commuted circuits : No
- commuted packets : Yes

### Cellular telephonic Network
Mobile phone networks work as follows:
An antenna (or a set of antenna) see the geographical space around it
split into small cells. Each of those cells will have 
a band of frequency assigned to it, on which cellphones will 
communicate with the antenna. On the same cell the band of frequency is split into channels where
cell phones can emit or listen for voice data  or configuration data. These channels are then split into a number of
timeslots which repeat themselves over time.  A cellphone must wait for its timeslot to emit data. 
3G is the first cellphone network to allow for data other than voice to be sent and received.
4G The core of the telephonic service provider is switched from commuted circuits to commuted packets,
voice is now also carried  through IP packets (VoIP)  alongside data. Faster Speed and crunching every last possible bits in the
existing frequency spectrum (also a bit widened)
5G exploits a broader frequency spectrum  and  smaller cells to allow for bigger bandwith (can be down to 100 meters per cell vs few kilometers per cell  for 1g !)



## Link Layer
The Goal of this layer is to allow two direct neighbours in the network to communicate efficiently.
It uses the Physical layer to emit and receives big chunks of bytes which assembled together mean something,
they are called data frames.
This layer offers the following services to a higher layer :
- separating flow of data in separate chunks in a  way  that allows other neighbours to make sense of them when they receive,
    even in a disorganized manner
- detecting and fixing some error in the frames 
- managing the flow of data to avoid network congestion on the physical layer.


### Frame 
In a continuous bit flow, multiple manners of slicing them into frames exists
- counting how many data bits will be stored in a frame and specifying it in the header of said  frame.
  The main issue with this technique lies in the case of  corruption of the number of data bits located in the header.
  If this happens, the data link layer will be unable to find the end of the current frame and thus, also the start of next frame.
  Desynchronization will occur. This is method is rarely used alone.

- Using a whole byte as a starting / ending flag delimiting the frames. The issue of this technique is that you must also allocate another byte
  called an escaping byte in case the byte chosen as a flag also appears as data. In this case, it will be preceded by the escaping byte,
  to make the data link layer understand that this flag byte is to be interpreted as data and not as a flag closing a frame.
  If the pattern of an escaping byte appears in the data, an another escaping byte is inserted before to tell that  the escaping
  byte is to be understood as data.
  This method is employed by PPP protocol.

- Using a pre-existing pattern of bit. For example you can declare that in the data flow everytime you see this pattern "11111"
  The next bit shall always be a zero and it will delimitate the end of a frame. The receiving data layer will understand that the
  last zero is to be discarded. When this method is used, the size of frames
  is dependent on the data, this pattern will be cut into five frames : "11111111111111111111111111111111111"
  while this pattern while fit into one single frame : "110000000000000000000000000000011111"
  This method is employed by the USB protocol.

- Asking the physical layer to send "illegal" bit patterns which are easily recognizable that they carry no data
  (strongly dependant on how the physical layer works)

### Error Control 
The physical layer is not perfect, errors can happen and the signal can be altered,
a few example of interferences sources  :
- wrongly calibrated receiver
- cosmic rays hitting electric cables
- Magnetic fields from other devices charging the electric cable ...

We need to have a method to detect/ correct error  in a data frame

We first need to characterize what form errors can take : 
-  one or multiple isolated bits can see their value  flipped
-  multiple bits in a row can see their value flipped 
-  A bit can be altered in a way  that the physical layer  can't guess their value, because the signal sent is illegal
  (which is good because you know the message has been wrongfully altered)

The type of error we want to protect against dictates the algorithm we will develop/use.

Then we have to measure how frames,(here binary words), differ from each other.
We can use the hamming code comes for it.
Apply a XOR function between the binary two binary words. In the resulting binary word 
- the number of bits with value 1 gives the hamming distance : how many bits needs to be flipped to go from
  the first binary word to the other and vice versa
- the position of bits with value 1 tells which bit needs to be flipped in order to do so.

The general Idea behind every algorithm of error detection and correction is as follows:
For a word of m bits (all data bits), r bits of redundancy are added, bringing what is transmitted to n bits.
a word of n bits can have 2^n variants. The trick is that the r bits aren't random but related to the m bits,
bringing the number of legal variants from 2^n to something lower. As such any pattern of bits received
lying in the illegal side can be rejected. The objective is that with clever use of the r bits 
the hamming  distances between one legal word and the other, noted d is big (an utopic word  d=n)
such that you need many bit flips (d+1) for an incorrect message to be wrongfully tagged as correct.
The goal is to maximise d while minimising r (and by doing so minimising n the size of the whole message)
so you have a good ration between data sent vs redundancy added.

Those algorithms guarantee you error detection up to x bits  (x depending on the algorithm) and sometimes they also offer
error correction of up to y  bits (y depending on algorithm  but always x > y).
They exploit polynomial, matrices, binary operations, and more generally, algebraic concepts.



#### Flow Control
The sender may send more data to the receiver than what it can handle. 
We need flow control to stop this from happening.
Here are some common measures :
- The sender numerotates each frame sent so  if the same frame is retransmitted it is not understood as new data  by the receiver
- The receiver emit acknowledgment to confirm that a frame was correctly received 
- The sender arms a timer each time a frame is sent, so in case a complete frame or acknoledgment is lost the frame will be sent again
  
And also, the sender can adapt to the speed at which the receiver is able to process data via :
- feedback based flow control : the receiver says how much it is ready to receive at a given time and the sender reacts accordingly.
- rate based flow control  : The sender constantly  guesses the maximum allowable flow  rate by  monitoring how many frames are lost at any given point,
  if many frames are lost, it slows down the flow, if no frames are lost, it increases the flow until some are.

##### Sliding Windows

### MAC WiFI  and ADSL
### PPP 

## Media Access Control Layer

## Network Layer 

## Transport Layer 

## Application Layer

## Security
