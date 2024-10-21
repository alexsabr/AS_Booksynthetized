
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
- No **paid** favoritism among packets (time sensitive traffic like video games or calls has usually priority) 
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
- routing based on packets (more common) or on virtual circuits (rarer)
- Congestion management and Quality of Service alongside Transport layer 4 
- routing regardless of number and technology of intermediate routers (tunneling)
- adressing is consistent, from LAN to WAN 

If you want to learn more about the architectural design principle of the network layer for  the internet,
read the RFC 1958 (only 8 pages !). 

### packet routing versus virtual circuits
Two big  routing methods exists,
connection-less,
where packets of data are each being indepently routed. As long as they arrive to the receiver,
the sender couldn't care less about the path they follow (he can't specify it neither  
(some connection-less protocol may allow this feature )). The routing decisions are made at each
individual router in "realtime".

connection-full or virtual circuits, where all packets from a sender to a receiver during a communication follow the same path. 
The sender must specify the path they have to follow (or it can be forced upon him). The path is agreed
upon in advance and then respected. Very useful when you have stringent  Quality of Services requirements.

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
- Congestion control
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

#### Routing by link state 
- 1. Discover all neighbours  and their network adress
  If multiple routers share a link (they are on a bus for example) create a "ghost router" to make
  routers connected in point to point. One of the router on the shared link will act as itself and the ghost router.
- 2. Give a cost to reach each neighbour
  Depending on what matters on the network, latency, bandwidth ...
     
- 3. Broadcast a compiled version of all of what you have discovered to all your neighbours, and receive similar packets from your neighbours
  it should carry a timestamp, your adress, a list of your neighbours and the cost you have affected to each of them.
  To avoid Congestion of the network by information packets each packets contains a sequence number.
  At any time when an information packet is received by a router, if the sequence number of said packet is lower than the
  highest  previously received from the same sender, the packet is dropped, as it is a stale duplicate. Otherwise it is broadcasted to all links except the one  where it came from. Packet AND their information can also become stale from old age, so if a router restarts or a corrupted sequence number goes unnoticed, or a packet starts looping around for any reason, after  a while the informations it broadcasted wil become stale and be removed, and the packet will no longer be broadcasted.
The affected router will be again able to emit information that will be  taken into account by other routers.

- 4. process the smallest link toward each device

This routing method is used by some industrial grade protocol 
- **Intermediate System-Intermediate System (IS-IS)**
- **Open Shortest Path First (OSPF)**

#### Routing Hierarchy 
The problem of routing by link state is that when the network gets very large,
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
Multicast is a  particular broadcasting system. In multicasting, you want to transmit a message to many nodes, yet not all of them.
You can just do a broadcast, but if the packet ought to be private or the group it is intended to reach is small vs the size of the network,
this is a massive waste of resources. If your routing is vector of distance based, you can use the minimal covering tree indicating you where to send packets,
and trim it to reach only target nodes of the multicasting. this method is costly however, as if you have m groups,with nodes in each you have to retain n * m 
more minimally covering trees.

A Better Alternative is the "Core Based Tree" algorithm. All members of a tree agree to make a node in the group the "central node".
A single minimally covering tree is derived, from the central node to all members of the group. This tree is shared among all members of the group.
Any time a packet for the group is emitted, it shall travel following this tree of members. Note that it is absolutely not mandatory that the packet first 
reaches the central node before reaching other members of the group.
With this method, all routers of the network only needs to remember one tree per group in the network, and they don't even have to  take part in 
it's conception only to remember it.
This is why this Algorithm is used on internet, Notably with  **Protocol Independant Multicast** or PIM.


#### Anycast Routing 
When you only wish that your packet reaches a receiver but you do not care which one (for example when you have multiple server able to distribute a resource,
like Content Delivery Network (CDN) or a time emitting server ) you want to exploit anycast.
The solution is simple : the service provided should lie on a host, not a router, and said host shall all have the same adress.
When trying to contact a given adress, all the routing algorithms  seen above ( distance vector, hierarchy, link state) will naturally (and unknowingly)
route the packet to the closest (depending on the metric) host providing a service.
Service provider shall not be routers because otherwise algorithm like distance vector, will see different routers as one single entity
and think that this unique super cool router is the way to many  shortest path to other device in the network,
when in reality it is really multiple scattered devices.




### Congestion Management
First let us define some terms 
Traffic Management : All measures related to having a working network able to dispatch as many data packets from emitters to receiver as possible  in a timely fashion.

Flow Control  : All measures pertaining to avoiding the situation of a sender sending too much packets for a receiver to receive,
causing packet loss.

Congestion Management  : All measures pertaining to avoiding the situation of Sender sending too much packets for the n
etwork to handle, resulting in a loss of packets or even a collapse of the network.

Here are a list of measures to be taken to manage congestion, ranked from the slowest to react,
to the fastest.

- Provisionning : Adding faster links and routers on most used routes.
- Traffic based routing  : Changing the appeal of links based on the how much traffic is currently using it
- Control of entry/admission : denying a sender from sending new packets to limit congestion
- traffic throttling  :  reducing the number of packet sent by emitters on the network on a time frame 
- load shedding :  routers dropping packets when they can no longer make up with the network charge


#### Traffic based routing :
This method has a drawback : the network can oscillate between links, congestionning them on a cyclic basis
instead of exploiting them all to reduce congestion.



#### Control of entry/admission
This how the telephonic networks work, it denies new cellphones to communicate while all other slots are occupied.
The task is more difficult in packet switching network, as you cannot predict which new connection
could be a factor of increased congestion. For example, a movie  streamed has a smoother demande on network
than web browsing, which is less intense, but also very subject to burst of demands.

