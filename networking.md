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
####
#### OSI Model
#### TCP/IP Model
#### Hybrid IP/OSI (the one of the book)

### Standards and ethics 
#### Standards

#### Ethics

## Physical Layer

Note : As I'm no electronical engineer, 
this part really does not interests me and I've felt free to oversee many pages about the physical Layer.



## Link Layer


## Media Access Control Layer

## Network Layer 

## Transport Layer 

## Application Layer

## Security
