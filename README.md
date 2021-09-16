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