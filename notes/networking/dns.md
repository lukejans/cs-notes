# Networking: Domain Name Service

> a unique identity that distinguishes a network node or device

## What Is a Network Address?

two main purposes:

1. provide a unique identity for each network node in a group that it's connect to
2. to find that node within the group

when a client requests a webpage from an address the server takes note of the requesting address so it can send the data back to them.

network devices have two addresses, IPv4 and IPv6 but for now we wil only be talking about IPv4.

## IP Address - (Internet Protocol Address)

an IP address can be written in a few ways but are usually seen in what is called "dotted quad" notation: `142.222.6.191`(Mohawks address). The computer than interprets this in binary form like so `10001110.11011110.00000110.10111111`.

IPv4 addresses consist of four decimal numbers separated by dots, and each of those decimal numbers is in the range 0 to 255(8 bits each), together those **four 8 bit values make up a 32-bit long address**. This means you can represent a number between 0 to ~4.3 billion (4294967295). Due to the large range of possible addresses we make good use of the bits by defining multiple logical networks.

## Classes, Subnets and Netmasks

for reasons including network traffic management and security we want to separate our networks rather than use the full range of addresses in one big network. So we must be able to logically separate these networks from each other.

### Classes

- **Class A**: networks use the **8 leftmost bits of a 32-bit network address to define 128 logical networks**: `(00000000)₂ = (0)₁₀ to (11111111)₂ = (127)₁₀` and the remaining 24 bits are used for ~16.8 million possible node addresses.
- **Class B**: networks use the **16 leftmost bits to define 16 384 logical networks**, leaving the remaining 16 bits for over 65 500 possible node addresses.
- **Class C**: networks use the **24 leftmost bits to define ~2 million logical networks**, leaving the rightmost 8 bits for ~250 possible node addresses.

**NOTE:** some of the numbers above don't seem to make sense (i.e. 8 bits should have allowed for 256 networks) - and it's because some of the bits are reserved to identify the class:

```text
legend:
 - reserved ID bits (^)
 - network bits (n)
 - node bits (H)
```

#### Class A: identified by a "0" in the leftmost bit

```text
00000000.00000000.00000000.00000000 = 0. 0. 0. 0
01111111.11111111.11111111.11111111 = 127.255.255.255
^nnnnnnn.HHHHHHHH.HHHHHHHH.HHHHHHHH
```

#### Class B: identified by a "10" in the two leftmost bits

```text
10000000.00000000.00000000.00000000 = 128. 0. 0. 0
10111111.11111111.11111111.11111111 = 191.255.255.255
^^nnnnnn.nnnnnnnn.HHHHHHHH.HHHHHHHH
```

#### Class C: identified by a "110" in the three leftmost bits

```text
11000000.00000000.00000000.00000000 = 192. 0. 0. 0
11011111.11111111.11111111.11111111 = 223.255.255.255
^^^nnnnn.nnnnnnnn.nnnnnnnn.HHHHHHHH
```

### Subnets & Netmasks

classes may introduce some new confusion on how a computer may interpret which bits of the address refer to the network part and which bits are for the node part. This is solved by having a partner value with every address that we call the **subnet mask (_netmask_)**. The Netmask specifies how many bits are used for the network and thus allowing us to also find how many are for the node address.

- netmasks are 32-bit values that use the same notation as addresses
- we assign **a _"1"_ bit for every part of the address that belongs to the network** part, and **a _"0"_ bit for the node parts**.
- this creates a new dotted quad value that we can use to make it clear how the address is constructed. You'll also commonly see a shorter notation called **CIDR (Classless Inter-Domain Routing)** which is just a forward slash followed by the number of bits used for the network part (i.e. /8 or /24).

```text
legend:
 - reserved ID bits (^)
 - network bits (n)
 - node bits (H)
 - netmask
```

#### Class A: (the last being the netmask)

```text
00000000.00000000.00000000.00000000 = 0. 0. 0. 0
01111111.11111111.11111111.11111111 = 127.255.255.255
11111111.00000000.00000000.00000000 = 255.  0.  0.  0 or /8
^nnnnnnn.HHHHHHHH.HHHHHHHH.HHHHHHHH
```

#### Class B: (the last being the netmask)

```text
10000000.00000000.00000000.00000000 = 128. 0. 0. 0
10111111.11111111.11111111.11111111 = 191.255.255.255
11111111.11111111.00000000.00000000 = 255.255.  0.  0 or /16
^^nnnnnn.nnnnnnnn.HHHHHHHH.HHHHHHHH
```

