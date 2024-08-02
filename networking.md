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

##### Piggy Backing
If the receiver only send acknowledgements of received frame to an emitter on a separate simplex channel,
a lot of available bandwidth is lost.Indeed a full simplex channel
is used to only transmit small acknowledgments. If the acknowledgments are instead sent alongside some data, lost bandwidth
is reclaimed. One caveat though, you need to be ready to send acknowledgements if no data for the emitter is presentend in a timely fashion,
otherwise you run the risk of timing out the emitter and having it resend the frame for nothing.
This  practice is called piggy backing. 

##### Sliding Windows
Sliding windows protocol allows more flexibility in the sending and receiving of frames.
Multiple frames can be "in flight"  between the sender and the receiver at a given time
allowing for a potential better use of the bandwidth available.
Sender and receiver agree on "a window" of allowed frame numbers;
The sender can send frames as fast as it wishes as long as it does not overshoots the end of the frame.
The reicver receives the frames and then transmits them to the network Layer,  IN THE CORRECT ORDER.
If some frames are corrupted, two possibilities arises 
- the receiver  acknowledges all the frames that it received correctly regardless of their continuity with the frame   number. By doing so, the sender will understand that it needs to re-send only the corrupted frames. This is **selective frame rejection.**. Useful when you have lot of memory to hold frames while waiting for the missing ones.
- The receiver acnowledges the frames that it received correctly until it breaks the continuity of the frame number
  the sender will re-send all frames after this number, even if some were correctly received by the receiver
  (the sender can't know that.) This is **Global Rejection, go back n frames**. Useful when the receiver has little    memory for frames.

Regardless of the chosen method, the link layer  always tranmits the data IN ORDER to the network layer.
The Sender and the receiver then agrees on moving on to some other allowed frame numbers.
and they deny the older ones. They "slide the window" further.
If a modulo system is used where 
In a system where the sender sends only one packet, then waits the acknowledgement of the receiver 
before sending another packet, the window is of size one.


### MAC WiFI  and ADSL
### PPP 

## Media Access Control Layer
Protocols in charge of managing how multiples entities access a shared single channel of communication on a physical  layer 
are a sub-part of the link layer. They are called Medium Access Controll Protocols or MAC.

To study the sharing of a canal of communication,
We will lay some  properties which must be kept in mind while studying the following algorithms,
they limit the domain of possibilities and  efficiency when  they are altered.
- Each entity is independant from  other entities: and has it's own will wether it wishes to  emit traffic or not.
  while emitting, it cannot receive traffic or do anything else. This hypothesis does not require explications.
- Single Canal : All  communications happen on the studied canal, where entities send and receive messages. If it wasn't the case,
  synchronization would be much easier.
- Collisions of frames are witnessable : entities can detect that two or more frames from different entities are on the same channel at the same time,
  jamming each other. This is hypothesis very important, as protocols must adapt heavily when this hypothesis changes.
  It is generally True for cable-based links and false for Over The Air Electromagnetic waves based links.
- Time can be  either discreet or continuous : Time can be alloted in slot where an entity has or hasn't the right to emit (discreet)
  or it can be in the countrary thought as a continuous flow (continuous).
- Listening or disregarding the state of the link before emitting : entities can listen the state of the link before emitting, or completely disregard it.

### ALOHA
Developed  in the university of Hawaii, it is the first publicly demonstrated protocol of a wireless packet
network. In this setup client entity emits data as they wish, to a central computer which is charged to broadcast
the packet to the entirety of the network. A client entity knows it's message was correctly broadcasted if it then hear it back from the mother station.  Time is continuous and the state of the link is disregarded when emitting, consequently many collisions may ocurr and  the efficiency of the link when a great number of users is present is quite low, only around 16 %
of all messages are correctly transmitted. Later the time was splitted into slots, reducing the possibility for collisions
and doubling the rate of correctly transmitted messages to 36%.

### CSMA
Carrier Sense Multiple Access is a protocol which exploits the initial foundation layed by ALOHA,
while also benefiting from the fact that it was designed for wired networks. 
On a wired network, entities can listen for traffic on the entirety of the link unlike wireless stations.
Indeed, in a wireless network having the following Topology, A=====B=====C, if A and C are only in  range to talk to B,
even if A listened while C was already emitting, A would not hear anything as it is  too far out C.
then A would emit and walk on C  when it's signal reaches B. This problem is called **the problem of the hidden node**. That's why aloha does not listen for already existing traffic.  In a Wired network with the same topology, A and C can both hear themselves (maybe with a delay bigger than to B), and consequently reduce the number of accidents if they hear for each other before emitting.
This is exactly what promotes CSMA. If nevertheless a collision happens, stations wait a random delay before
hearing again, then retransmitting their messages, ensuring that they do not keep bumping into each other indefinitely.
This method can attain around 50% of correctly transmitted messages,  better than  ALOHA. 

Nevertheless collisions can stil ocurr, for example if multiple entities wait for the link to be already empty before emitting
they will all start emitting at the same time. An enhancement to this, brought by "non-persisting CSMA" is to perform not one but two checks of the emptiness of the link :
Check if the link is empty, if so wait a random amount of time then listen again, if hte link is still empty, emit right away
otherwise repeat the process.
This enhancement runs the risk of slowing down the network a bit, although it can reach up to 80 % efficiency !

#### CSMA/CD (Collision Detection)
A particular version of CSMA which can detect collisions as it transmits, thanks to the link hardware, and thus
end the frame transmission early if it detects a collision. Used in early ethernet networks.

#### CSMA/CA
A particular version of CSMA where various entities collaborate to take turn in occupying the link.
Unlike CSMA/CD this protocol does not require particular link hardware properties to work.
- In  the bitmap protocol, a "table" passes where each entity notifies if it wishes to transmit a frame.
  afterwards each entity transmits it's frame before waiting for everyone which registered in the table To do the same.
  The entitity with the biggest adress emits first. The table then circles again.
- In the Token Sharing protocol, a token travels among the entities. When the entity has the token it can emit a  frame.
  Afterwards, the entity sends the token to the next entity. Entities are logically arranged in a loop
  (it doesn't need to be the case at the physical layer)
- In the binary counting protocol which works if the transmission time is negligeable, when the deciding phase begin,
  every entity which wishes to emit a frame broadcasts it's adress bit after bit, starting with the largest bits first. The entity with the biggest adress 
  emits it's frame, before the whole link enters a new adress emitting phase.


We have this far seen two types of protcol:
- those which manages collision gracefully, like CSMA/CD or ALOHA : They work well when a link is not very used
- and those who avoid collision like CSMA/CA. : They work well when a link is very used, otherwise they incurr useless delay

Another familly of protocol exists, "the best of both worlds" : protocol with limited contention.
Entities are split in small groups and compete against each other only inside of the group,
the groups have a predetermined order of passage 


### MACA (Multiple Access Collision Avoidance)
We have talked so far of protocols more tuned for wired networks. Here's one for wireless networks.
An  entity A which wishes to emit sends a small frame requesting to the target B the right to talk **RTS** or **Request to Send**.
The target B answers positively **CTS** or **Clear to Send**. The entity A now knows it has the right to emit it's frame. 
this situation mostly solves the **hidden node problem** as another entity C too far to hear the RTS of A will still be able to hear the 
CTS of B and thus, know it must not talk. In the eventuality of B receiving multiple RTS at the same time which would become jammed,
it does nothing. The emitters of the RTS will understand that something bad happened and will retry after waiting an random interval of time.

This protocol however does not solve every problem, see this network topology A---B---C---D
B wants to emit to A and C wants to emit to D 
B sends RTS to A, C will hear the RTS of A and will not talk to D even though it totally could as C cannot jam A when emitting.
this is the **exposed node problem**
One solution is that if C does not hear the CTS of A nor knows A, it can assume that A is out of it's reach and emit to D.
Word of caution though, that C does not stop B from emitting by jamming the CTS sent by A to B !


### Ethernet
This protocol which combines functionalities of  OSI layer 1 and 2, is named after luminous aether, a substance which was supposed
to be the medium used by electro-magnetic waves to travel in space, before discovering that they can travel through vacuum.
It is defined by the norm IEEE 802.3 .
Eternet  exploits CSMA-CD for MAC with exponential backoff.
Exponential backoff means that when multiple collisions between entities occurs, the maximum number of slots entities must potentially wait before trying to emit again (they 
pick randomly a number in the interval ) rises exponentially (usually a power of 2).

With the rise  of the power of electronics alongside the fall of it's price, ethernet hubs, 
which repeats the signal it receives along all of it ports, making a network behave like a single big ethernet cable
were replaced by ethernet switches, which tranmits ethernet packets only to the relevant port, segmenting the network and limiting it's congestion.
This has been the downfall of point to many ethernet, toward a point to point architecture (even if the other point is a switch and not an end device !).


If the first Ethernet norm provided 10 Mbit/s bitrate, standard have evolved and now ethernet exists in flavor of 100 Mbit/s  and 1 Gbit/s (40 and even
100 Gbit/s ethernet exists but they currently used in datacenter and telecommunications operators backbones, and even faster ethernet is currently developed).
All these standards are backwards compatible.

Ethernet is implemented on twisted pair copper cables (improperly named RJ45) and on fiber optic.


### WiFi
It is defined by the norm IEEE 802.11 .
Initially with frequencies in the domain of IR waves  and 2.4 Ghz ( in the ISM band),
the Bandwith spread with updates and now also has some right in the 45 and 60 Ghz bands.
CSMA/CA is exploited to split the avaiable slots among stations. Since WiFi is very used by nomad devices,
with limited battery life, some thought has been given in power saving, for example  
- the AP emits a heart beat packet at a fixed interval, detailing network status,time, and among other things, a network map specifying if the AP has a packet
  for a device in the network. Knowing this, a device can notify the AP that it goes sleeping, requesting all packets be saved by the AP until it wakes up.
  The device can then only wake up for heartbeat packets and check if the AP has a packet for it, if not it can then go to sleep until the next heartbeat.
-  a device can lay an agreement with the access point that the Access Point  will keep traffic for the device and send it only after it has received data from
the device.

### Bluetooth
First available to the public in 1998, Bluetooth own it's name and logo to Harald Gormsson, a Danish and Norwegian King.

The wireless architecture of a bluetooth network consist of 1 master node linked to up to 7  active slave nodes and 255 sleeping, in a radius of 10 meters.
Multiple master nodes can communicate together, usually linked by a bridge node, a slaved node shared by the two masters.
Communication is centralized through the master nodes, two slaves cannot communicate directly among themselves, they need the master as an intermediary.
Bluetooth does not respect the OSI model, it is made of various "profiles" which dictates how  the whole protocol will behave, depending on the application exploiting the link provided by bluetooth. This is a clear violation of the OSI model / of the layering principle where a layer
focuses itself on providing a service and expressing needs to provide this service, regardless of the intended use for the protocol.
Bluetooth was built with the idea of a very low implementation costs which partly explains design choices.

### Commucation at the data link level
A network **Bridge** is a device (either physical or logical) that interconnects two networks at the link level. Ethernet switches are an example of bridge, here they
are bridging two ethernet networks. An ethernet hub is not an example of bridge, as it does not link two different ethernet network but rather unifies them into a single one.
Ideally, bridges when inserted should automatically determine where to route packets without configuration or update among any equipment in the network.
This is possible thanks to two algorithms : Learning Bridges and Spanning Trees.

#### Learning Bridges
When a newly plugged bridge receives a packet from an emitting  device A for a receiving device B , it behaves as follows :
- If the emitter A and the intended receiver B of the packet lie on the same port of the bridge
  (for example if the bridge's port is linked to other devices on a bus or a hub)
   the bridge drops the packet, an intervention of the bridge  is not needed here.
- If the receiver B lies on a known different port than the emitter A, the bridge emits the packet to the correct port.
- If the bridge does not know on what port lies the receiver B, it emits the packet on all of it's port except the port where the packet originated from, it "floods" it's port.
Moreover, it takes good note of the date and  the port from which originated the packet of A , it now knows that A is on this port.
Every few minutes, stale entries in the table of what devices lies on which port is freed from old entries, so if A is unplugged on another port ,
the change will be automatically acknowledged within a few minutes. The Bridge is learning backward.

This algorithm has a flaw, let's imagine two bridges linked together via two different ports, in case one physical link breaks.
When the first bridges receives a packet for a recipient it does not know, it will emit it to all of it's port, excepted the on it received the packet on.
The other bridge, will  receive the packet from the first bridge on a port, and if it also does not now where the recipient lies, will send it to all it's port
except the one where it received the packet. Now the first bridge will receive the packet from the second bridge, and since it sill does not know  on what
port to send it, it will send it everywhere. The second bridge will pick it up, rinse and repeat, the packet will loop forever in the network,
and the more the shared port between the bridges, the worse. This is called a **switching loop** (**routing loop** describes the same phenomenon for protocols of layer 3 not 2).
To remedy to this problem, backward learning is peered with spanning trees. 

#### Spanning Trees
All Bridges run a distributed algorithm to create a tree (algorithmical structure, a graph WITHOUT any loop)
which describe to each bridge how to reach other bridges and what port to desactivate to not create a **switching loop** while still servicing all  devices.
This algorithm is thoroughly defined in the norm IEE 802.1D .

### Virtual Lans
For many reason, you may want that  architecture at the Level 2 Link layer  differs from the real architecture (Level 1 physical layer).
You can use VLAN to create "virtual cables" which tunnels the traffic according to your wish.
VLAN packets are defined in the norm IEEE 802.1Q .
For the following explanation, we will consider that VLAN are tagged using colors.
Bridges can be configured beforehand to know what VLAN are available on any given port  (or auto-detect and configure themselves at runtime).
When they receive a packet, this packet is  tagged with a VLAN color (or not tagged) at all.
From this situation, the bridge can perform 3 actions
- Add or remove the color of the packet before transmitting it to a port with the same /no color (for example if the packet originates or is for a device that does not know
  VLAN protocols)
- Route the packet to a port with the corresponding color (flooding all port having  the same color as the packet if necessary to find the receiver)
- Drop the packet as no port of the color of the packet is configured  to be legally  emitted from any of the port of the hub

Please note that two bridges linked together through a link can affect various color to their end of the link,
for example if bridge 1 is linked to only gray vlan devices and bridge 2 is linked to gray and white vlan devices,  the following is valid :
Bridge 1 GW ------ G Bridge 2 
Here bridge 1 is able to forward any packet tagged Gray OR white to Bridge 2 , But Bridge two may only forward to bridge 1 packet tagged gray,
packet tagged white will NOT be forwarded to bridge 1. 


## Network Layer 
The Goal of this layer is to route packet from a sender through intermediaries to a receiver. The sender and the receiver can be 
separated by multiple networks and devices, yet the network layer is to bring packets to their destination regardless.
It uses the link layer to send packets to the correct closest intermediary which is one step closer to bring the packet to the destination
This layer offers the following services to a higher layer :
- routing
- 
- 

### packet routing versus virtual circuits
Two big  routing methods exists,
connection-less,
where packets of data are each being indepently routed. As long as they arrive to the receiver,
the sender couldn't care less about the path they follow (he can't specify it neither).

connection-full or virtual circuits, where all packets from a sender to a receiver during a communication follow the same path. 
The sender must specify the path they have to follow.

Here is a comparison of virtual circuits versus packet routing :

- Establishing connection beforehand
   connection-full : Mandatory before emitting
   connection-less : not necessary
- Adresses management
   connection-full : the identity of the virtual circuit is known among each router
   connection-less : only the address of the sender and the receiver are known, embedded in the packet.
- Routing
   connection-full : the route is fixed at the start of the communication, all packets follow it
   connection-less : each packet can follow a different route, at the discretion of intermediary routers.
- What happens when a router fails
   connection-full : all virtual circuits in which the failed router took  part are inoperative.
   connection-less : only packets managed by the router at the time of failure are lost 
- Guarantees of Quality of Service
   connection-full : Easy to guarantee, ressources only have to be allocated before-hand
   connection-less : hard to guarantee, mumbo jumbo of  heuristics, algorithms and packet tagged with a priority flag
- Overflow control
   connection-full : easy to guarente, ressources have been pre-allocated
   connection-less :  hard to guarantee, again algorithms and heuristics hard at work 

### Connection-less Routing algorithm 
The One of the  objective of routing algorithms is to determine the best path for packet to follow.
Depending on your need, the best path is a varying notion, do you want the best bandwidth ? The lowest latency ? The shortest
geographical distance because you pay more if you use more infrastructure ? The smallest number of crossed devices to limit network congestion ?

It all starts at the same point though : finding the shortest routes in a (possibly valued ) graph representing the network devices and links between them.
For any given device, we want the shortest route  from anywhere toward this device. This takes the form of a Directed Acyclic Graph, a Tree.
We luckily have few algorithm to solve this problem : for example the  Dijkstra Algorithm and the bellman-Ford Algorithm. The Dijkstra algorithm solves all shortest route from anywhere toward anywhere for all nodes in a graph.
You also need that all router are agreeing together on what is the shortest path, this is called **convergence**.

#### Flooding routing
The simplest, almost naive algorithm. Yet one of the most robust, does not necessitate any prior knowledge of the network.
When a packet is received, it is duplicated and sent to all links except the one it came through.  Measure should be taken to avoid
routing loop where the same packet circles around a number of same router indefinetly, for example a life expectancy for the packet taking 
the form of a decreasing number of  allowed crossing, or a sequence number. Also Useful if you need to broadcast  data 
to all nodes of the network. 

#### Routing by distance vector
In this algorithm  (also known as the Bellman Ford-Algorithm ) each router maintains a vector
of the shortest distance required to route a packet from itself to a destination, alongside the neighbour to which forward said packet.
This algorithm in it's basic form has a regrettable flaw, if  good news, as a new shortcut appeared which speeds up the routing, travel fast among the network.
Bad news on the other hand, like a router died and all traffic must be re-routed elsewhere travels slowly among the network.
Indeed let us take the following network topology : A -- B  -- C -- D.
If the link between C and D is broken, C will anounce that it no longer knows how to go to D, C has an infinite number of jump toward D.
The problem lies in the fact that B will see this, and  sees that A broadcasts that it knows  a way to reach D in 3 jumps.
Not knowing that the route that A broadcasts is stale and goes through B itself,  B will then update it's distance vector and set A as the go-to neighbour to reach D.
A will see that B increased it's distance and will consequently update it's own vector to take the change broadcasted by B into account.
The distance will slowly rise to infinity, when the network will finally understand that D is unreachable, but this may take some time.

Enhancement have been proposed such as split horizon and reverse poison
##### Split Horizon 
For any node N able to reach node D with a shortest path going  through an Interface I 
any change in distance from N to D should not be broadcasted by N on the Interface  I

##### Reverse Poison
For any node N able to reach node D with a shortest path going  through an Interface I  ,while I is the interface of the shortest route,
N broadcasts on I that the shortest distance from N toward D is infinite.

Note that Reverse Poison does not work in the following networking topology :  A linked to B, A linked to C, B linked to C , C linked to D, link between C and D broken.
Here A B and C  will in turn believe that  one of the two other nodes knows how to reach D. 

#### Routing by link information 
- 1. Discover all neighbours  and their network adress
  If multiple routers share a link (they are on a bus for example) create a "ghost router" to make
  routers connected in point to point. One of the router on the shared link will act as itself and the ghost router.
- 2. Give a cost to reach each neighbour
  Depending on what matters on the network, latency, bandwidth ...
     
- 3. Broadcast a compiled version of all of what you have discovered to all your neighbours, and receive similar packets from your neighbours
  it should carry a timestamp, your adress, a list of your neighbours and the cost you have affected to each of them.
  To avoid overflow of the network by information packets each packets contains a sequence number.
  At any time when an information packet is received by a router, if the sequence number of said packet is lower than the
  highest  previously received from the same sender, the packet is dropped, as it is a stale duplicate. Otherwise it is broadcasted to all links except the one  where it came from. Packet AND their information can also become stale from old age, so if a router restarts or a corrupted sequence number goes unnoticed, or a packet starts looping around for any reason, after  a while the informations it broadcasted wil become stale and be removed, and the packet will no longer be broadcasted.
The affected router will be again able to emit information that will be  taken into account by other routers.

- 4. process the smallest link toward each device

This routing method is used by some industrial grade protocol 
- Intermediate System-Intermediate System
-  Open Shortest Path First

#### Routing Hierarchy 
The problem of routing by link information is that when the network gets very large,
processing Dijkstra or Bellman-Ford gets costly. Moreover, in a very large network,
failures are bound to happen somewhere, triggering frequent, costly, recalculations.
One solution to this is to split routers into clusters. Each router knows the complete intricacies of the cluster it belongs too,
as well as the go to routers to reach when you want to send a message outside of your cluster, those are "gateway router".
Thanks to this repartition, routers don't need to track every change in the network.  

#### Broadcast Routing 
When a host needs to be able to broadcast data among all devices in the network, the **Reverse Path Forwarding** algorithm
comes to our help. When router receives a broadcasted packet, it checks the link from which it came from.
If this is  the same link as the one this router would have 
used to send a message to the emitter of the broadcasted packet, it means that the broadcasted packet probably came from the best route possible,
and thus it should be broadcasted to all other links. If this is not the case, then the packet probably came looping around after 
riding on the best route. It should be consequently discarded and not broadcasted again to avoid loops.
This algorithm takes for granted though that link are bi-directional and are ranked symetrically from the sender and the receiver perspective.
If this is not the case, the algorithm does not work at all.


#### Multicast Routing
Multicast is a very particular broadcasting system. In multicasting, you want to transmit a message to many nodes, yet not all of them.


#### Anycast Routing 

### Overflow Management

### MPLS , connection-full routing 


## Transport Layer 

The Goal of this layer is to
It uses the XXXX  layer to 
This layer offers the following services to a higher layer :
- XXXX
- XXXX
- XXXX 


## Application Layer

## Security
