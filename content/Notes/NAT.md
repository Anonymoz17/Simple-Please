---
aliases:
  - Network Address Translation

  - publish/done
---
**NAT** manages connections from multiple users or devices. It ensures that data packets are routed correctly, so each user gets the right response without mixed-up requests.

[[IP Address#2. Shared|Shared IPs]] relies on NAT to work as intended.

#review %% this passage %%
Allows many private IP devices to share one public IP. The router tracks outbound connections by port and maps replies back to the correct internal device. Works alongside CIDR to conserve public address space.

[[CGNAT]] - ISPs do Carrier Grade NAT, giving customers a private address that gets NAT-ted again at the ISP level before hitting the internet. 

> [!important] Fun Fact
> NAT can be nested infinitely in theory. The entire private IP range can be freshly reused at each layer infinitely.
> 
> Practical limits are latency, CPU overhead, and protocol breakage rather than address math.

