# Networking: Ports

> uniquely identify a connection endpoint and to direct data to a specific service
>
> you can think of port numbers in the following way, **system address + port numbers** are analogous to **apartment buildings + apartment unit**.

With TCP/IP networking you must use a socket (IP address + port number) meaning you never are just connecting with an address. The port number is either implicitly set or you have to set it. Both TCP and UDP transport protocols use ports. A port is a **number between 0 and 65535**.

When writing a network application, programmers create a type of file descriptor called an **internet socket** that combines the specification for the transport protocol, the IP address and the port number. This is called **_binding_** - it's how a socket is created.

The OS now transmits outgoing data from all the application ports onto the appropriate network and forwards incoming packets to running processes by matching the IP address and port number to a socket.

In situations where many incoming connections are expected (web server), a commonly used technique has one process monitoring the port for incoming requests called the **listener** that then hands off the incoming clients to other processes to do the work requested so it can immediately go back to monitoring incoming connections.

**Port Ranges:**

- well-known: `0-1023`
- registered: `1024-49151`
- dynamic / ephemeral: `49152-65535`

## Well-Known Ports

when browsing the internet you access website with a human readable domain name which gets resolved from a DNS resolver to find the IP address but we still need the port number. This is specified at the front of the url with the protocol being used `http` or `https` and many other protocols. When the browser sees you're using `http` it will automatically choose `port 80` when connecting to the remote machine. The reason it does this is because it is a **well-known** port number. Note that port 80 is used on for connecting to the server and not for web clients so your web browser choses a random port number from a specific range withing the port number range. A potential interaction may look like the following:

```text
  __                              _
 [  ]  ------------------------  |*|
====`o                           |_|
192.168.0.10:60189             52.60.149.28:80
```

as seen above, common services are assigned to what is called a _well-known_ port. The **well-known port range is `0-1023`** but 0 is reserved so it doesn't really count. This range is for system-level services such as E-mail, printing, web services, databases, directory services, etc. In most operating systems for a process to bind to a well known port it must be running as an administrator (root). This is in place to restrict client nodes from interfering with infrastructure level ports.

## Registered Ports

Ports in this range are not controlled or assigned and processes run by regular system users are permitted to bind to them. The **registered port range is `1024-49151`**. On some operating systems this range can overlap with another range but generally this range is safe to use as registered ports. Not all software applications are granted a well known port so software developers can use this range for their applications. Still only one application can use the port (the first to declare it otherwise, port is in use) so there may be cases where a user has conflicting ports but developers often allow users to configure what port number to use in these cases. A registry of these ports has been established so that the default port used by the programmers application is less likely to conflict with another port.

## Dynamic / Ephemeral Ports

The remaining port numbers are set aside for what are known as **dynamic ports**, **ephemeral ports**, or sometimes **private ports** in which all refer to the same **range which is `49152-65535`**. Some operating systems that routinely simultaneously run a large number of client applications (e.g. Linux) use a **range of 32768-65535**. The intention of these ports is to only be used for a short time (duration of a session). These ports are allocated as needed on a temporary basis and are released and available for reuse when the session is over. This is like the above example with http assigning a random port in this range for the client.

## Commonly Used Ports

| port # | service          |
| ------ | :--------------- |
| 20     | FTP (Data)       |
| 21     | FTP (Control)    |
| 22     | SSH              |
| 23     | Telnet           |
| 25     | SMTP             |
| 53     | DNS              |
| 67     | DHCP (server)    |
| 68     | DHCP (client)    |
| 69     | TFTP             |
| 80     | HTTP             |
| 88     | Kerberos Auth    |
| 143    | IMAP4            |
| 389    | LDAP             |
| 443    | HTTPS            |
| 445    | Active Directory |
| 445    | SMB              |
| 873    | Rsync            |
