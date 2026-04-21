# Networking: Structure

> an interconnected chain, group, or system of devices

## What Is the Internet?

consists of billions of attached computers and related devices. The internet is really a network that is built from other, smaller networks. Traffic on networks is highly structured and follows the rules of various standards and protocols.

- a device on a network is called a **node**.
- a **node** that provides a service is called a **host**.
- devices are interconnected by some form of a communication link.
- the medium used for each connection can vary and all have different. advantages and limitations such as maximum transmission speed **(bandwidth)**.
- **hosts** often called **servers**, provide resources / data that is consumed by other "end devices" **(clients)**.
- **routers** and **switches** are responsible for _forwarding "traffic"_ between other nodes.

## Typical Structure

like any network, the host machines are there to provide some form of service hence them being called _servers_. They provide a well-defined interface to their services. Clients run a local applications and use the defined _"hooks"_ to send and receive data from and to the server applications.

### High-Level Overview

large networks are typically built using a three layer design.

1. **Core Layer** - the heart of the network where interconnected **_routers_ and _switches_ connect the network to other networks**. You will also find core network services at this level such as application servers and network-based attached storage.
2. **Distribution Layer** - **connects the core layer to the next layer**, this layer takes on a lot of the heavy lifting of **routing and filtering traffic**. some network designers prefer to have this layer connect to other networks, rather than at the core layer.
3. **Access Layer** - connects the distribution layer to the end-point device (computer, printers, etc). Mobile devices are connected via wireless access points **(APs)**. If an access layer device fails only devices directly connected to it will go off-line.

## Network Data Flow

refers to data being requested and transmitted through the internet to be received by an end-point device.

### Packets

packets are used to help with network interference and bottlenecks. They allow you to start reading data before all of it is received. If data is lost with packets all you have to do is resend the packet that was lost rather than all the data again.

- you can send more than one message at once by alternating sending packets for each message. (allows you to request other unrelated data at the same time)
- we most commonly use **Ethernet** and **TCP/IP** networks. Given this we can send the packets on whichever pathways, or _routes_.
- packets take whatever the best route is at that moment, then use a different route for other packets later if needed. Similar to GPS where it evaluates what the fastest route to a destination is.

## Ethernet

The most prevalent method today for data is Ethernet. Like most other network types, Ethernet leverages the use of packets.

## Hubs, Switches and Routers

these devices are what physically connect the various parts of a network together, wireless access points (AP) also fall into this category.

### Hubs

hubs and switches serve a similar purpose in that they connect end points and other hubs and/or switches to the network.

- hubs are an older technology and are kind of dumb, **they just pass everything along to every connected device**, without any regard to the source, destination or any aspect of the data they work with.
- today, hubs are only used in special circumstances.

### Switches

**primarily responsible for connecting devices to a network**. they have sockets on them **(ports)**, into which we attach network cables.

- switches come in different configurations, with different port types and quantities, varying speeds and capabilities, with or without the ability to remotely manage them.
- switches are more intelligent then hubs as they examine each chunk of data that they receive and decide how to handle it.
- they **identify the destination device each chunk of data is intended for**, and if that device is connected to one of its ports (even if the intended device is connect to a another switch that itself is connected to one of its ports), it will send the data to that port - otherwise it will ignore it.

### Routers

**responsible for forwarding data between networks** (or between segmented parts of a larger network - mainly for security purposes).

- some switches have the capabilities of routers and can assume some of their responsibilities but networks will typically rely on routers for these jobs.

#### Routers and the Internet

when you break it down, the internet is really just a collection of cooperating routers that hand data traffic to the next device in the chain. For example a request to Google will create a route between your machine and one on Googles network hoping from router to router around the world until it reaches its destination.

## Types of Networks

- LAN: Local Area Network
- WAN: Wide Area Network
- MAN: Metropolitan Area Network
- PAN: Personal Area Network

### LAN - Local Area Network

**LAN** is a collection of devices that are all connected together in one location such as a home or an office. LAN can support one user or thousands. LAN infrastructure includes cables, switches and routers. When wireless networking is added to a LAN, the wireless part is called a **WLAN (Wireless Local Area Network)**.

### WAN - Wide Area Network

**WAN** is a collection of LANs that are geographically dispersed - for example, if a company has offices in Hamilton, Toronto, Montreal, and Vancouver or even Hong Kong and they would interconnect each location's LANs, forming a WAN. WANs are really networks of networks, routers are the main infrastructure we identify as being part of a WAN. There is also **WWANs (Wireless Wide Area Networks)**, which is using cellphone infrastructure to add devices and locations to a WAN.

### MAN - Metropolitan Area Network

**MAN** is in between a LAN and WAN, and is generally described as a LAN that includes other buildings that are in the same city or geographic region. A similar network type is a **CAN (Campus Area Network)** that's really a large LAN spread across a number of buildings in the same general location.

### PAN - Personal Area Network

**PAN** describes a network of devices within a person's workspace or even worn or carried by a person. PANs usually have a gateway device that bridges the PAN to a LAN or WAN. Most PANs are really **WPANs (Wireless Personal Area Networks)** that connect low-powered (therefore short-distance) devices via technologies like Bluetooth (i.e. smart watch, headphones, etc.), although short-distance wired links such as USB are often used.

## Network Media

network signal travel is called network media, we can use **bounded** (cable/wire connection) or **unbounded** media type (wireless). Wireless systems are mainly a "last mile" connection type - cables are the majority of the network media that we work with due to reduced _interference_.

### Bounded

**bounded** media types are wires or optical fibre because they are bound within a cable. Cable media has to be run from a source location to every point you want to be able to attach network nodes and other infrastructure which can be more expensive and a bigger logistics issue.

#### Cables

- **copper coaxial cable** - cable modem connecting to your ISP (internet service provider) link outside your home. Not an ideal cable type for modern in-building networks due to its data carrying limitations.
- **twisted pair cable** - cables are twisted to improve performance and reliability, they are used for connecting a cable or DSL modem to a Wi-Fi router, going from your desktop computer to the router or connecting workstations in any office or lab to the institutional network. This is the most common type used for modern in-building networks.
- **fibre optic cable** - these are more delicate so they aren't used on end-point devices as they are made out of very narrow glass fibres, they are mainly used to connect infrastructure devices together. These cables use light instead of electricity and because of this they do not suffer from any form of electromagnetic interference. Capable of high speed data transfer.

### Unbounded

**unbounded** media refers to wireless communication using a radio system (eg. Wi-Fi, Bluetooth, etc.). Wireless systems are great for mobile devices and laptops and not have concern about having a nearby network jack. Unfortunately wireless systems are more prone to _interference_ compared to bounded media types.

- **Wi-Fi** - the most common wireless network connection.
- **Bluetooth** - mainly used to connect peripherals (i.e. earbuds) to an endpoint devices like a phone.

## Detecting Collisions

### Ethernet Collisions

The method used on ethernet networks is called **CSMA/CD** with the **CD** standing for collision detection. This can sense another device transmitting, and will stop and wait for things to quiet down before it starts again.

### Switches / Routers Collisions

Network switches and routers will only transmit data on a given port if the data is intended for a host on that port. Although some issue may still arise given that a switch can be connected to a port on another switch meaning multiple devices may request data at the same time.
