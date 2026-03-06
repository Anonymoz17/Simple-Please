---

  - publish/done
---
### ISP Address Allocation

ISPs own pools of public IP ranges and carve them out to clients using CIDR subnetting. Blocks must be contiguous and power-of-2 aligned. A business can be given multiple separate blocks if contiguous space isn't available, though it's not ideal.

### IP Wastage and Fragmentation

CIDR doesn't eliminate wastage. Power-of-2 alignment means businesses always get slightly more than they need. Fragmentation builds over time as returned blocks sit surrounded by active allocations and can't be merged back into larger blocks.

---

### RIR Allocations and IPv4 Exhaustion

RIRs received massive blocks (/8s) from IANA and subdivided them down to ISPs using the same CIDR mechanics. IANA exhausted its free pool in 2011 and RIRs followed shortly after. Now mostly transfers and sales occur, with IPv4 addresses trading for real money (~$40-50 each).

### IPv4 Address Map Is Now Largely Fixed

Since exhaustion, CIDR blocks and their starting addresses are essentially permanent. This is why IP geolocation and WHOIS lookups remain reliable — allocations don't move, only ownership transfers. IPv6 is where active fresh allocation is happening now.