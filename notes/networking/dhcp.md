# Networking: DHCP

The _Dynamic Host Configuration Protocol (**DHCP**)_ is responsible for assigning devices on a network an ip address.

## scope

range of IP addresses that a DHCP server can assign to a client on its network. This can be any range that admin user sets this to.

| start IP address | end IP address | scope         |
| ---------------- | -------------- | ------------- |
| 10.0.0.1         | 10.0.0.100     | ...1 - ...100 |

## lease

DHCP servers _lease_ IP addresses to clients that are within its _scope_. If a client stays on the network it will renew its IP address, if the client is no longer present in the network the address is returned to the server and may be assigned to another client.

## reservation

a _reservation_ ensures that a specific client will always be given the same IP address from the DHCP server. Reservations are typically used for clients like servers and routers.
