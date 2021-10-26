# PC-Networking

---

## Chapter 1 : Introduction

## Chapter 2 : Small practice overview

## Chapter 3 : The basics of communication

## Chapter 4 : Networking topologies

## Chapter 5 : Communication models

## Chapter 6 : Ethernet

## Chapter 7 : Wireless LAN

## Chapter 8 : Network without new cables

## Chapter 9 : Cable Internet Access

## Chapter 10 : DSL

## Chapter 11 : Wireless Internet Access

## Chapter 12 : Internet Protocol

## Chapter 13 : Address Resolution Protocol & Neighbour Discovery Protocol

## Chapter 14 : Internet Control Message Protocol

## Chapter 15 : Transmission Control Protocol

## Chapter 16 : User Datagram Protocol

## Chapter 17 : DHCP

## Chapter 18 : Name Resolution

## Chapter 19 : Simple Networking Management Protocol

## Chapter 20 : Zeroconf

## Chapter 21 : Universal Plug and Play

## Chapter 22 : Networking cables

## Chapter 23 : Networking cards

## Chapter 24 : Switches

## Chapter 25 : Set up Windows

## Chapter 26 : Set up Linux

## Chapter 27 : Set up macOS

## Chapter 28 : Troubleshooting

## Chapter 29 : Additional Apps

## Chapter 30 : Determining network speed

## Chapter 31 : Remote administration and collaboration

## Chapter 32 : Security and data protection in the LAN and on the Internet

## Chapter 33 : Network Security Programs

## Chapter 34 : WLAN and Security

## Chapter 35 : Encryption

## Chapter 36 : Internet Access

## Chapter 37 : DynDNS-Services

## Chapter 38 : Network Storage

## Chapter 39 : Virtualization

## Chapter 40 : Virtual Appliences

## Chapter 41 : siegfried5 - a more versatile server

## Chapter 42 : Network Backup

## Chapter 43 : Media Streaming

## Chapter 44 : Voice over IP ( VOIP )

## Chapter 45 : Cloud-Computing

## Chapter 46 : Home Automation

## Chapter 47 : Raspberry Pi

---

## Introduction & Small Practice Overview

Informations about the book and a small practice example.

---

## Chapter 3 - The basics of communication

Before we look at how communication takes place inside a network let's think about communication rules on the daily basis.
When we think about communication on the daily basis we have the following components:

- Sender
- Receiver
- Communication/Transmission medium
- Rules
- Content encoding

The sender and receiver are pretty logical. One of the communication/transmission medium in our case is air for example. The rules are for example, not talking with your mouth full or you can't interrupt people while they're talking. The content encoding should be for example the language that you are using, the grammar, etc.

If we look at network communication it is the same. We need a sender, a receiver, a transimission medium, rules and content encoding.
But what is a network ?
A network is the connection between at least 2 PCs.

---

## Chapter 4 : Networking topologies

There are multiple networking topologies. The term topology also mean structure or layout.

### Bus topology

The bus topology contains of a central cable that is connected to all the other stations ( PCs, Latops, Printers, etc. ). If the central cable doesn't work anymore, everything stops working.

![Bus Topology](/ScreenshotsForNotes/ScreenshotsChapter4/BusTopology.PNG)

### Ring topology

The ring topology is very similiar to the bus topology. As the name says, all the stations are put in the form of a ring. We have the central cable and, on top of that, a Token. The token is a sort of cart that transports messages from one station to another and moves around the ring and when a station has a message to receive or transport, it can be taken out or put inside that token.

![Ring Topology](/ScreenshotsForNotes/ScreenshotsChapter4/RingTopology.PNG)

### Star topology

Inside the start topology, you have a central station, called a HUB that controls the data flow of the stations that are connected to it.

![Star Topology](/ScreenshotsForNotes/ScreenshotsChapter4/StarTopology.PNG)


## Chapter 5 : Communication models

Communication models were created in order to better describe the communication inside a network.

There are 2 main models:

- DoD-Model ( Department of Defense )
- ISO/OSI-Model ( International Organization for Standardization )

The OSI Model stands for Open System Interconnection Model.

The DoD Model is a condensed version of the OSI Model so I will only explain the OSI Model.

The OSI model consists of 7 different layers

### Layer 7. Application layer

Look at the following example:

![OSI Example](/ScreenshotsForNotes/ScreenshotsChapter5/OSI_Example.PNG)

Let's say that 10.0.0.3 is a web server having a web application and 10.0.0.5 wants to consume it. 
The client, so the 10.0.0.3 phone, goes into a browser and types 10.0.0.3:80 ( 80 is the port ) and will click enter which translates to a get request that is being sent to the web server. The get request sends a lot of information like headers, cookies, content-type headers, etc. This is what happens inside layer 7, the application layer.

