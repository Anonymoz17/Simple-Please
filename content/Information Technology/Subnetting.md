---

  - publish/done
---
**Subnetting** is the practice of dividing a larger network into smaller, logical sub-networks (subnets). 

This is done to improve organization, security, and efficiency. It is also the reason why IP addresses are split into two portions:

- a **network portion**, which identifies the subnet
- a **host portion**, which identifies the individual device within it. 

**Subnet masks** and **[[CIDR]] notations** are then used to define and express where that boundary lies.

---
# Why we need Subnetting (detailed example)

> [!example]+
> When a device wants to communicate with another device, it broadcasts to only its immediate network level from its gateway. When the target device is not found in that immediate network, the network's gateway device, usually a router, intelligently routes the data across other networks. The responses are also routed back in to its origin device in a similar fashion. This is all done with the help of **subnetting**.
> >[!info]-
> >>*When the target device is not found in that immediate network, the network's gateway device, usually a router, intelligently routes the data across other networks*
> >
> >In reality, subnet masks and [[CIDR]] notation already helps the gateway device determine if the destination device is already in its network or not.
> 
> Without subnetting, there will be no network distinctions and all devices will be broadcasting their request and responses to all other devices. This would cause chaos and unnecessary overload, not to mention, its lack of security and organization.

#review %% This is mostly about efficiency and somewhat about organization. Maybe could expand a bit further on organization and security %%

---
# Subnet Mask
A **subnet mask** is a 32-bit number used in IPv4 networking that helps divide an IP address into two components: the **network** portion and the **host** portion.

> [!info] Recap: IP Address Representation
IP addresses are usually represented in dot-decimal notation.
![[IPv4 Address Drawing|700]]

Let's take an example IP Address of `192.168.1.10`
![[Example for Subnet Mask Drawing|700]]
In the binary numbering for the subnet mask, the bits that are **1s are reserved for the network**. **The 0s are available for hosts**.

Thus, the mask in the example tells us that 
- the first 24 bits (first 3 octets) are reserved for the network: `192.168.1`.
- the last 8 bits (last octet) is available for hosts: `10`

> [!note]+ Subnet masks are often represented in [[CIDR]] notation.
> Example: `/24`, which means 24 bits are reserved for the network (same as `255.255.255.0`).

reference: https://www.portnox.com/cybersecurity-101/networking/what-is-a-subnet-mask/

---
# 7 Attributes of Subnetting

| Attributes              | Description                                                                        |
| :---------------------- | :--------------------------------------------------------------------------------- |
| **Network ID**          | First IP address in each Sub-Netwo                                                 |
| **Broadcast IP**        | Last IP address in each Sub-Netw                                                   |
| **First Host IP**       | IP address *after* the Networ                                                      |
| **Last Host IP**        | IP address *before* the Broadca                                          IP        |
| **Next Network**        | IP address *after* the Broadcast IP /<br>the Network ID of the next Sub-Network IP |
| **No. of IP Addresses** | Number of IP addresses in a Sub-Network                                            |
| **CIDR / Subnet Mask**  | Converting between CIDR and Subnet Mask                                            |

---
# How to Calculate a Subnet Mask
## Subnetting **Cheat Sheet**

First, Draw a Subnetting Cheat Sheet. 3 Main Steps:
1. **First Row**: Start with *1*, double until you reach *128*. (*right to left*)
2. **Second Row**: Subtract top row from *256*.
3. **Third to Sixth Row**: From /32, list CIDR notation. (*right to left*)

|    ==Group Size==    | 128 | 64  | 32  | 16  |  8  |  4  |  2  |  1  |
| :------------------: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
|      ==Subnet==      | 128 | 192 | 224 | 240 | 248 | 252 | 254 | 255 |
| ==CIDR (4th Octet)== | /25 | /26 | /27 | /28 | /29 | /30 | /31 | /32 |
| ==CIDR (3rd Octet)== | /17 | /18 | /19 | /20 | /21 | /22 | /23 | /24 |
| ==CIDR (2nd Octet)== | /9  | /10 | /11 | /12 | /13 | /14 | /15 | /16 |
| ==CIDR (1st Octet)== | /1  | /2  | /3  | /4  | /5  | /6  | /7  | /8  |

ref: *[Drawing the Cheat Sheet - Subnetting Mastery - Part 2 of 7](https://youtu.be/ljS07YTEJ2I)*

## Solve Subnetting Using Cheat Sheet
Using the cheat sheet, we'll use it to solve for all 7 attributes of subnetting.

**Example**: Given an address and its CIDR notation: `10.50.111.222 / 12`.

The following drawing shows how to solve subnetting with the cheat sheet in detail, or can check the original reference below it.
![[Solving Subnetting with Cheat Sheet Drawing]]

ref: [How to solve ANY Subnetting Problems in 60 seconds or less - Subnetting Mastery - Part 3 of 7](https://youtu.be/5-wlfAdcmFQ)

## Practice


---
# Important Notes
- ==You will need to know how to convert between a CIDR notation and a Subnet Mask.==

---
# Related


---
# References
- https://www.freecodecamp.org/news/subnet-cheat-sheet-24-subnet-mask-30-26-27-29-and-other-ip-address-cidr-network-references/
- https://youtu.be/BWZ-MHIhqjM - Very good 7 part series explanation on IPv4 subnetting

---
https://www.cisco.com/c/en/us/support/docs/ip/routing-information-protocol-rip/13788-3.html- Explains configuring router and subnetting.