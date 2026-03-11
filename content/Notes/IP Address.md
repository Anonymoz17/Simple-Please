---
aliases:
  - Internet Protocol

  - publish/done
---
#computer-networking 
# Summary
IP addresses are unique identifiers assigned to every device connected to the internet. Computers that communicate over the internet or via local networks share information to a specific location using IP addresses. They serve **2 main functions**:
1. Host Identification
2. Location Addressing

An IP address mainly consists of 2 parts. #review %% write about this in this note %%
1. Network Address
2. Host Host Address

There are different types of IP address based on their scope, persistence, allocation, and usage. IP addresses have **4 properties**:
1. **Scope/Visibility**
	1. Public
	2. Private
2. **Assignment Persistence**
	1. Static
	2. Dynamic
3. **Allocation Model**
	1. Dedicated
	2. Shared
4. **Addressing Pattern**
	1. Unicast
	2. Multicast
	3. Broadcast
	4. Anycast

IP addresses have 2 distinct [[IP Address#IP Address Versions|versions]]:
- [[IPv4]]
- [[IPv6]]

---
# About
IP stands for Internet Protocol. It is a set of rules that facilitate data communications between networks. Each internet-connected network or device within a network needs an Internet Protocol address to send and receive data. An IP address works in helping your device, whatever you are accessing the internet on, to find whatever data or content is located to allow for retrieval. 

IP addresses are allocated by the [Internet Assigned Numbers Authority](https://www.ipxo.com/blog/what-is-iana/) (IANA), a subsidiary of the [Internet Corporation for Assigned Names and Numbers](https://www.ipxo.com/blog/what-is-icann/) (ICANN), a nonprofit organization based in the US.

---
# What IP Addresses Do
An IP address serves two main functions:
1. **Host Identification:** Host identification means that an IP address can uniquely identify a specific device (or host) on a network.
2. **Location Addressing:** Location addressing means that an IP address can specify the logical or physical location of a device on a network.

---
# IP Addresses Consist of 2 Parts
1. **Network Address**
2. **Host Address**

*Example*:
IP Address: `192.168.1.32`
Here, the first 3 octets are the Network portion of the address and the last octet is the Host portion of the address. Dive deeper into [[Subnetting|subnetting]] about this topic.
> [!warning] This part is only for IPv4 example.

#review %% add IPv6 also %% 

---
# How are IP Addresses Generated?
IP addresses are generated with the help of a specific system in order to ensure the unique identification of devices on the Internet. The process begins with The **Internet Assigned Numbers Authority (IANA)**. It is responsible for creating and allocating a range of IP addresses to **RIRs (Regional Internet Registries)**. RIRs manage the IP addresses for specific regions. Then RIRs allocated IP addresses to **ISPs (Internet Service Providers)** then finally the ISPs assign the IP addresses to the **End Users**.

The general Hierarchy of the IP address assignment looks like this:
- IANA
	- RIR
		- ISP
			- End Users

When a device connects to the Internet, the ISP’s DHCP or Dynamic Host Configuration Protocol server assigns an available IP address from its pool.

*Dive deeper into [[IP Address Allocation]]*

---
# How do IP Addresses Work?

An IP address is a unique identifier assigned to every single device that is connected to the Internet. With the help of IP addresses, it is now possible to send as well as receive data over the Internet which in return allows devices to communicate with one another worldwide.

The process begins when a device sends a request to access a website or a server. When a request is sent, the IP address is used in order to identify the destination device, and data is **routed** through the internet backbone (a network of high-speed connections) to reach the intended device. Once the data reaches the destination, the IP address ensures it is delivered to the correct device, allowing the requested data to be displayed on the user’s screen.

---
# IP Address Versions and Representations
There are 2 versions of IP addresses. IPv4 is most commonly used.
1. [[IPv4]]
![[IPv4 Address Drawing|700]]
2. [[IPv6]]

[[Why is IPv6 adoption slow?]]

---
# Properties of IP Addresses
## 1. Scope/Visibility

### 1. Public 
**Alias**: Primary or External Address.

A public IP's primary purpose is to connect to the internet. A public IP address, or external-facing IP address, applies to the main device people use to connect their business or home internet network to their internet service provider (ISP). Most of the time, this device is the router. The ISP then assigns a public IP address to the router which then shares that connection with the devices in the private network. 

All devices in the private network that connect to the router communicate with other IP addresses using the router’s IP address. Thus, when browsing the internet, it is the public IP address that is visible to others.

### 2. Private
**Alias**: Secondary or Internal addresses

A private IP address, or internal-facing IP address, is assigned by an office or home [[intranet]] (or local area network) to devices, or by the internet service provider (ISP). The home/office router manages the private IP addresses to the devices that connect to it from within that local network. Network devices are thus mapped from their private IP addresses to public IP addresses by the router using **[[NAT]]** (Network Address Translation).

> [!info]+ How IP Addresses are Assigned for Devices in Private Networks
> **Routers** assign each private IP within the LAN (Local Area Network) using DHCP (Dynamic Host Configuration Protocol). The ranges themselves were designated by the Internet Assigned Numbers Authority (IANA), but the router, not IANA, assigns the actual private IPs to devices. It's possible for two devices on two separate networks to have the same private IP, but no two devices on the same network can share the same private IP.

Private IP addresses are reused across multiple networks, thus preserving valuable IPv4 address space and extending addressability beyond the simple limit of **IPv4** addressing (4,294,967,296).

In the **IPv6** addressing scheme, every possible device has its own unique identifier assigned by the ISP or primary network organization, which has a unique prefix. Private addressing is possible in IPv6, and when it's used it's called Unique Local Addressing (ULA).

#### Private IP Ranges
- **Class A**: *10.0.0.0 to 10.255.255.255* - ISPs & Large Enterprises
- **Class B**: *172.16.0.0 to 172.31.255.255* - Medium to Large Organizations
- **Class C**: *192.168.0.0 to 192.168.255.255* - Small Businesses and Homes

> [!warning]+
> Public IPs could technically be used as Private IPs (this could lead to [[IP Shadowing]] as an attack vector). No strict rules are placed but the **conventions are followed rigorously** by everyone for good reason.

### Difference between Public and Private IPs

|                                      Public                                       |                                       Private                                       |
| :-------------------------------------------------------------------------------: | :---------------------------------------------------------------------------------: |
|                     Used to connect to other devices in a WAN                     |                  Used to connect to other devices on the same LAN                   |
|                         Access across the entire Internet                         |                           Access across the local network                           |
|                     Assigned by an Internet service provider                      |                     Assigned by the network device, e.g. Router                     |
|                      Must be different to avoid IP conflict                       | Same address usable for multiple devices as long as they're not on the same network |
| Address can be any string of numbers outside those set aside for class A, B, or C |        Address limited to certain number sets - class A, class B, or class C        |
![[Pasted image 20260215194900.png|400]]



Public IPs are globally routable. Private IPs (RFC 1918: 10.x, 172.16.x, 192.168.x) are reserved ranges that internet routers are configured to never forward, allowing them to be reused independently by any network worldwide.

Why do we need Public and Private IPs?

---
## 2. Assignment Persistence
### 1. Static
An IP address that a person manually configures and fixes to their device’s network is referred to as a static IP address. A static IP address cannot be changed automatically. An internet service provider may assign a static IP address to a user account. The same IP address will be assigned to that user for every session. #review %% what does 'user account' means here? %%
> [!example]+ STATIC IP
> Day 1: You → 198.51.100.50 
> Day 2: You → 198.51.100.50 ← Same IP 
> Day 3: You → 198.51.100.50

[[How to set your own Static IP?]]
*Is it possible to configure this with ifconfig and, if so, how?*

### 2. Dynamic
A dynamic IP address is automatically assigned to a network when a router is set up. The Dynamic Host Configuration Protocol ([[DHCP]]) assigns the distribution of this dynamic set of IP addresses. The DHCP can be the router that provides IP addresses to networks across a home or an organization.

Each time a user logs into the network, a fresh IP address is assigned from the pool of available (currently unassigned) IP addresses. A user may randomly cycle through several IP addresses across multiple sessions.

> [!example]+ DYNAMIC IP
> Day 1: You → 198.51.100.50 
> Day 2: You → 198.51.100.51 ← Different IP 
> Day 3: You → 198.51.100.52 ← Different IP

---
## 3. Allocation Model
### 1. Dedicated
A dedicated IP address is an IP address that is exclusively assigned to a single website or domain. It means that no other website or domain can use the same IP address. Dedicated IP addresses are usually more expensive and less common than shared ones. They are mainly used for websites that need higher security, performance, or reliability, such as e-commerce sites, online banking sites, or email servers.

>[!important]+ Clarification
>**Dedicated IPs are typically part of an IP range or block allocated by the ISP/hosting provider exclusively for the customer's use.** For example, a business might be allocated 203.0.113.0/29 (8 IPs), and they have exclusive use of all IPs in that range, even if they only actively use one or two of them.

> [!example]+
> ISP/Hosting Provider Allocates Block: 203.0.113.0/29 (8 dedicated IPs: 203.0.113.0 - 203.0.113.7) 
> All **exclusive** for YourCompany.com
> 
> ├─ 203.0.113.1 → YourCompany.com
> ├─ 203.0.113.2 → mail.YourCompany.com
> ├─ 203.0.113.3 → api.YourCompany.com
> ├─ 203.0.113.4 → Reserved for future use 
> ...
> ├─ 203.0.113.7 → Reserved for future use

### 2. Shared
A shared IP address means that multiple users or domains share the same public IP address and it relies on a process called **Network Address Translation** ([[NAT]]). Shared IP addresses depend on the **context**:
1. ISPs
2. VPNs
3. Hosting
#### ISP
ISPs often assign the same IP to multiple users at the same time. ISPs use techniques like carrier-grade network address translation ([[CGNAT]]) to conserve them, similarly to what your router does on a local network level ([[NAT]]). If you're using a shared IP through your ISP, you're essentially sharing it with others on the network. *This is done to preserve the number of IPv4 addresses.*

> [!warning]+
> This can sometimes lead to problems like getting blocked from websites if another user sharing your IP violates a platform's rules.

> [!info]+
> The ISP context also applies to that of the **LAN** where the private IP addresses of the devices are mapped to a single external-facing public IP address of the router.

#### VPN
Virtual private networks ([[VPN]]s) also use shared IPs but for different reasons. When you connect to a VPN server, many users share the same public IP address. This serves **2 purposes**: 
1. Optimizes resource use 
2. Enhances privacy

By blending your activity with that of others, a shared IP makes it harder to trace your online actions back to you specifically.

#### Hosting
A shared IP address is an IP address that is shared by multiple websites or domains. It means that several websites or domains can use the same IP address. Shared IP addresses are usually cheaper and more common than dedicated ones. They are mainly used for websites that do not have high requirements for security, performance, or reliability, such as blogs, forums, or personal sites. This setup is cost-effective and works well for most small to medium websites.

> [!example]+
> Multiple websites/domains map to the **same IP address**: 198.51.100.50
> 1. example.com
> 2. myblog.net
> 3. store.org
> 
> When users request for any of these sites using their domain, the DNS maps them to the same IP address. When the requests arrive to the server with destination IP address of 198.51.100.50, the server reads the **'Host:'** header in the request to determine which content to serve.
> If it was **'Host: example.com'**, the server would check the configuration *'example.com → serve files from /var/www/example/'* and serve the appropriate files back to the user.

*Reference on Shared IP Addresses:*
https://nordvpn.com/blog/shared-ip-address/

### Dedicated vs Shared IPs
#review %% this passage %%
Shared IP Hosting and Virtual Hosting
Multiple domains can share one public IP by differentiating at the application layer via HTTP Host headers. Dedicated IPs are sometimes needed for email reputation, legacy SSL/TLS requirements, or protocols that rely on IP-based identification.

---
## 4. Addressing Pattern
#review %% Understand thoroughly about addressing patterns %%
### 1. Unicast
A unicast IP address is an IP address that is used for one-to-one communication between a sender and a receiver. It means that a packet sent from a source device to a destination device with a unicast IP address will be delivered to that specific device only. Unicast IP addresses are the most common type of IP address on the Internet.
### 2. Multicast
IP Multicast is a way of transmitting IP packets to an interested group of receivers instead of to a single destination or all devices. This is highly efficient since one sender can send data to multiple receivers without replicating the data for each recipient. Multicasting applications include streaming media, video conferencing, and real-time data distribution.
*How are the responses from the receivers handled?*
### 3. Broadcast
A broadcast IP address is an IP address that is used for one-to-all communication between a sender and all the receivers on a network. It means that a packet sent from a source device to a destination device with a broadcast IP address will be delivered to every device on the network regardless of their individual addresses. Broadcast IP addresses are mainly used for network discovery, configuration, or maintenance.
### 4. Anycast
This address is used for a specific group of devices where the data is sent to the closest or most appropriate device within the group. It’s often used for content delivery networks ([[CDN]]s) to ensure users access content from the nearest server.

For example, imagine sending a package with multiple potential delivery points, and the closest one gets the delivery.

---
# Questions


---
# Related
- [[NAT|Network Address Translation]]
- [[Working with IP Addresses Practically]]

---
# References
https://www.fortinet.com/resources/cyberglossary/what-is-ip-address
https://www.pynetlabs.com/types-of-ip-address/

---
# Extra
IP address gives a lot of information.
https://who.is/
https://geoiplookup.io/