### Layer 6. Presentation Layer

The presentation layer, as the name indicates, is about how the data is presented. The data might be for example encrypted or not. HTTP doesn't encrypt the data while HTTPS ( which stands for HTTP Secure ) encrypts it.

### Layer 5. Session Layer

Since in our example we are using HTTPS, which is a connection based architecture, each data that is sent is 'tagged' with a session. So each data that is transported has a session ID.

### Layer 4. Transport layer

The transport layer is all about how we choose to transport the data. We usually have to break data down into more parts ( that are unified by the session ID, so each data part that is broken down keeps that specific session ID so they can all come together in the end ). There are 2 different ways of sending data:

- TCP ( Transmission Control Protocol )
- UDP ( User Datagram Protocol )

#### TCP

When you look at a web-page or download an email you expect the data to be complete so you don't only get to see half of the web-page and you expect it to also be in order so you don't get to see the footer first and the header last. 
In order to make sure that you get all the data packs and that you get them in order you must use **TCP**. It ensures that all the data is received and, in order. 
**TCP is a connection oriented protocol** which means that it must first acknowledge a session between the two computers that are connected. It does this by using a **3-way handshake**. A computer will send a message called a SYN. The receiving computer will send back an acknowledgement called a SYN ACK telling the sender that it has received the message. Finally, the sender computer sends another acknowledgement message back to the receiver called ACK RECEIVED

![TCP Example](/ScreenshotsForNotes/ScreenshotsChapter5/tcp.PNG)

**Once this has taken place, data can be delivered.**

TCP guarantees the delivery of data. If a data packet doesn't arrive, TCP will resend it.

#### UDP

UDP is very similiar to TCP however, **UDP is a connectionless oriented protocol** which means that is doesn't establish a session and it doesn't guarantee data delivery. When a computer sends data, it doesn't care if the data is received or if the data that is being received, is in order.

Because it doesn't guarantee data delivery, it is faster than TCP.

### Layer 3. Network layer

As we said before, in the transport layer, data is destructed into more data segments that eventually also contain a session ID ( if working with TCP ). Inside the network layer **each data segment** is destructed into more packets. Every network packet has a header that contains information about the data ( origin, destination, etc. ).
The network network layer doesn't know what port the data is assigned to, that was left out from the transport layer

### Layer 2. Data link layer

Inside the data link layer we will break **every single packet from the network layer** down into more frames. The way it is broken down doesn't matter ( it might break things like origin an destination IP, bits of data, etc. ). 
On top of breaking every single network packet down, it adds some more information to the headers of the frames, it adds for example the target MAC address. 
These frames are the smallest bits since the data has been already broken down into segments ( inside the transport layer ), packets ( inside the network layer ) and frames ( inside the current layer ). The data link gets into touch with the physical medium.

Sometimes you don't know the MAC address. This is where the **ARP ( Address Resolution Protocol )** can reverse engineer the IP Address into the MAC Address. 

The data link layer doesn't know the IP's of the origin and destination devices, it was left out inside the network layer

### Layer 1. Physical layer

After we have destructed the data into segments, packages and frames and we have established inside the frame the mac address we go into the physical layer which converts everything that we had inside the data link frames into bits ( 1's and 0's ). From this point on, we reverse everything back to the application layer.

We have this sequence of bits that is basically a flow of electricity and this sequence of bits will go to all the devices that are bound to the main network device ( like a router for example ). We will now start going up the osi model. 
We will then start with the data link layer by going to the last sent frame ( remember that the data layer transforms each segment of data into frames ). Each frame contains the MAC address of the destination device. So when we send this flow of bits to all devices, every device will go back to the frame inside the data link layer and will check the MAC address. If the MAC address of the frame and the MAC address of the device is not the same then that means that, that device is not the destination device so it will just not accept the data.

This is the one of the reason why you shouldn't connect to public wi-fi since everything that you send over a public network will automatically be sent to all the other devices that are currently connected to that network and while you might think that the network card rejects all the dl-layer frames that don't correspond to the current MAC address, you can use something like Wireshark in order to get those frames and if you used a website on layer 7, the application layer, that doesn't use HTTPS ( HTTP Secure ) and that doesn't encrypt your data, everybody on the network will be able to see your private information.

The data link layer will then send back a 'cleansed' version of the frame without the MAC address ( a version that contains the IP address of the destination device ) to the network layer.

From the network layer we will go back to the transport layer where we will send the network packages without the IP Address, we will just give it the port since it already has the MAC and the IP. So now we have the PORT.

From the transport layer we will go back the the session layer so we know to what session the data belongs to.

From the session layer, everything is optionally decrypted ( only for HTTPS ) inside the presentation layer and finally you get back the data from the GET Request from the server.