#### Traffic Shaping / throttling
The token bucket  algorithm (or it's cousin the leaky bucket) allows routers to manage sudden burst of communication without getting overflowed.
A message emitter manages a bucket of tokens pertaining to a link with a router. When the emitter want's to send a message,
it consumes a token from the bucket. If the bucket is empty, it cannot send any message until it has received a token to consume.
If the sender has a burst of messages to send, it can send them as fast as the link can handle as long as it consumes token in relation
to the messages it sends. when the bucket is empty, the sender will hold any new messages to the router, until the bucket starts to replenish.
Thanks to this algorithm, burst of messages are allowed within reason, before smoothing it out to a more sustainable flow.
Other options of traffic throttling involve:
- router deleting random packets in the heap when it detects  early in a congestion, hoping that the transport layer interprets the packet loss as a congestion marker and
  reduces the flow (transport protocol TCP correctly assesses packet loss this way )
- Choke packets :  router sending a packet to the emitter asking it to reduce the flow of data 
- Explicit Congestion Notification (ECN) : tagging a packet before it being delivered so the receiver detects the impeding congestion and notifies the sender to reduce the flow of packets



#### Load Shedding :
Really the nuclear option of routers. Which packets to drop ?  It depends on the traffic. 
If you are transferring a file, if you delete oldest packets first (example with sequence number 6 ) then the receiver 
will have to keep newest packet (example sequence number 7,8,9) in a heap until the oldest had been transferred again, potentially worsening the situation. If you are transferring realtime data like Voice, 
new packets are more important than older ones. 
Third situation, the video compression algorithm MPEG transmits periodically base images and then lightweight differences,
allowing the receiver to reconstruct other images from the base image and the differences. Here the base images
are important but more numerous differences packet, less so.
Fourth situation, state of network packets (or how I like to call them administrative packets) are also more important 
than data packets.

A solution for effective load shedding is for the devices exploiting the network to mark packets as important or non-important.

### Quality of Service
Applications (and people) require more guarantees  than just best effort.
Quality of Service englobes defining and meeting demands.
There is 
- Reliability of the data being received is also the one being sent
- Delay between data being sent and received
- jig intempestive viariation of the delay 
- Bandwidth requirements 

How does the network layer manages when multiple packets from different emitters must follow the same route ?
This is a scheduling problem. Multiple scheduling solutions exists,one of them is the fair queuing, where 
the date of arrival, the expected lifetime and the size of the packet are taken into account to choose when a packet should be sent.

To guarantee Quality of service for realtime data streaming, various protocols were designed, they all fall under one of two categories, 
the **Integrated Services** and the **Differentiated Services**. 

 
#### Integrated Services
##### RSVP Protocol
Defined in RFC 2205 and following, a layer 4 Protocol but we detail it here,
as it does not carry any data and is closer to an "administrative" protocol like ICMP.
This is really a multicast protocol but with sending a message in the group to allocate some resources specifically
for a communication.


#### Differentiated Services
Unlike Integrated Services where resources are allowed on a per communication basis,
almost like telephonic circuit switching, with differentiated services 
resources are allowed on a per class basis. Think first class and second class packets,
getting different treatment when they enter a router, for example variation in scheduling.
Note that if a first class packet is going to get a better treatment than a second class packet,
two first class packet facing one another will be treated the same.
Differentiated Services have largely supplanted Integrated Services, because they do not require configuration
and are more robust when a router fails.

##### Expedited Forwarding (EF)
Layer 3 Differentiated Services Protocol, with first class and second class packets.

##### Assured Forwarding (AF)
Layer 3 Differentiated Services Protocol, with four class of packets,
each containing themselves 3 level of needed newtork congestion for the packet to be droppable.


### Network Inter-connection
If inside a given network, it is admitted  that all entities  use the same L3 Network Protocol,
between networks this is much less obvious. Even if the same L3 Network protocol is used, other things can vary,  routing algorithm are a great example.
Routing inside each Internet providers network of customer (called an **Autonomous System** or **AS**) should be confidential, otherwise 
their competitor could know how much money they pay / invest to move data around. But those networks must be connected together,
otherwise this is no longer the internet. The following sections  will expose problems that arises and solutions, when interconnecting multiple networks.

#### Tunneling
What to do when you want to allow two  network A and C  with the same L3 network protocol
to communicate together when they are separated by a network B using a different L3 network Protocol ?
Use Network Tunneling.
A and C have each at least one router which also takes part in B. Those routers, we'll call them here boundary routers
can communicate on their respective network and on B network. 

To establish a communication between A and C, an entity on A will send data  to it's boundary router.
The boundary router from A will communicate with the boundary router of C  through the network B. 
To do so, it will  encapsulate  the network data packets abiding to the L3 Network protocol of A and C
in packets to be conveyed through B. Routers on B will see those packets as normal packets carrying some data.
The boundary router on C will then take the "data" and  translate it  back into  packets with the correct L3 Network protocol to navigate in C. 

Virtual Private Networks (VPN) are a form of tunneling. An other one is IP to IP (for example IPv4 to IPv6).

#### Packet fragmentation
When a packet crosses multiple networks, there is no guarantee as it is not too large for some networks and needs to be cut in smaller 
packets or straight out dropped. In IP this  "size of packet" is called the **Maximum Transfer Unit** or **MTU**.
Multiple solutions exist : 
- cut the packet into smaller ones when needed, and reassemble immediately when possible along the way,
- cut the packet and then route it as smaller packets, let the recipient reassemble them,
- Design a packet which isn't too big for any network used during routing. The sender sends a packet, if the packet is too big, it is dropped and the emitter
  is notified that the packet was too big. The emitter tries again with a smaller packet. This is called **MTU Discovery**





### OSPF Open Shortest Path First
Very similar to IS-IS (Intermadiate System-Intermediate System)
from which it is inspired. When introduced, was to implement ameliorations in routing __inside__ 
Autonomous System routing for ISP.
A link state routing protocol (routers know about most router of the network and process shortest path)
excpected ameliorations were : 
- multiple distance metrics (latency, number of hops, geography...)
- routing with hierarchy network is split in smaller chunks
   and every router does not need to know what happens everywhere on the network
- load balancing, instead of throwing all packets on the single best route
- a minimum of security

OSPF represents the network as a directed valued graph, mapping routers and links between them.
OSPF allows routing by hierarchy and thus routers can be split in groups.
A group is one composed of one or more contiguous networks.
Routers outside of a group cannot see the architecture inside of it. Routers can be groupless. There is also the the backbone group 0,
all groups must be directly connected to it (notice we said connected, not take part in) either directly or via a tunnel.
This forces groups to take a star hierarchy, with the backbone at it's center.
Router inside the backbone group are called __backbone routers__.
Like other groups, the hierarchy inside backbone group is unknown to those who do not take part in it.
A router connected to two groups or more must take part in the backbone group, those routers are called __group border routers__.

A router between two autonomous system is called __autonomous system's border router__.
Routing usually takes this form, packet goes from inside a group to a group border router,
into the backbone, to one of the destination's group border router.

A newly connected router broadcasts a HELLO message on all of it's link.
One elected router per LAN answers the message with link state information.


##### BGP Border Gateway Protocol
Routing Protocol between  autonomous systems.
This is not as simple as routing inside autonomous system, because inside you are interested
by speed and efficiency. Between autonomous system, you have political or monetary incentive to
use or not use a router or an autonomous system when it would have been wise from a routing perspective.

To allow this kind of routing, BGP is a distance vector algorithm.
Each Autonomous System broadcasts to other what routes it can reach and with what distance (varying distance).
If an Autonomous system doesn't want packets from Autonomous System to go through it to reach another
destination, it simply does not broadcast to those autonomous system routes it can reach. 
If the whole path is emitted, only crossed autonomous system are specified except for the last router.
This has the benefit of detecting routing loop between autonomous system.
All the border routers of given autonomous system know about destination that can be reached by other 
border routers of said autonomous system, allowing an autonomous system to be though of as a single entity.


Consult RFC 4271 for more informations.



### MPLS MultiProtocol Label Switching , connection-full routing 
MPLS is a routing protocol which allows packet to follow a predetermined path, to ensure 
quality of Service. This not a L3 nor an L2 Protocol, not an L3 because it depends on IP adresses and header
not an L2 because it manages routing more than just one link.
Packet receive on top of the IP header an MPLS header,
which is composed of 
- one or more labels
- 3 QoS bit flags
- an MPLS Time To Live

When an MPLS router receives a packet with a MPLS header, it looks up the labels in said header.
The labels will help the router decide, which link to use next, and with what label to replace the current one.
An emitter or an MPLS router can stack multiple labels in the header to dictate the path that must be followed by the packet
for multiple routers.

At the end of the MPLS network, the MPLS header can be removed, and then the packet can be router as a normal IP packet.

An MPLS packet can also navigate on a network using MPLS and another network protocol than IP,
as long as their is an IP network at the end of the MPLS one.

The discovery and sharing of MPLS labels is defined alongside the MPLS protocol
in RFC 3031, 3032 and following. They can exploit **Label Discovery Protocol LDP**  and **BGP** .




#### Header of an IPv4 Packet
- IP version on 4 bits (IPv6 packets differ more from IPv4 packet  than just IP Version)
- Header Length , max length of header is 60 bytes 
- Type of Service, Used today to specify  differentiated service the packet (priority and when to drop)
- Total Length, length of packet header included
- Identification, to recompose a fragmented IP packet
- Don't Fragment bit, specifies if  a packet can be fragmented or should be discarded if it is too bit for the network.
  Today exploited for MTU Discovery (maximum size a packet can reach while travelling unfragmented)
- More Fragment bit, All fragments of a fragmented packet have this flag raised, except the last fragment.
- fragment position, position of the fragment in the packet, always a multiple of 8 bytes excepted the last fragment.
- Time To Live, Time before a packet should be dropped. Can be real time based or number of hops.
- Transport L4 Protocol used, to what layer this packet should be given.
- Source IP Adress and Destination Ip Adress
- Options, for various packet options
  Here are options
  - Strict Source and Record Route : Specify the entire path for the packet to follow 
  - Loose Source and Record Route : specify some routes that must be used when routing the packet
  - Record route : Each router should add its adress inside the option section of the packet so the route followed by the packet can be recorded.

#### Subnetworking, masks and CIDR 
IPv4 adresses are noted as four packet of numbers separated by points. These numbers range
between 0 and 255, as each packet represents the value of 8 bits. 
To subdivide a set IP adresses we use a subnetworking mask noted /xx with xx a number between 0 and 32.
The number defines how many bit of the adresses are to remain unchanged (starting from the left), to be part of the network.
Example, 192.168.0.0/16 , this sub-network masks encapsulates all ip adresses from 192.168.0.0 to 192.168.255.255
Another example 192.168.1.0/29 encapsulates all adresses from 192.168.1.0 to 192.168.1.7

Routing using thoses prefixes and rule "route to the most specific prefix "
(if for example I have the adress  81.57.151.237, and the choice betwween a route 81.57.0.0/16 and 81.57.151.0/24 I will use the latter one)
is called **Classless Inter Domain Routing** or **CIDR**.

It is called "Classless" because initially all IP adresses were split in classes ranging from A to E 
intended for bigger and bigger networks

#### Network Address Translation (NAT)
To face a growing lack of IPv4 Adresses, while waiting for a widespread use of IPv6
a solution was found for multiple hosts to use the same IP adress : Network Address Translation.
It first defines three IP ranges describing local network, that is, those ip adresses are to be used at will on any local network
without any International (or national) agreement, but they CANNOT be used on the internet. 
10.0.0.0/8 allowing for 16 777 216 Hosts
172.16.0.0/12  allowing for 1 048 579 Hosts
192.168.0.0/ 16 allowing for 65.536 Hosts
224.0.0.0/24 for local network multicasting only, 255 IP adresses available 
A router connected to an Internet Provider, takes part in this local network and also have an IP adress for the Internet.
When a host wants to communicate with someone from the internet, it's packets are transmitted to the router.
The router changes the IP adress and the source port of the packet from the local adress of the host  to it's own adress (of the router) on the internet
and a port that suits him.
It also feeds a table remembering the port from the emitter and the receiver and the IP adress of the receiver.
The receiver will then receive the packet, and answer back to the router, thinking it is the router which emitted the packet.
When the router receives an answer, it feeds the remote address and the ports involved to the table, to find which host on the local network 
should receive the message. It then changes back the destination adress and the port to transmit the packet to said host.

This method, widely used today for allowing ever more houses to access the internet while IPv6 is implemented,
has drawbacks :

- NAT by default forbids communication initiated by the outside world to the inside
  forbidding the creation of servers unless it is configured appropriately

- IP is thought as a connection-less networking L3 protocol, Nat inserts connection-full concerns,
  if a NAT fails, all communication going through are lost.

- NAT breaks the concept of layering, as it is concerned by what the layer above it does,
  indeed it was initially designed with TCP and UDP in mind, what would happen if someone wanted to use
  another transport protocol ? Or even a new version of TCP and UDP ?  It can't exploit it
  (or it has to modify it's NAT router to accept the new L4 protocol )

- The FTP Protocol, for file transmission, transmits multiple ports and IP to use, inside the payload of the packets.
  If an host behind a NAT sends this kind of info, it will relate to local network adresses and be unusable for the distant host.

- a NAT can only support about 61 440 connections at the same time as this is the number of TCP/UDP ports.

#### IPv6
Evolution of IPv4, aiming to solve and enhance multiple points,
most notably Adresses exhaustion of IPv4, but also,
reduce size of routing tables, allow the protocol to evolve, give more ability to better guarantee QoS,
enhance Multicast ... .

Notation :8 set of 4 hexadecimal digits separated by ":" character.
"::" indicates one or more set of digits composed only of 0's
IPv4 adresses can be legally  written this way in IPv6 : ::192.168.1.1

- IP Version (always 6 for IPv6)
- Differentiated Services, class of packet to determine which has priority, QoS indication 
- flow label, initially a supplementary QoS indication, still searching for a real use today 
- Payload Length
- next header, indicate either Transport Layer 4 being used or a following optional header with more informations
  optional header could convey informations about authentification (packet is encrypted), routing informations,
  packet fragmentation, jumbo packet (for networks of super-computer) ....
- hop limit, life expectancy of packet, to avoid it wandering for ever
-  IPv6 source and destination address, 128 Bits per Address (which means Ideally 7 * 10^{23} IP adresses per m² on earth)

There is no mandatory fragmentation header field  as hosts are expected to use MTU discovery algorithms,
there is nevertheless an optional one as IPv6 packet  can be fragmented by the emitter (and only the emitter,not
by intermediary routers).
No checksum header field as the upper layer is now expected to catch errors.


### Internet Control Message Protocol (ICMP)
Small packets working administrative tasks, to notify  emitter / receiver about a problem
here are a few example of messages : 
- DESTINATION UNREACHABLE : Can't deliver packet because of fragmentation or can't find destination
- TIME EXCEEDED : Packet reached it's EoL
- PARAMETER PROBLEM : A header field has an illegal value
- SOURCE QUENCH : almost forgotten, to notify an emitter to stop congesting the network with packets
- REDIRECT : when a router judges that a packet is not routed effectively
- ECHO / ECHO REPLY : Ping
- TIMESTAMP REQUEST / REPLY : to measure network performance


### ARP / NDP
NDP (Neighbor Discovery Protcol) is the IPv6 version of ARP (intended for IPv4).

For an IP program to know to which L2 Link  (and neighbour) give the packet to reach it's destination,
wether  the destination lies on the same link (multiple links joined by switches or hub also work ) it uses the ARP protocol.
When the destination lies on another network (or another link, with at least a router between them) the ARP protocol alone wont suffice.

When the ARP protocol suffice, the host can 
- lookup in a preconfigured ARP table what is the MAC address to send  the packet 
- Send a broadcast L2 packet asking the MAC address of the host having the destination IP.
Of course, if you see an ARP communication which doesn't involve you,
you can nevertheless save the ARP answer in your table, requirnig less broadcast later.
ARP entries in their table expire with time, so an IP address isn't linked for eternity to a MAC address.

This works if hosts are on the same link (can be joined by hub and switches)
but L2 broadcasts are stopped by L3 router, so ARP cannot propagate.
There are 3 solutions 
- configure an ARP proxy among the router on the same link as the emitter. This router
  will say that it has the IP adress that emitter wants (when it is not the case) and give it's own MAC address.
  It will then receive the packets for the destination and forward them to where they need to be.
- configure the router to propagate the broadcasts (not possible on all routers, especially if they are the interface between two different link technologies)
- configure on the emitter side the closest router as a gateway,
  the emitter will ARP ask for the MAC address of the router, and will send packet to the router which will be
  in charge of bringing them closer to the destination.
  this solution is very similar to the arp proxy, but instead of the router lying to the emitter and saying that it has the searched IP
  address, it is the emitter that resignates to send the data to the router. Here the emitter knows  that the router is not the physical
  address of the destination, but rather just a hop.

ARP can be spoofed, an attacker can, just  like an ARP proxy, broadcast it's own MAC adress  as holding someone's else  IP,
therefore intercepting all traffic.


 
###  Dynamic Host Configuration Protocol (DHCP)
When a host connects itself to a network via a Link but doesn't have a preconfigured IP address,
it can request an IP address to a DHCP server if there is one on the network.

The hosts makes an L2 Broadcast asking for a DHCP server to provide IP address.
The DHCP server answers, attributing the IP address to the host (it has the physical address of the host).
The IP is given based on a lease, if after some time the DHCP server or the host doesn't renew the lease,
the host loses it's IP address.

More than just an IP address, DHCP server also provides network masks, gateways, DNS address, time server ... .




## Transport Layer 

The Goal of this layer is to bring packets to their destination with a variable level of reliance,
regardless of the quality of the networks used.
It uses the Network  layer to  send packet 
This layer offers the following services to a higher layer :
- reliability that the data sent will be the data received
- uniformity, allowing software developper to conceive App that work on a variety of types of network (without them even knowing !)
- networking protocols which executes on the users hardware versus L3 and below which mostly executes on router and switches,
  outside of the control of the user.
- demultiplexing of networking flows, allowing multiple process inside the same host to communicate at the same time
- flow and congestion control with the L3 Network Layer

Just like the Network Layer, the Transport Layer promotes two type of "means of transportation"
Connection-oriented and Connection-less

The usage of  TCP layer protocols can be reduced to 6 generic functions :
- LISTEN : Block until someones tries to connect to you
- CONNECT : Actively try to connect to someone 
- SEND : Data to someone you are connected
- RECEIVE : block until you receive data from someone you are connected 
- DISCONNECT : Make known that you no longer wish to communicate
  
***Transport Service Access Point TSAP***, entities allowing multiple processes on a same host to use the network at
the same time,  those are ports in TCP and UDP.

Port mapping program
inetd 

### Establishing a connection and three way handshake 
When establishing a Transport Layer connection, to avoid the risk of multiple connections
being opened at once because of a  packet received twice  for any reason (late arrival, accidental duplication, ...)
The **Three way handshake** has been retained in TCP : 
Host A chosses a sequence number to enumerate packets it will send.
Host A  sends a Connection request with  the sequence number .
Host B chooses a sequence number and sends it to host A with an acknowledgement that 
Host B answers that it has acknowledged the sequence number chosen of the first host and also joins
it's own sequence number to enumerate of the packets.
Host A answers that it has received the acknowledgment alongside it's first packet of data. 

Host A and B shall pick a new sequence number each time they send a message during the handshake,
so if at any time during this handshake a packet is duplicated, it will be detected and discarded.

### Releasing an established connection
Releasing an established connection is harder than establishing one,
this problem is known as "the two general's problem" :
If two remote hosts want to decide something on an unreliable link (say, to end communication),
they can't if they rely only on acknowledgments coming from the unreliable link.
Indeed, in all cases one of the host will never have a strong guarantee that it's latest message 
arrived to the other, thus he can't with certainty be sure that the other host also agrees on the decision.

The solution to this is two fold : first introduce the notion of timer,
if after a certain amount of time no packets are received, or a disconnection request is not acknowledge,
consider the connection lost. Second, let the process above the transport layer decide when the connection is lost.


### Error, flow Control and Congestion Control

Transport Layer is entrusted in providing guarantees that the data which arrives is correct,
and that the sender does not overflows the receiver. It also works with the Network Layer to not congest the network.
consequently this layer implements Error detection / correction codes / algorithms,
sequence number, congestion control , and flow control by sliding windows. 

Those mecanisms are important, because there are no guarantees that the link exploited 
has error detection, or that packets wont be interverted on the network.

#### Max-Min fairness 
To avoid congestion in the network, we need to decide how to share bandwidth among multiple transport entity.
We usually aim for max-min equity. This is when  you cannot raise the bandwidth given to a connection, without lowering
the bandwidth of another equal or smaller connection.
This situation translates that whe have __Maximized__ the size of the __minimum__ flow rate (the smallest flow is as big as it can get.)

#### Additive Increase and Multiplicative Decrease
To do congestion Control, the sender acts on the same lever as flow control, how fast it sends the data to the receiver.
To know how fast it can send data without congestin the network,it has few options
- rely on the sender sending him notifications of imminent congestion, which it had received from a flag raised on packets by  intermediary routers
- Be contacted itself by congested routers which asks for a lower rate of data
- Detect Packet loss and assum thatit is because the network is congested (the choice of TCP)
- adopt a behavior which minimises the time spent in congestin the network, while maximising the data rate, this is what **AIMD** is for

#### Additive Increase, Multiplicative Decrease (AIMD)
Starting from a fact, it is faster to create a congestion than to resolve it,
we can adapt the sender behavior to make it slower for it to create a congestion than to resolve it.
To do this, the sender increases the data rate Linearly (Additive Increase)
and decreases it Exponentially when a problem is detected, (Multiplicative Decrease).
Since Strictly linear increase can be a bit too harsh for the sender, the method used now is more
"Multiplicative decrease until a threshold, then linear increase until congestion occurs, then it that case go back to the threshold
or even lower if necessary".
This is all assuming that the flow rate wont be too big for the receiver.

Another problem of this technique is that you need to be sure of how you are identifying congestion, for example if it is packet loss,
and you use a wireless network, you run the risk of having a very low flow rate without a network congestion necessity, because
packets are lost on wireless link fairly easily (that's why some network links usually have auto retransmit a few times without informing L4 layer).

### UDP
Connection-less, congestion-less, flow control-less protocol, guarantees of delivery-less
really just a Transport Wrapper for IP which adds Multiplexing and a Checksum.
Very small Header though, only 64 bits.

###  Remote Procedure Call (RPC)
Another Transport protocol than TCP or UDP is RPC. It allows a programm to call a function in another program on the same system,
or, in relation to the topic of this book, in another program in another system via network.
There are some caveats though, like what happens if the remote system is unreachable.What happens when you pass a memory pointer in 
the arguments of the function you call, which will point to something else entirely on the remote system ? Or even just is goal to reach worth the slowdown ? (tens or hundreds of milliseconds  versus nanoseconds) A thing of distributed architecutre an micro-services really.

### Realtime Transport Protocol (RTP) and it's Manager Real Time Control Protocol  (RTCP)
At the border between a L4 and L7 Protocol lies RTP, a protocol which relies on UDP to move around video and audio flow.
Quality of Service is to the surprise of no one at the center of this protocol.
To ensure it multiple tricks are used mixing timestamps, sampling rate, udp multiplexing and usage of network buffers.
RTCP is to transport information to maintain good Quality of Service, it displays to the sender information about the network :
jitter, latency, bandwidth... .

#### Transport Service Access Point (TSAP)
multiplexing solution of transport protocol to allow a single L3 network address
to be used by multiple program on a same host to communicate on the network at the 
same time. In TCP and UDP, these are ports.

### TCP
THE transport protocol. Connection-full, with timestamp, congestion and flow protocol with sliding windows / tmestamps , with
mutiplexing (ports). The communication is point to point.
When a communication is established, the receiving and the emitting host both create a socket to communicate.
Note that both hosts use a port (rarely the same) when they create a socket.
Connection are established via three-way handshake

A TCP header has a size of 20 bytes + some additional bytes for options. The maximum size of a TCP packet is 65 KBytes.
In the fixed size header we find
- Source Port
- Destination port 
- sequence number 
- Acknowledgment Number  (the next expected sequence number, all packets before it have been received)
- Some unused bits (still in the fixed header) for futureproofing the protocol
- flags to notify network congestion, that action have been taken to reduce said congestion, an "emergency flag" to signify something at the discretion of the user,
  a flag to ask that data be forwarded to the application immediatly without sitting in a network buffer, ...
In the various options that can be added we find for example, the ability to specify a maximum segment size,
the ability to increase drastically the size of the sliding window... .

TCP also offers **the Nagle Algorithm**, since it is not mandatory in the protocol
to emit an acknowledgment immediately when a packet is received, the nagle algorithm offers
to wait as long as possible to send a maximum of acnowledgement at once to better use bandwith.
This can be enabled and disabled via TCP_NODELAY and TCP_CORK. 


#### Congestion Management Connection in TCP
TCP was primarily designed to run on wired connection. This means that the rate 
of packet loss is low, and that a lost packet has much more chance of meaning that the network is congested
thank there is problem with a L2 link. This idea shapes many of the congestion management mechanism
employed in TCP. Particularly, one method used is to maintain a network congestion window, to know when the network is congested
in supplement to the flow control window to not overload the recipient of the connection.

#### The use of AIMD in congestion control
TCP congestion control algorithm tend to adhere with the AIMD idea,
slow increase of the number of packets sent, and sharp decrease if a problem arise

##### Ack Clock
To determine the fastest rate at which packet can be emitted without overflowing the network,
a sender can send a short burst of four packets. These packets will arrive to the receiver, in a burst
slower than when they were emitted. The length of this burst is dictated by the slowest link.
The sender should acknowledge these packets at the same rate that they were received.
The emitter now knows the highest rate at which it can send packet without overlooding the slowest link.
This mechanism is not self sufficient. IF for any reason acknowledgement are retained for a variable period of time
(for example because the receiver uses the Nagle Algorithm), the algorithm falls apart, or it's efficiency is greatly reduced.
It is also not fair for small connections 


##### Slow Start 
The problem with AIMD is that when the increase is slow when you start at a ridiculously slow rate,
it can much time to reach the tipping point. To solve this issue, we commit a small infraction to the paradigm.
The increase is multiplactive until a point, then it rises additively to reach slowly the point where it is 
sending data too fast.


##### Fast Retransmit
If a packet is lost, we have to wait for it to timeout before re-emitting it.
To enhance performance, we can realise that 
if packet x is lost, but packets x+1 x+2 and x+3 arrived correctly
the recipient will send four times the same  acknowledgment.
This acknowledgement says that  the last received packet is x-1 and that the next expected packet is x.
We can consider that after three duplicate acknowledgment (four acknowledgement received in total)
the packet was lost, and resend it without having to wait for it to timeout.
We know that it is packet x that is lost because otherwise we would have received 
an acknowledgement that packet x is arrived and x+1 is expected.
This method was used in the implementation TCP tahoe.

##### Fast Recovery
With fast retransmit in TCP tahoe, when a packet is lost, the congestion sliding window is completely closed before
being reopened with slow start. But we can do better by exploiting the duplicated acknowledgements as an ACK clock.
when a packet is lost (we have detected it thanks to multiple duplicated ackwnoledgements) we halve the congestion 
window and wait for the ACK to come back from the packet inflight. When enough packet have reached their destination,
We can start emitting again, with a smaller congestion window, but one which was not completely shut beforehand.
This algorith was used with TCP Reno.

#### Cumulative Acknowledgement
Instead of acknowledging sequence numbeer after sequence number, 
if you receive a number of packets (the order does not matter as long as they are all contiguous in the end),
you only acknowledge the packet with the biggest sequence number you received. The Sender will understand that this packet,
and all other before it were correctly received. 

#### Selective Acknowledgment
Cumulative acknowledgement on steroids, you can acknowledge ranges of values. The sender
will only retransmit missing packets  while also being able to go forward on the transmission of data.
In TCP, up to three distinct ranges are possible.

#### The Silly Window Problem
When data is emitted or consumed slowly we can reach a silly window problem,
where data is sent immediately when present (slow emitter)
or requested immediately when a very small ammount is processed (slow receiver).
The result is a very inefficient use of the network as big header are used to transmit  small amount
of data (can be down to the byte !).
To avoid this few solution : wait until their is much data to send (slow emitter) or
much room to receive data (slow receiver)

#### TCP Cubic
Designed for Long Fat Network to offer better congestion control pertaining to these kinds of network.

### QUIC
Multiplexed Conncetion Protocol over UDP, designed  by Google in 2012
to enhance performance of website browsing. Still mainly used by google today,
accounts for 10% of website worldwides.

### Long Fat Network (LFN)
Highbandwidth over long distance network (think Gbit/s and more  fiber optic over a few hundred kilometers)
brings up unique challenges, like high latency and very poor usage due to the sheer capacity of the link.
Let's take two host connected by a one Gigabit per second fiber optic with a RTT of 50 miliseconds.
To occupy fully the link we use the product of bandwidth over time which here gives 0.05 seconds * 1 Gigabit =
50 Mbit burst data to fully use the link.
This also means that sequence numbers are burned through very rapidly ( 34 seconds to go through 2^32 numbers ! )
and we run the risk with older protocols of multiple packets wandering in the network, having different payload, yet the same
sequence number (life expectancy inside internet is 120 seconds).

### SCTP


## Application Layer

### Domain Name System (DNS)
This protocol allows an entity on the network to get the IP address of another entity,
based on a name using alphanumerical characters, a domain name. Domain names are case insensitive.
Domain names can be made of other characters than latin (like cyrillic) since 2012. 
Domain Name follows a hierarchy, the most generic to the right, the least generic to the left.
In www.example.com , the most generic part of the domain is ".com." (millions of websites end in ".com.")
Followed by example (maybe a handful of network services have "example.com." at the start of their domain name).
It is Finished by "www.", only one service is linked to "www.example.com.", A web server.

#### Governing Body of DNS and top level domain names
The ICANN is responsible for managing domain names distribution.
The most generic domain names, called Top Level Domain, can be generic like .com . biz or .edu
or they can be country codes like .ja .fr .uk .ch .de ... . Top Level Domain names
can also be made of other than latin characters, since 2019.

#### Fully Qualified Domain Name
Think like Absolute Path on an operating System.
the whole name is present, up to the "global name" which is just a dot ".".
www.example.com. Is a fully qualified domain name (the last dot is usually "hidden" by web browsers)

#### Qualified Domain Name
Think like relative path on a operatin system.
Only part of the name is present.
www.example is a qualified domain name of www.example.com. .


#### How a DNS Request is resolved
It works as follows, an entity asks to the closest dns solver, "the stub"
the IP adress associated with a name. The stub is usually running on the entity (a daemon, or a function call).
The stub will then forward the request towards the nearest "local recursive resolver"
which will emit multiple queries to various Domain Authorities  from the most generic towards the most specific, to
determine what is the IP given to the associated name.
In the present day (was not true at the start), the IP adress of the initial entity is
also provided in the request from the local recursive resolver towards the Domain Authorities,
so Content Delivery Network can provide the closest server for the 
When found, the answers then comes back toward the initial entity.


#### DNS Record and DNS entry
group of entries Detailing what IP adress is associated to which domain name.
A DNS entry is composed of
A domain name, a lifetime expectancy before the name will be forgotten if not refreshed,
a class  ("IN" for Internet, other types are rare) and a Type.
Here are some possible types that a domain name can have:
A for an IPV4
AAAA for an IPv6
MX for a web mail server
NS for another dns server
PTR an alias for another IP
TXT generic text 
CNAME alias for another domain name
...

All DNS records start with an SOA entry, which points to the area's main DNS.



### Email 
Every program attempts to expand until it can read mail, Zewinskie law.

Email are exchanged as follows, the agent user of the sender connects to it's message server, to transmit an email it wishes to d
send to areceiving  agent user located on the same or on another message server (the sender and the receiver can also be identical).
The message server contacted by the sender then sends the email to the message server of the recipient agent user.
When the agent user will next connect to it's message server, the message server will notify it that 
a new email is available.
The receiver can also be a diffusion list, in which case the receiver is a collection of multiple agent user
which have all subscribed to the diffusion list, to receive everything sent to the email address of the diffusion list.


####  Simple Mail Transfer Protocol (SMTP)
Server messages exchanges email of agent user through the SMTP protocol.
Here is in short what happens during an exchange of email 
```
220 recipientserver.com SMTP Service READY
HELO emittingserver.com
250 receivingserver.com says hello to emittingserver.com
MAIL FROM coolsender@emittingserver.com
250 sender ok
MAIL TO nicereceiver@receivingserver.com
250 receiver ok
DATA
354 Send Mail
thedata of the email ...
.
S 250 message accepted
QUIT
221 receivingserver.com closing connection
```
Note that in SMTP data are sent in clear, which is a huge security concern.
This Among other limitations, prompted the creation of **Extend SMTP (ESMTP)**.
To know if a client accepts ESMTP, instead of sending HELO,
the client sends EHLO, if the connection is accepted with this anagram, the server
understands ESMTP.


### Email adress
an email adress is a domain name (the one of the server message)
preceded by an @ and a username. Just like domain names, email adresses are case insensitive.


#### Agent User
program able to connect to a message server to send and receive  emails.
The agent user can be light (if it is a website to which one connects through a web browser)
or heavy (a program installed on the machine of the host).


#### MultiPurpose Internet Mail Extension (MIME)
IF at the start emails were expected only to send text (just ascii characters !)
It quickly became evident that this would not suffice.
Enter MIME, a format to send content in emails that is not text, but  type of files.
MIME are today used not only in emails but also in web development.
files can be sent in email through ascii characters which needs to be recomposed into a
file (provided that there is a MIME header beforehand)

#### Internet Message Access Protocol (IMAP)
SMTP and ESMTP are for message server to exchange emails. 
Communication between an agent user and a message server can be done
through various protocols, one of them is IMAP.
IMAP is the newer version of an older protcol, ***Post Office Protocol (POP)***.

#### World Wide Web (WWW)
Applicative framework which allows user to access content disseminated in the entire world.
Designed by Tim Berners Lee at the CERN, a european physics laboratary located in switzerland next to the french border.
Here is a snapshot of the first website :
http://info.cern.ch/hypertext/WWW/TheProject.html

#### World Wide Web Consortium (W3C)
Body composed of numerous organiaztions which detach permanent personel to work
on writing new standards for websites.
They maintain among other things, HTML, CSS, Javascript.

#### HyperLink 
#### Unified Resource Locator (URL) and Unifier Resource identifier (URI)
##### URL
Protocol ::// the.domain.name./the/path/to/the/resource
various protocol
the "about"  protocol keyword

#### Hyper Text Transfer Protocol (HTTP / HTTPS)
Protocol based on TCP (although HTTP/v3 also works on UDP) for transmitting web pages.
Based on a Request Response model, this Application Layer 7 protocol is in plain ascii text (when not encrypted, see HTTPS).
The requests are called "method" and are quit generic,
which allows HTTP to be used not only by websites but also by other programs such
as media player for example to convey information on the Internet.
Here are some (not all!) methods along what they mean
GET When you want to receive a resource
PUT When you want for the server to save data in this request
DELETE Delete information pertaining to a resource
OPTIONS What are the available options with this resource
The response come with codes 
1xx Information  (rarely used)
2xx Resource processed Correctly, data follows if any
3xx Tells the browser to redirect it's request to someone else
4xx When the Client committed an Error
5xx When the Server experiences an Error

The requests can carry a header which enriches it with additional information,
type of client, languages preferred, understood data compression shceme ... .


#### Cookies
Small text files saved by websites inside the client web browser to remember 
informations about it like account automatic reconnection, it's shopping cart, ... .
Cookies are only accessible by domain's name website which initially  put the cookie, this is the "same origin rule".
Cookies can be also used to track users in their navigate, with what's called third parties cookies.
A website owner signs an agreement with an advertisement agency, which will provide for the website to send to each user.
This code will call the website of the announcer and allow it to deposit it's own cookie, the third party cookie.
If the user then browses toward another website which has also signed an agreement with the same advertisement company
the same scenario will repeat, allowing the the advertisement company to access the cookie stored earlier, and thus, extracting
information about the browsing of the other website. The advertisement company can also store other informations,
like the IP adress used when accessing the website, so it can later on link users together or nomadic and static devices of a same
user together.

#### Caching
A web browser can save a web page to display it faster to the user the next time it visits the page.
The browser, will ask the web server beforehand if the resource has changed since it was last cached.

#### Tracking and Numerical fingerprint
Cookies aren't the only way to track a user on the internet.
Browser allow website, for performance reason, a variety of informations about the device
such as available fonts, screen size, battery state, languages installed, web browser, GPU 

We can only recommand this website of a university
which determines if with finger printing technologies only if you can be isolated 
from any other user who also browsed their website :
https://www.amiunique.org/fingerprint



#### Proxy 

#### VoIP
A particularly demanding problem,
data is generated in realtime, no chance to preload it, and
accepted delay before communication is perceived as  bad is between 150 and 400 ms.
Compression must be optimized to gain time, and jitter is a feirce problem.
Differentiated Services or Integrated services with their orientation on Quality of Service (QoS)
can help VoIP, if only they are implemented on the network where the packets go.


#### VOD
##### Dynamic Adaptive Streaming over HTTP (DASH)
Networking protocol to send over the network recorded video files.
This open-source protocol requires a video to be split into multiple files with
varying refresh rate and quality. The protocol can then tell which small part of the video to send
when required, to best match with the current congestion level of the network.
The protocol frequently probes the network to know the congestion level of the network.
All available format and video qualities are listed in a file called a manifest, which is then sent to the client
for it to decide which one to choose based on the network conditions.
HLS is an Apple  concurrent of DASH.


#### Zipf law 
The most popular content is X times more likely to be requested than the Xth one.
Useful when you want to ponder the need for resources between different content / actors.

#### Peer To Peer (P2P)
Network Protocol / Architecture / service where multiple machines collaborate together to provide 
content. They can both be client and host at the same time, giving it's name to the protocol
from one peer, to another peer.
The first P2P widespread service was Napster, it's flaw was a centralized database of content.
It caused it's downfall since the service became well known for illegally sharing music,
by closing the main website no one was able to continue sharing and research for content on a widespread scale.
To create peer to peer, three questions must be answered
1 How can a peer find other peers which have the content they seek ?
2 How is replicated content among peers to ensure a fast download for many ?
3 How do peers incentivize themselve and other to share and take part in the network ?

To Answer the first (1) Question, torrent  were born. These are small files which informs 
- about the hash code of the chunks of the content (to verify that received content is valid)
- the address of a tracker, a machine in charge of guiding new peers which want said information to peers who have it
  (by using DHT)

To  Answer the second question, the sharing of chunks must be not in order. If a chunk is hard to find, it must be downloaded
in priority to be replicated among multiple peers to make it easier to find. This is especially true when
P2P networks have a high rotation, where many peers usually don't stay for long after their download is complete.

To answer the third question, regularly, peers evaluate who tries it's best to share shunk (seeders)
and who tries it's least, while trying to download as much as possible (leechers).
Peers will then make a choice to share a bit more with well behaved peers and less with ill-behaved peers.
They also chose some peers randomly, to allow for redemption, and to allow  new peers to take  part in the network.


##### Distributed Hash Tables 
To be more resillient than a single database creating a Single Point of Failure on a large scale,
the concept of distributed hash table was created.
Each peer is reponsible for a small part of the subnetwork in charge of providing data,
and guides request to the nearest peer who may have the answer ... a bit like a networking algorithm.




### Content Delivery Network (CDN)
A service provider places multiple servers at strategic points of the Internet.
Internet Exchange point or even inside the network of internet providers are an example
of good strategic points.
Those servers use the internet to sync between themselves.
When a client request information to the service provider, 
it is unknowingly (to it) routed towards the closest server, reducing 
the delay between asking for a resource and receiving it.
A good architecture for CDN is the tree architecture,
there is one (or more) CDN mother server which distributes content to CDN child servers,
which are those which all client interact with.


### Computer farm
To make a cluster of computer behave like a cohesive single entity, (or at least that's what the user sees)
multiple solutions are possible
- using anycast routing to route to the closest server which will then process the request
- configure a DNS server to equally distribute load among servers 
- have a single machine acting as a proxy be the single point of entry before sharing load among servers.
  the proxy server can even answer request itself if it is about a static resource, which will be at it's disposal
  

### inetd

## Security
The first hack goes through network goes back the 1960's era,
the goal then was to be able to engage in telephonic conversation to the other
side of the world without having to pay the salty fee associated to it.
The fault came from a sound tone used to authorize the caller to make the call,
which a whistleblower sold with breakfast cereals was able to reproduce close enough,
that with a little diy and technical knowledge, you could use to call for free.
Today, the world, the  tools and the consequences have changed.

### The security triptych / triangle
But what does it mean to be safe ? Actually it boils down to three objectives:
- Confidentiality
  Data is only known by those who are intended to.
- Integrity
  Data has not been tampered with or falsified
- Availability
Data can be accessed by those who are meant to access it in due time.

If Integrity is always necessary, sometimes Confidentiality or availability isn't

stock market status needs to have integrity and availability, but confidentiality
is unnecessary, it is public data.
Offline offsite backup saves of critical data  needs to be confidential and have integrity,
but the immediate availability secondary (not in all cases).

Two very important ideas about users emerges from this triangle 
- authentification
  Identification is saying who you are,
  authentification is proving that you are who you pretend to be
- non-denial
  An author cannot deny (without immeasurable amounts of bad faith)
  deny acts that it has accomplished.

### Seven fundamental principles about security 
To reach the objectives of the security triangles, their are seven principles to guide
our hand
-1 Simplicity & Restrain of means
  When there is more than one way to reach a goal,
  the one which uses the least amount of resources / the least complicated must be preferred.
  Because the more means you invest, the more  changes are that something goes wrong (the bigger the attack surface)
  "Perfection is not reached when nothing can be added, but when nothing can be withdrawn" also see "Ocam's Razor".

-2 explicit safety
  choices made must be clearly documented, and set everythin. Default /unknown / floating values or states must be assumed to be unsafe.
-3 Complete mediation 
  Any access to any resource must be authentified.
-4 Principle of Least Authority
  Any system or user shall be given the least amount of power / authority which it needs to perform it's tasks.
  By doing so, if a user or system is compromised, the whole system does not automatically crumples like a house of cards.
-5 Separation of concerns
  Very similar to principle 4. Each user/system does one thing, does it well and safely but one thing only.
  Note that this principle is also plebiscited in programming.
-6 No unnecessary sharing 
  Data shared among multiple systems make them more complicated (see principle 1)
  and can potentially open new pathways for attackers.
-7 open construction / white box principle
  All of your security measures should see their efficiency unchanged even if the attacker knows that they are in place.
  Particularly important for cryptography, if your cryptographic algorithm is vulnerable the moment 
  the attacker knows that you are using it,without knowing what is your key, it is not a good algorithm.
-8 Agreeableness and tolerable
  Choices in place  must be documented and explained. No technical measure can guard against a frustrated 
  human being who thinks your system is only slowing it down. 
  This principle surely explain why vulnerability mitigations are always thoroughly justified.

### Offensive Fundamentals
When on the attacking side, you must be dilligent and organized if you want
to succeed, the following points are frequently if not always of the foundation of
an attack
- Recon
  First you need to obtain as much informations as possible about your target, without
  taking any action that could yet make you spotted, these are
  - searching all and any freely accessible resource about the target (OSINT)
  - searching in trashcans (yes really) although it might get you spotted 
  - going near (not too much) the physical location of the target and inspecting if
    something could be exploited (easily accessible networking cabinet, informations about hardware used, wireless communications ... )
- sniffing and snooping
  Like recon but maybe a bit more involved, and also may get you spotted. You're looking for
  firewalls, IP adresses, open connections, hardware informations , some L2 packets, useful DNS entries  etc.
- spoofing
  An aggressive action without any reasonable doubt, you try to spoof the identity of the target or someone
  related to it, to attain your goal. You can try to spoof DNS server, TCP connections, to poison ARP cache ....
- disturbing
  Another aggressive action, you try to disturb services used or hosted by the target, or the access of the target to those services.
  You can flood the victim with useless connections (Denial of Service or even Distributed Denial of Service), force it to perform many hard
  tasks making it unusable for tohers, or just crash it. To protect oneself against DoS / DDOS attacks, one can
  - force clients to resolve a hard problem first, so the burden is on the attacking side
  - use a powerful third party to analyze and delete dubious packets (with strange options for example)
  - use a powerful third party DNS to reroute request first to a proxy which can act as buffer and even treat some requests.
  - make disappear a /24 segment (16 M adresses) on the internet by making a powerful third party announce it via BGP.
  this third party will then reroute traffick inside it's Autonomous System  toward yours.
  
  
### Firewall
A program that inspects all traffic between a part of the network labeled "the outside "
(the internet, a particular network submask, everything outside the host ...)
and the inside. Only allowed packets will be accepted, others will be discarded and stopped from travelling further.
to decide if a packet must be kept or discarded, a firewall reads a rule table, indicating discriminating factors.
these rules can now also depend not only of the date avaiable on the currently monitored packets,
but also of prior packets beforehand, allowing for a more fine grained monitoring.
with **Application level gateway** the firewall can now make decisions based not only on connection state and L2 to L4
informations but also because it "understands" the L7  Application used (or the content).

### Intrusion Detection System (IDS)
These are programs which can detect anormal behavior which could be sign of a potential attacks,
like password bruteforce, strange flags in IP packets, port sniffing, ... . 
They can be host based  (HIDS) or network based (NIDS).
They have a drawback though,
- NIDS have either very limited power or are central to the network and acting as a man in the middle,
if they crash or they are compromised, the whole network is compromised/ can go down.
- HIDS eat up processing power on the host they are running on.

There is also the question of how many false positive, versus false negative you will get.
Too many false negative and the system is useless. Too many false positive will tire you,
forcing you to check everytime for anything strange on the network.

### Cryptography
Cryptography is the art or science of converting accessible information called **clear text**
into gibberish called **ciphered text** for anyone but allowed agents. They can read through thanksto the **key** that they possess.

When evaluating a cryptographic algorithm, we have to assess what are the different threats
that we seek to defend to 
- **eaves dropping** when we fail to prevent  somemone from getting  a piece of information it shouldn't have.
-  **replay attacks** when someone has a rough idea from what is the content/intent of a message and just re-send
  a couple time to disrupt a service, without even having to break the encryption.
-  **spoofing** when someone sends or receives messages, passing for an allowed agent when it isn't
-  **denial / non-repudiation** when an allower agent becomes malicious and tries to deny it commited acts when it really has

#### Kerchoff principle
Proving all those properties are true simultaneously at any point in time in a cryptographic algorithm  can be quite a hassle.
To be sure that this is really the case we ought to follow cryptographic algorithms which follows the 
Kerchoff principle which states "encryption algorithm used to protect something should have their innerworking open to the public.
With only the key which are used to encrypt data kept private, the algorithm must stand and keeps the mentionned properties."
This principle was first enounced by Auguste kerchoff in a french military science Journal. 
(Journal des sciences militaires, vol. IX, pp. 5–38 "II. DESIDERATA DE LA CRYPTOGRAPHIE MILITAIRE.", Jan. 1883)
If others principle he enounced which were true at the time are no longer used today, this one still stand strong,
it has some real world example like the WW2 Enigma machine or the WEP wireless encryption protocol.

#### Attack patterns in cryptography
There are three types of attack one can make against a cryptographic algorithm,
studying the robustness of an algorithm against each type helps us decide if the algorithm 
is sound or not.
- ciphered text only
  The attacker only has ciphered text, he does not know what is the clear text which gave the cipher
  he is working with.
- known clear text
  The attacker has some ciphered text and the clear text associated to it, but he cannot
  feed the algorithm the text it wishes, only work with what he managed to get.
- chosen text
  The attacker can play at will with the algorithm, encrypting the text of his liking and studing
  the resulting cipher.

#### Redundancy & Freshness
Now onto some very important considerations to be taken account about the data we intended to cipher 
-first some of the data must be **redundant**, that is it must include some information that is not
  "data" but unneeded metadata. If it is not included, then the receiver of a message has now way to check if 
  what he has received is valid data, data with errors, or pure gibberish generated by an attacker.
  Too much redundant data cannot be added either, it eases the work of an attacking cryptographer otherwise.
- second the fresheness of the received data must be considered, otherwise the algorithm
  is open to replay attacks, where an attacker having an idea of what means a message, without having broken the encryption,
  just sends it again to cause an unwanted action to take place.

### Encryption algorithms
#### Substitution And transposition cipher 
Also called "Caesar-cipher" A well-known toy cipher, even taught to kids under 15 !
Each letter of the alphabet is replaced by one another, in the whole message.
Very easy to implement, but also very easy to break, you only have perform a statistical analysis on a message
big enough and you can deduce which letter has been replaced by which, since not all letters are used at an equal rate
in any given language.
Transposition cipher work by altering the location of the letter instead of the letter itself,
also easily breakable.

#### One time pad 
A random generated set of data called a pad is XORed with the real data before being sent.
The receiver only has to XOR again the result with the same set of data to obtain the text in clear.
A bullet proof technique. Yes really ! because from the ciphered text,
Any clear text is possible, the only way to know which one is correct is to know which pad was used.
Change the pad, and the same ciphered text know means something else.
One drawback though it requires that both users have the same pad (how to distribute it ?).
The pad is one time use because if reused, information leakage can happen and reveal information
about this message or other ones.

#### Quantum encryption
Relies on the use of optical filters, fiber optics and laws of quantum mechanics
to be resilient even against Man In the Middle Attack. BB84 is a "famous" quantum key distribution protocol.
Some products using quantum encryption  do already exists but they come with limitations.

#### Symetric Keys Cipher
These algorithms use the same key to encrypt and decrypt data.

They rely on a cascade of permutations and substitutions to cipher data.
Which permutation / substitution is applied is depending of the key. Reminder, permutation is changing the position of the bits, substitution is changing the value of the bits.
You can stack those operations on one another, each level of the stack is called a stage. (a single stage can be made of multiple encryption / decryption algorithm)
The resulting  of clear data which when through a full stack is called a cipher product.
if you feed a cipher product  multiple times  in the same full stack in a row , this is called an encryption round.
These operations can happen very fast, and even faster on custom made hardware (almost the speed of light !)

##### Data Encryption Standard (DES)
encryption standard developed by IBM, used by the US government, once widespread and a reference, 
today deemed obsolete and weak it is no longer used. The same applies for it's variant  the "Triple-DES".

##### Advanced Encryption Standard (AES)
This algorithm is the result of an open cryptography competition, stemmed by the US administration to
find a replacement for DES.
This algorithm (and all other which were proposed at the competition) had to abide to five rules 
- Symetric cypher, one block of data after the other 
- Full conception and innerworkins ought to be public
- 128 192 and 256 bits keys
- could be implemented on hardware and on software
- algorithm should be released in the public domain or alike, granting anyone the freedom to use it.
the rinjdael algorithm, designed by cryptographer Joan Daemn and Vincent Rijmen both originating from Belgium was chosen.
The fact that the designers are originating from outside the USA is a plus, the fear of the time, that the
NSA would influence cryptographers to have a backdoor in the winning algorithm is greatly reduced.
It is today a widely used standard, even implemented in the hardware of some processors.

##### Electronic Cook Book(ECB)
TODO
##### Cipher block chaining
TODO
##### Flow Cipher
TODO

#### Asymetric Key cipher (or public-private key pair)
The main problem with symetric keys cipher is always the same: how to distribute safely the key to both communicating parties.
Even worse, what do you do when you have many people you want to talk to, or who wish to talk among themselves ?
In 1976, Diffie and Hellman publicly proposed their algorithm which was of a new kind, they were using asymetric keys.
(In 1969 a british intelligence agency already had proposed this idea internally.)
Those kind of algorithm have 3 fundamental properties
Here P is a clear text message, D() is the use of the Decryption Key and E() is the use of the encryption key.
- D(E(P)) = P (obvious, or the algorithm does not work)
- It is excessively hard to deduce D from E (like algorithmically difficult problem)
- E cannot be broken, even with a chosen clear text attack.

An algorithm which respects those three properties yields interesting results :
the E() (encryption key) can be made publicly available !
Anytime someone wants to talk to you, it can use your __publicly available__ Encryption key,
and only you will be able to read the content of what was ciphered. 
It is like selling locks to talk to you, only you have the key, so the attacker 
can buy as many locks as he wants he will not be able to understand your communications !
Two agent that wish to communicate with this kind of algorithm  proceed as follow,
they encrypt data they wish to send to the other agent with the public key of said agent,
and they decrypt incoming ciphered data with their own private key.

The problem of the Man in the middle Attack still stands though, as if A and B wants to communicate
an attacker E can silently come between them , provide it's public key decrypt, read and then re-encrypt
the content, without A and B ever noticing.
This is because this family of algorithm alone doesn't provide any mean of checking who apublic key belongs to.

Asymetric key algorithms usually rely either on either the arithmetic difficulty
of factorizing big products of prime numbers (1000's bits long) or on the 
arithmetic difficulty of studying ellipses of big prime numbers.


##### Rivest Shamir Adleman (RSA)
The most widely known asymetric key cipher algorithm.
Designed in 1977, it stands the test of time and is still widely used today.
It relies on an arithmetic property,
that factorizing a big  prime nubmer is algorithmically difficult.
This algorithm being  slower than a symetric key cipher, it is usually used to exchange
"publicly"  symetric key pairs.


### Electronic Signatures
An algorithm which has the following three properties 
is called an electronic signature :
- the recipient can check the true identity of the emitter
- the emitter cannot deny information it has emitted
- the recipient (or anyone) cannot forge a valid message
  which could be thought as originating from the emitter.

You could make signature with symetric key algorithms but then
the keys would have to be held in a trusted third party, something not always available.
Instead  RSA is prefferred,
indeed this algorithm has the nice perk that public and private key can be used in either way.
If you can of  course cipher with a public key and decipher with the associated private key, 
the algorithm also work if you cipher with the private key, and decipher with the associated public key.
Note that this is a particular property of RSA, **NOT**  of asymetric cipher in general.
Now if two entity use cleverly their respective private and public key,
they can be sure that a message is originating from the rightful emitter,
and reaching the correct recipient (provided their is no Man In the Middle when the public key were exchanged.)
Note that this does not solve alone the issue of replay attacks (though you can ensure it with the addition of a timestamp).
Also note that the emitter can for example voluntarily leak it's private key and say
that a message it really emitted was in fact forged.

#### Hash function  in electronic signatures 
Guaranteeing authentication alone, rather than authentication AND secrecy is easier.
Hash functions come to our rescue.
Any good hash function must exhibit four properties
We will call "message" data  provided to a hashing function, 
and "hashed value" the result of data being processed by the hashing function.
- For any message,  it is easy to process the hash value
- For any hashed value, it is __impossible__ to guess the original message
- You cannot find (easily) two different messages such as one hashed they both exhibit the same hashed value.
  If you do find one (they exist considering a hash value accepts a message of infinite size,
  and converts it into a hash value in a finite result domain) you have found a **collision**
- A slight change of message must result in a drastic change of hashed value 
Some widely used hashing algorithm are SHA-1 (already broken),SHA-2 (stands to this day) and SHA-3(already ready for the future).

you can now process the hash value of your message, cipher it with your private RSA key.
You have now a signature which proves at the same time that  your message was not alered in any way 
and that you are the true emitter of the message.

### Public Key management
#### Certificate 
