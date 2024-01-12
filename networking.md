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

### Magnetic bands 
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

### twisted pair


### coaxial cable

### optical fiber

### electromagnetic waves

#### Radiowave

#### Microwave

#### Infrared

#### light 


## Link Layer


## Media Access Control Layer

## Network Layer 

## Transport Layer 

## Application Layer

## Security