Shortly explained again:

We have one router ( 10.0.0.1 ) and we have 4 devices that are connected to that router ( the MAC Addresses are A, B, C, D and F )

![Example Connection](/ScreenshotsForNotes/ScreenshotsChapter5/Example_Connection_1.PNG)


Let's say that 10.0.0.3 is a web server and the phone ( 10.0.0.5 ) wants to consume it:

![Example Connection 2](/ScreenshotsForNotes/ScreenshotsChapter5/Example_Connection_2.PNG)

Let's say that the web server has that web application on the website https://www.example_app.com. So you go on the phone and type inside the browser "https://www.example_app.com". The moment you press enter and go on the website, a GET Request will be sent to the server that contains the IP address of the phone, the port where it was connected to, http headers, cookies, content-type, etc.

![Layer 7 Application Layer Example](/ScreenshotsForNotes/ScreenshotsChapter5/Layer7_Example.PNG)

Since we are using HTTPS, which stands for HTTP secure, in our example, we will have a new layer added to the network model. That layer is called the presentation layer and as the name says, it's about how we present our data. In this case we will encrypt the data since we are using HTTPS.

![Layer 6 Presentation Layer Example](/ScreenshotsForNotes/ScreenshotsChapter5/Layer6_Example.PNG)

Since we are using HTTP/HTTPS, which is a connection based architecture, we get to get session layer, which is layer 5. The session layer sets a sesssion ID to the data passed since we might build more connections to multiple devices we have to know where data comes from, we must keep track of its origins and its destinations.

![Layer 5 Session Layer Example](/ScreenshotsForNotes/ScreenshotsChapter5/Layer5_Example.PNG)

After the encrypted data has a session ID we get down to the transport layer. In the transport layer we destruct the data into multiple segments where we add the ports ( origin and destination ports inside the headers ).
In the transportation layer we can choose if we want to use TCP or UDP. Shortly explained if we want to use TCP, the phone will send a message to the server called a SYN. If the server will receive the message it will send a message back to the phone called SYN ACK ( acknowledgment ). The phone, if it will receive the SYN ACK, will send a message back to the server telling it that he has received the acknowledgement ( ACK RECEIVED ). This is called a 3-way handshake. After this handshake the data will start to be sent between the server and the client. During the transmission, the server will always make sure that the phone gets **all the data in order**. UDP on the other hand doesn't care if you get the all the data or if it is in order.

![Layer 4 Transport Layer Example](/ScreenshotsForNotes/ScreenshotsChapter5/Layer4_Example.PNG)

After the transport layer we come into the network layer. In the network layer **each data segment inside the transport layer is destructed into network packets**. The packets have no information about the ports ( neither origin nor destination ). We got rid of the ports and put the IP addresses of the origin and destination devices inside the headers. It looks just like a russian doll if you think about it.

![Layer 3 Network Layer Example](/ScreenshotsForNotes/ScreenshotsChapter5/Layer3_Example.PNG)

After we passed the network layer we get into the data link layer. In the data link layer **each network packet is destructed into more segments**. The segments don't know the IPs of the origin or destination devices, they only have the MAC addresses.
Sometimes you can't find the mac address, this is where you can use the ARP ( Address Resolution Protocol ) that takes the IP address and reverse engineers it into the MAC address.

![Layer 2 Data Link Layer Example](/ScreenshotsForNotes/ScreenshotsChapter5/Layer2_Example.PNG)

After the data link layer we go to the physical layer where every piece of data inside the frame is transformed into 1's and 0's, into an electrical flow of 1's and 0's. 

![Layer 1 Physical Layer Example](/ScreenshotsForNotes/ScreenshotsChapter5/Layer1_Example.PNG)

Electricty doesn't have a direction. This 1's and 0's will go to all the devices that are connected to the router.

![Layer 1 Physical Layer Going through all devices Example](/ScreenshotsForNotes/ScreenshotsChapter5/Layer1_Example_AllDevices.PNG)

Now from the physical layer we go back to the data link layer where each frame contains the MAC address. So after the 1's and 0's of data are going to all the devices that are connected to that network, the next thing that will happen is going to the frame in the data link layer that contains the MAC addresses of the origin and destination devices inside the header. If the MAC addresses are not the same, then the devices won't accept the frame and will stop the propagation on the other layers.

![Layer 2 Data link layer backwards Example](/ScreenshotsForNotes/ScreenshotsChapter5/Layer2_Example_Backwards.PNG)

