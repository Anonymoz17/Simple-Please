---
aliases:
  - Internet Protocol version 4

  - publish/done
---
Internet Protocol version 4.

This version uses 32-bit addresses. This limits the amount of addresses to about 4,294,967,296 possible unique addresses. Some of these addresses, about 290 million, are also reserved for special purposes. IPv4 is most commonly used and currently assigned to all computers.

- **Address size**: 32-bit
- **Format**: Dot-Decimal Notation (e.g., 192.168.1.1)
- **Total addresses**: 4,294,967,296
- **IPSec**: Optional
- Widely used but facing address exhaustion

---
# IP Address
An IP address always consist of 4 numbers separated by dots. The numbers have a possible range from 0 to 255. Example:
**172.16.254.1**

![[IPv4 Address Drawing|600]]

This representation of the IP address is called the dot-decimal notation. This consists of 4 octets of the address expressed individually in decimal numbers separated by periods.

> [!info]- Other Types of Address Representations
> The quad-dotted IP address 172.16.254.1 represents the 32-bit decimal number 2886794753, which in hexadecimal format is 0xAC10FE01.
> **But Dot-Decimal notation is mostly used to represent IPv4 addresses**.

---
# Classes
In the IPv4 IP address space, there are five classes: A, B, C, D and E. Each class has a specific range of IP addresses (and ultimately dictates the number of devices you can have on your network). Primarily, class A, B, and C are used by the majority of devices on the Internet. Class D and class E are for special uses.

> [!important]+ 
> This is only for historical context and a basic understanding of classful system if any old references are made about it. The classful system is considered **obsolete** since the [[CIDR]] was adopted in 1993. Everything today is based on CIDR.

## Class A
Class A IP address ranges are typically used by Internet service providers and large corporations such as Google and Apple.

| IP Type | Range                            |
| ------- | -------------------------------- |
| **Public**  | `1.0.0.0` to `126.255.255.255`   |
| **Private** | `10.0.0.0` to `10.255.255.255`   |
| **Special** | `127.0.0.0` to `127.255.255.255` |
- **Subnet Mask**: `255.0.0.0` (8 bits)
- **Number of Networks**: 126
- **Number of Hosts per Network**: 16,777,214

## Class B
Class B IP address ranges are typically used by universities and medium-sized businesses.

| IP Type | Range                            |
| ------- | -------------------------------- |
| **Public**  | `128.0.0.0` to `191.255.255.255` |
| **Private** | `172.16.0.0` to `172.31.255.255` |
- **Subnet Mask**: `255.255.0.0` (16 bits)
- **Number of Networks**: 16,382
- **Number of Hosts per Network**: 65,534

## Class C
Class C IP address ranges are typically used by small businesses and home networks

| IP Type     | Range                              |
| ----------- | ---------------------------------- |
| **Public**  | `192.0.0.0` to `223.255.255.255`   |
| **Private** | `192.168.0.0` to `192.168.255.255` |
- **Subnet Mask**: `255.255.255.0` (24 bits)
- **Number of Networks**: 2,097,150
- **Number of Hosts per Network**: 254

## Class D
Class D IP address ranges are typically used in multicast streaming services (e.g., video conferencing). Unlike Class A, B, and C, IPs in this class are not 'owned' by a specific entity. They are instead **used temporarily and within an enterprise network** for streaming content to multiple recipients simultaneously over their networks.

**IP Range**: `224.0.0.0` to `239.255.255.255`

## Class E
Class E IP addresses are not allocated to hosts and are not available for general use. These are reserved for research purposes.

**IP Range**: `240.0.0.0` to `255.255.255.255`

---
# Special IP Addresses

- `0.0.0.0`
    - **Name**: Unspecified address
    - **Purpose**: "This host (unknown address)"; used as a source before a host gets an IP. Not assigned to interfaces. (Default route is `0.0.0.0/0` different concept.)
    - **Globally Routable?**: No
- `255.255.255.255`
    - **Name**: Limited broadcast
    - **Purpose**: Broadcast to the local (layer-2) network only; routers must not forward.
    - **Globally Routable?**: No
- `127.0.0.0/8`
    - **Name**: Loopback
    - **Purpose**: Host-internal traffic (e.g., `127.0.0.1`); never leaves the device. These are virtual IP address, in that they cannot be assigned to a device. Specifically, the IP 127.0.0.1 is often used to troubleshoot network connectivity issues using the *ping command*. Specifically, it tests a computer's TCP/IP network software driver to ensure it is working properly. *Learn how to use ping 127.0.0.1 to test your computer's TCP/IP network stack*.
    - **Globally Routable?**: No (host-local only)
- `169.254.0.0/16`
    - **Name**: Link-local (APIPA)
    - **Purpose**: Automatic Private IP Addressing (APIPA) is a feature with Microsoft Windows-based computers to automatically assign itself an IP address within this range when a Dynamic Host Configuration Protocol (DHCP) server is not available on the network. A DHCP server is a network device that is responsible for assigning IP addresses to devices on the network.
    - **Globally Routable?**: No (link-local only)
- `224.0.0.0/4`
    - **Name**: Multicast
    - **Purpose**: Group addressing. `224.0.0.0/24` is local-subnet control; `239.0.0.0/8` is admin-scoped. Not unicast.
    - **Globally Routable?**: No (special multicast scope)
- `240.0.0.0/4`
    - **Name**: Reserved
    - **Purpose**: Reserved for future use; commonly treated as invalid by hosts/routers.
    - **Globally Routable?**: No
- `100.64.0.0/10`
    - **Name**: CGNAT (Shared address space)
    - **Purpose**: Used by ISPs for carrier-grade NAT; not the same as RFC1918 private space.
    - **Globally Routable?**: No (ISP-internal)
- `192.0.2.0/24`, `198.51.100.0/24`, `203.0.113.0/24`
    - **Name**: TEST-NET 1/2/3
    - **Purpose**: Documentation and examples; safe to use in manuals, posts, and labs. Not used on the Internet.
    - **Globally Routable?**: No (documentation-only)
- `198.18.0.0/15`
    - **Name**: Benchmarking
    - **Purpose**: Device and network interconnect testing/benchmarks (non-Internet use).
    - **Globally Routable?**: No (testing-only)

---
# Related
**Fundamental Concepts**
- Classful Addressing
- Unicast, Multicast, Broadcast Communication
- Subnetting (Network Segmentation)
**Advanced**
- Classless Inter-Domain Routing [[CIDR]]
- Variable Length Subnet Masking (VLSM)
- Supernetting for route aggregation
- Efficient IP address allocation strategies

---
# References
https://www.meridianoutpost.com/resources/articles/IP-classes.php
https://www.geeksforgeeks.org/computer-networks/structure-and-types-of-ip-address/