#### Class C: (the last being the netmask)

```text
11000000.00000000.00000000.00000000 = 192. 0. 0. 0
11011111.11111111.11111111.11111111 = 223.255.255.255
11111111.11111111.11111111.00000000 = 255.255.255.  0 or /24
^^^nnnnn.nnnnnnnn.nnnnnnnn.HHHHHHHH
```

**we can divide our network via a process called _subnetting_**, this is done by **taking the leftmost bits from the node part** of the address and **designate them to be part of the network bits**. We have to make sure our netmask reflects this, otherwise the computer won't understand how we've structured our network and will not be able to properly deliver our network traffic.

lets say we want to create 8 subnets:

we'll need three bits: (111)₂ = (8)₁₀ then add those bits to our class B netmask of 255.255.0.0

```text
changes to the netmask:

11111111.11111111.00000000.00000000 = 255.255. 0. 0
^^nnnnnn.nnnnnnnn.HHHHHHHH.HHHHHHHH
  |
becomes
  |
  v
11111111.11111111.11100000.00000000 = 255.255.224. 0
^^nnnnnn.nnnnnnnn.nnnHHHHH.HHHHHHHH
```

each of those networks has 13 bits left for the node part of the address, which means each of them can have over 8192 nodes: (1111111111111)₂ = (8192)₁₀.

#### The Reasons We Subnet

- traffic only needs to travel between nodes within that subnet like between servers on the server subnet and will not have to be received and processed by any outside machines.
- to manage something called a _broadcast domain_

#### Why We Use Vague Address Numbers

- some of the lower addresses are reserved for infrastructure components: routers and switches
- we can't use the first value (X.X.X.0) because it is traditionally reserved for the network's ID
- we can't use the last value (X.X.X.255) because it is reserved for network broadcasts

#### Broadcast Traffic

- sometimes we want to send information to ALL of the nodes on the network - for example a device may want to announce that it's available. In this case the nodes would use the _broadcast address_ of the network: the last node address is reserved for this purpose
- if we put all of our nodes in one large Class B network we would have over 65 500 machines sending occasional broadcasts but the problem is all of those nodes would then have to process that traffic. This is something we try to avoid and subnets are a good way to do this.

NOTE: think of subnetting like directly messaging someone rather than messaging the entire group when the message only pertains to one person

## DHCP - (Dynamic Host Configuration Protocol)

All the nodes on a TCP/IP network get an IP address to know how to reach each other. This can either be assigned directly by the admin or nodes can ask for one from a resource on the network called a **DHCP (Dynamic Host Configuration Protocol) server** and the server can respond with an address.

### MAC - (Media Access Control)

all network nodes have a **MAC** address which is a **unique physical hardware address**. This is similar to the serial number that is assigned by a hardware manufacturer. The first half of the address is assigned to the manufacturer, and the second half id unique to the specific device. **Only used for communications on a local network** otherwise you will need to know the network node IP address. Devices maintain a little table of MAC addresses within their local network.

```text
Colon-separated: 00:1A:2B:3C:4D:5E
Hyphen-separated: 00-1A-2B-3C-4D-5E
No separator: 001A2B3C4D5E
```

- typically 42-bits long
- displayed as 12**hexadecimal digits (0-9,A-F)**
- grouped into pairs separated by colons(:), hyphens(-) or without separators.

## DNS - (Domain Name System)

is a mechanism to refer to and translate an IP address into human-readable address names. **DNS** is more than just a convenience as it enables a way to balance load on critical network resources. **DNS** is really a **distributed database** with a hierarchical structure.

### Breaking Down the Address

if we look at the address of a website which has a _Domain Name_ to identify the host server, we will notice that it has three parts to it.

```text
www.wikipedia.org
|3||----2----||1|
```

These parts are read from right to left:

1. `org` - the **Top Level Domain (TLD)**, this will drive our first action.
2. `wikipedia` - when combined with TLD, forms the domain name and we'll take an action with this information next.
3. `www` - is the name of the specific node within the domain that we need to talk to - the host name

### How Does DNS Work

- the computer asks the root name server for the DNS server name for the TLD of the node's address
- the computer then asks the TLD name server for the name of the DNS server for the domain the node is in
- the computer then _resolves_ the address of the target node by requesting it the domain's DNS server of the address of the host node
- now the web browser can ask the web server on the host node for the resource it was looking for.
- the server will request the resource using the IP address then send the data it receives to the requester.
- DNS - RR format
    - Name
    - value
    - type
    - TTl (time to live)
