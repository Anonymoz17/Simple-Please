---
aliases:
  - Classless Inter-Domain Routing

  - publish/done
---
CIDR (Classless Inter-Domain Routing) is an IP addressing scheme that replaces the older [[IPv4#Classes|classful system]] of IPv4 addresses.

CIDR is also a compact way of representing the same information that a subnet mask show.

# CIDR Notation
The CIDR notation consists of the IP address then a forward slash followed by a decimal number denoting how many bits are in the network prefix.

> [!example]+
> The **IPv4** block 191.113.112.0*/22* represents the 1,024 IPv4 addresses from 191.113.112.0 to 191.113.115.255.
> The **IPv6** block 2001:db8::*/48* represents the block of IPv6 addresses from 2001:db8:0:0:0:0:0:0 to 2001:db8:0:ffff:ffff:ffff:ffff:ffff.

#review %% this passage %%
Written as an IP address followed by a prefix length (e.g. `203.0.113.0/22`). The prefix tells you how many bits are fixed (*network portion*) and the remainder determines block size (2^remaining bits). From the notation alone you can calculate the full range and size of the block.

## Benefits of CIDR

CIDR has many benefits compared to the classful network addressing that was in use previously.

- Due to the variable-length subnet masking, you can allocate IP addresses in multiples of 2’s. This can make better use of the IP address range that was allocated as more subnets can be created within that one range.
- A smaller number of routing entries can be used to represent a large number of networks.
- With the CIDR’s hierarchical design, details of lower-level, smaller networks can be hidden from routers when traffic is moving between large groups of networks.

*Here summary explanation of last 2 points:*
- Route Aggregation
	- ISPs advertise one summary route to the internet covering all their client blocks. Outside routers don't need to know the internal breakdown — massively reducing global routing table size.
- Hierarchical Routing / Hiding Network Detail
	- Each level of the hierarchy (IANA → RIR → ISP → Business) only knows the routing detail relevant to its scope. Lower-level subnet changes don't ripple upward and affect the broader internet.

---
# Related

---