# Networking: Data Flow

> the transfer of information from one system to another

## Bits and Bytes

bits can be used to store a _1_ or _0_ which represents on or off (true or false). Bits are really too small to work with so so we typically put them into a group of **8 bits to form a single byte**.

- bytes are used to store a single character of data (i.e. "A", "z", "$", "8", etc.).
- we have a standard way of choosing a bit pattern for storing characters called **ASCII (American Standard Code Information Interchange)**. It's a table of 7-bit designations that we use to represent uppercase and lowercase Roman letters, numbers, punctuation and other symbols and special control characters. we usually represent these values using the decimal equivalent for readability (i.e. "A" is 65 (11000)₂)
- other languages with different alphabets use the unicode standard, which uses 2 bytes per character.
- a byte can be used for any type of visual data have it be an image, video, or text.

```text
  I       f   e   e   l       s   o       e   x   t   r   a
 73  32  102 101 101 108  32 115 111  32 101 120 116 114  97
```

### Integers

storing integer numbers in bytes we usually use 4 or 8 bytes.

- **4 bytes** - can store -2147483648 to 2147483647
- **8 bytes** - can store -9223372036854775808 to
  9223372036854775807
- the leftmost bit indicates the sign(+ or -): if its a "1" then the number is negative.
- if you exceed the range the bytes can provide you get _integer overflow_ which will loop to the opposite end of the range.

## Hexadecimal and Octal

we common use _hexadecimal_ numbers (base 16) - where the values are 0-F. Hex is more efficient as we can represent any number from 0-255 with only two hex digits but in binary we would need 8 bits (digits). Hex and octal and binary can also be easily converted to and from as they are powers of 2.

## Packets, Frames, and Segments

### Packets

breaking messages into packets improves efficiency and our computer would only have to retransmit a few tiny parts of a message that has suffered interference and it gains the ability to **interleave**.messages

- due to packets being sent separately, if a short message needs to be sent after a long message it doesn't have to wait for that long message to complete. It only has to wait for the current packet in front of it to finish before sending.
- the computer can alternate sending packets from each message.
- packets also help reduce the required storage of routers and switches while its traveling through the internet by only requiring the current packet to be stored briefly while they wait for their turn on the outbound link rather than the entire data load.
- like all traffic on the internet packets that are to be sent to the same source may take different routes meaning some of them may get caught up and received later than packets that were sent after it.
- to solve this packets are tagged with the address of the source and destination nodes. In addition the sender tags the packet with an _offset_ value that specifies the position of each packet within the message allowing the destination node to easily reassemble the packet.

### Frames and Segments

**"brackets the packet"** refers to the Transport and Data Link layers around the Network layer where the packets are assembled.

## OSI Model

the **OSI (Open System Interconnection)** model describes the functions of the internal structure and technology of computer communications by defining seven abstraction layers, allowing us to visualize the flow of data. Each layer has a **Layer Name and Function** as well as a **PDU (Protocol Data Unit)**. The top four layers are also **Host Layers** while the bottom 3 layers are **Media Layers**.

```text
        protocol             layer name
  +---- +-------------------------------------------+
  |     |   data   |       Application Layer        |
  |     +-------------------------------------------+
 host   |   data   |       Presentation Layer       |
layers  +-------------------------------------------+
  |     |   data   |       Session Layer            |
  |     +-------------------------------------------+
  |     | segments |       Transport Layer          |
  +---- +-------------------------------------------+
  |     |  packets |       Network Layer            |
  |     +-------------------------------------------+
media   |  frames  |       Data Link Layer          |
layers  +-------------------------------------------+
  |     |   bits   |       Physical Layer           |
  +---- +-------------------------------------------+
```

- **Application, Presentation, and Session Layers** all deal with data going to and from the application being run on the computer.
- **Transport Layer** is where we see a mention of _segments_ and is where the data is broken up into manageable chunks for the transmission and reassembled upon receipt while also supplying acknowledgment of successful delivery.
- **Network Layer** is where _packets_ are assembled from chunks. When transmitting this is where the segments have the source and destination IP address applied, along with other useful metadata. When receiving they are stripped as the packet is sent upwards.
- **Data Link Layer** is where packets are encapsulated into frames. The outgoing frame is assigned the MAC address of the source node and the MAC address of the next device (such as a switch or router) in the network path. The addresses are typically represented in the hexadecimal number system. Incoming frames have that information removed as they pass upwards in the stack.
- **Physical Layer** this is where the message is actually sent out from and received by the machine in bits (binary). Electrical, electromagnetic or optical signals are applied to the media being used for transmission and are sent and read accordingly./

## Network Data Flow Revisited