Now that we know the origin and destination devices because of the frames from the data link layer that contain the MAC addresses inside the headers we just propagate back to the seventh layer, the application layer, in order to put the data on the website.
We will go from the data link layer to the network layer that contains the IP addresses inside the headers of the network packets. From the network layer, which is the third layer, we will go to the fourth layer which is the transport layer that contains the ports inside the headers of the data segments. Afterwards we will go to the fifth layer which is the session layer so that we know to what session the data belongs to. We will eventually also go through the sixth layer, which is the presentation layer, in order to decrypt the data ( if we have used HTTPS, which stands for HTTP Secure that encrypts the data ). And finally we will get the response to our GET Request from the server.

![Propagation finished Example](/ScreenshotsForNotes/ScreenshotsChapter5/get_found.PNG)

## Chapter 6 : Ethernet

### Subchapter CSMA/CD && CSMA/CA

**CSMA/CD ( Carrier Message Multiple Access with Collision Detection )** is a protocol used inside topologies like the bus topology in order to avoid collisions and also handle them correctly in case that they occur. Take a look at the following diagram:

![CSMA/CD Example Diagram](/ScreenshotsForNotes/ScreenshotsChapter6/CSMA_CD_Screenshot.PNG)

If a PC wants to send a message, it must wait for the main cable to be idle. Once the main cable is idle, it will sends its message. If two computers sense that the main calbe is idle and send a message at the same time, a collision will occur. 
When a collision occurs, the computers will send a **jamming** message to the entire LAN informing that a collision took place. Afterwards, the computers that caused the collision will both wait a random amount of time before trying to send their message again through the main cable.
The CSMA/CD protocol was used back in the day where we had half-duplex. Nowadays we are using full-duplex. Half-duplex means that communication can be in both directions but can't follow simultaneously.

**CSMA/CA ( Carrier Message Multiple Access with Collision Avoidance )** is a protocol used in wireless networks. Take a look at the following example:

![CSMA/CA Example Diagram](/ScreenshotsForNotes/ScreenshotsChapter6/CSMA_CA_Screenshot.PNG)

In this case a computer can't listen to any main cable to be idle before sending its message. It must sense other transmissions and if it doesn't sense any it can send its message. If a transmission is sent, it will wait a random amount of time before trying to send its message again through the network. Once the message is send, the receiver device will also send an acknowledgement message back to the sender device. If this message isn't received by the sender device then the entire process will start again.

### Subchapter Ethernet Cables -> Twisted Pair

Twisted pairt cables are the ethernet cables that are used nowadays. One end is plugged into the network interface card ( NIC ) of a device while the other end is plugged into the router's/modem's end for internet access. 

Twisted pairs cables come in two variations:

* UTP ( Unshielded Twisted Pair ). UTP consists of 4 pairs of color-coded wires twisted around each other. The wires are twisted in order to avoid any electriomagnetic interference.
* STP ( Shielded Twisted Pair ). STP is the same as UTP but it also has an extra layer of shield on the wires in order to avoid electromagnetic interference leaking inside or outside the wire.

Twisted pair cables have at their end an RJ45 connector.

### Subchapter VLAN

In a VLAN ( Virtual Local Area Network ) devices are logically connected regardless of their physical location. Let's say that you have 3 departments inside a building that are all connected to one LAN. It would look something like this:

![Why do we need VLAN Example Diagram](/ScreenshotsForNotes/ScreenshotsChapter6/VLAN_Screenshot_1.PNG)

You can see that the LAN is very unstructured and the worst thing about this kind of LAN is that all the departments can see each other's messages. 
VLANs are created for:

* improved security
* traffic management
* to make a network easier 

This is how this network would look like with a VLAN:

![VLAN Example Diagram](/ScreenshotsForNotes/ScreenshotsChapter6/VLAN_Screenshot_2.PNG)

VLANs are created by assigning certain ports to certain parts of the network that we want to divide:

![PORT Dividing VLAN Example Diagram](/ScreenshotsForNotes/ScreenshotsChapter6/VLAN_Screenshot_3.PNG)

### Subchapter Promiscuous Mode

When we use a HUB inside a network, the hub redirects the messages that it gets to all the devices inside the network. Naturally, the devices read the receiver MAC address of the message and if the receiver's MAC address doesn't coincide with the device's MAC address, then the message it is rejected. However, there are some workarounds for this type of problem. We could use something like wireshark in order to save all the messages that we get from outside networks regardless of the receiver's MAC address. This is called promiscuous mode. Promiscuous mode is basically eavesdropping on a network.

### Subchapter Unicast, Multicast, Broadcast

Unicasting means that a message goes from a host to only one device of a LAN. Broadcasting means that a message goes from a hsot to all the devices of a LAN. Multicasting means that a message goes from a host to multiple devices from a LAN ( not all ).

### Subchapter Ethernet Datagramm

When a message is sent through the ethernet, the message contains 7 frames:

![PORT Dividing VLAN Example Diagram](/ScreenshotsForNotes/ScreenshotsChapter6/EthernetDatagramm.PNG)