1. data is carved into chunks **(segments)** which are tagged with the destination IP address **(packets)** and placed in a frame destined for the "next" device.
2. the **"next" (network infrastructure)** device looks in it's MAC address table and if the destination node is attached (skip to bottom) or else send it up the chain where this process will repeat until the data lands on a router sees the destination network is local to it at which point the data is passed through the chain of switches that connect the router to the destination node
3. the destination node gets the **frame** from the last switch in the chain, extracts the packet from it and reassembles the segments to reconstruct the message.

## Network Protocols

an established set of rules and procedures that govern how data is transmitted and received between network devices. Protocols allow devices to successfully communicate regardless of any differences they may have. They take large scale processes and break them down in to smaller, more specific tasks or actions which is called the **"protocol stack** or **protocol suite**.

### Network Protocols: The Origin Story

a lot of hard work must be applied during the proposal, development, refinement, and implementation of network protocols. Here are some worldwide organizations involved in the development of these protocols.

- **IEEE (Institute of Electrical and Electronics Engineers)**: this group defines the standards and protocols for Ethernet and Wi-Fi networking, as well as Bluetooth.
- **ISO (International Organization for Standardization)**: they are behind the 7-layer OSI model and they have defined standards that impact all aspects of computing.
- **IETF (Internet Engineering Task Force)**: maintains and manages internet _RFCs (Requests for comment)_ in which defines the key underlying technologies that support the internet.
- **W3C (World Wide Web Consortium)**: standards define what they call the _"Open Web Platform"_ that enables web access on any device and includes protocols such as HTML and CSS.

### Communications Protocols

#### network transportation

- **TCP/IP**
- **TCP/UDP (User Datagram Protocol)**
- **TCP(Transmission Control Protocol)**: designed to send packets of data and other messages across a network and to ensure that they are successfully delivered. It works by establishing a connection between two machined called the server and the client. The client initiates the connection to a listening server over a specific port. Web browsers, E-mail system, and file transfer protocols rely on the features of TCP.
- **IP (Internet Protocol)**: transport layer that defines the structure of the packet containing the data that we want to send. Networking hardware uses the address data applied to the packet as per the Internet Protocol to route it from the course to its final destination. IP on its own only provides a best-effort delivery service and needs to work with a connection oriented stateful protocol such as TCP.

#### file transfer

- **SMB (Server Message Block)**
- **NFS (Network File System)**
- **FTP (File Transfer Protocol)**
- **SCP (Secure Copy Protocol)**

### Network Management Protocols

- **SNMP (Simple Network Management Protocol)**: allows administrators to view and modify network device information to alter their behavior. This relies on the use of agents to collect and send data to an SNMP manager, which in turn queries agents and gets their responses.
- **ICMP (Internet Control Message Protocol)**: designed to validate and test network links and assist in network troubleshooting and communicates error messages.

### Security Protocols

- **SSL (Secure Sockets Layer)**: a network security protocol primarily used to secure internet connections and protect sensitive data - note: related protocols include _SFTP_ and _HTTPS_.

### Multi-Protocol Modular Design

you can swap out protocols for what you prefer while still receiving the overall service promised. For example, if we are using the TCP/IP to log into a remote computer we have a variety of application-level protocols to choose from (telnet, ssh, etc.), but all of these still interact with the lower level protocols in the same way.

## Ports

network nodes such as a server get assigned an IP address just like other devices so they can communicate with one another. If the server wants to host more than one service it will have to utilize ports. when combined with IP addresses it will create sockets.

```text
yourcomputerIP:port    mycanvasIP:port
192.168.0.10:61572     52.60.148.28:80
             |---|                 |-|
```

## TCP and UDP

- both transport layer protocols
- TCP is connection oriented
    - allows for retransmission of lost packets.
    - creates a two way link between nodes with sockets.
    - when the connection is established communication can start.
    - built in mechanisms to check for errors and packet loss, and guarantees data can be reassembled.
    - due to its reliability it consumes more network resources.
- UDP is connectionless
    - each frame is sent independently
    - slightly faster than TCP
    - more simple protocol typically used when error checking and recovering is not needed
    - not ideal for email, surfing the web, or downloading data files
    - ideal for streaming audio and video where a few missed or delayed frames aren't critical as its a live feed so going back may be unnecessary.

## Stateless vs Stateful Protocols

### Stateful

- when a client sends a message to a server using a stateful protocol it expects some sort of response.
- contain a mechanism to remember and store details of the interactions they facilitate.
- TCP is a stateful protocol
- FTP is stateful as it remembers the client and the location with the file system.

### Stateless

- does not require the server to provide status information or retain other information about the state of requests
- UDP is a stateless protocol
- HTTP is stateless as every web page request is independent and not part of an ongoing _"session"_.
