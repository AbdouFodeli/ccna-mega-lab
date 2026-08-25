

## IP Addressing Plan

### Subnets & VLAN Allocation 

| Subnet / Network | Subnet Mask | Prefix | VLAN ID | Role / Description | VIP (HSRP) | Active Gateway (Primary) | Standby Gateway (Backup) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **10.0.0.0** | `255.255.255.240` | `/28` | VLAN 99 | Office A Management | `10.0.0.1` | `10.0.0.2` (DSW-A1) | `10.0.0.3` (DSW-A2) |
| **10.1.0.0** | `255.255.255.0` | `/24` | VLAN 10 | Office A PCs | `10.1.0.1` | `10.1.0.2` (DSW-A1) | `10.1.0.3` (DSW-A2) |
| **10.2.0.0** | `255.255.255.0` | `/24` | VLAN 20 | Office A Phones | `10.2.0.1` | `10.2.0.3` (DSW-A2) | `10.2.0.2` (DSW-A1) |
| **10.6.0.0** | `255.255.255.0` | `/24` | VLAN 40 | Office A Wi-Fi | `10.6.0.1` | `10.6.0.3` (DSW-A2) | `10.6.0.2` (DSW-A1) |
| **10.0.0.16** | `255.255.255.240` | `/28` | VLAN 99 | Office B Management | `10.0.0.17` | `10.0.0.18` (DSW-B1) | `10.0.0.19` (DSW-B2) |
| **10.3.0.0** | `255.255.255.0` | `/24` | VLAN 10 | Office B PCs | `10.3.0.1` | `10.3.0.2` (DSW-B1) | `10.3.0.3` (DSW-B2) |
| **10.4.0.0** | `255.255.255.0` | `/24` | VLAN 20 | Office B Phones | `10.4.0.1` | `10.4.0.3` (DSW-B2) | `10.4.0.2` (DSW-B1) |
| **10.5.0.0** | `255.255.255.0` | `/24` | VLAN 30 | Office B Servers | `10.5.0.1` | `10.5.0.3` (DSW-B2) | `10.5.0.2` (DSW-B1) |

---

### Point-to-Point Links & Infrastructure Subnets

| Subnet / Mask | Prefix | Device A (Interface) | IP Address (A) | Device B (Interface) | IP Address (B) | Dynamic Routing |
| --- | --- | --- | --- | --- | --- | --- |
| **10.0.0.32/30** | `/30` | R1 (`G0/0`) | `10.0.0.33` | CSW1 (`G1/0/1`) | `10.0.0.34` | OSPF Area 0 |
| **10.0.0.36/30** | `/30` | R1 (`G0/1`) | `10.0.0.37` | CSW2 (`G1/0/1`) | `10.0.0.38` | OSPF Area 0 |
| **10.0.0.40/30** | `/30` | CSW1 (`PortChannel1`) | `10.0.0.41` | CSW2 (`PortChannel1`) | `10.0.0.42` | OSPF Area 0 (PAgP L3) |
| **10.0.0.44/30** | `/30` | CSW1 (`G1/1/1`) | `10.0.0.45` | DSW-A1 (`G1/1/1`) | `10.0.0.46` | OSPF Area 0 |
| **10.0.0.48/30** | `/30` | CSW1 (`G1/1/2`) | `10.0.0.49` | DSW-A2 (`G1/1/1`) | `10.0.0.50` | OSPF Area 0 |
| **10.0.0.52/30** | `/30` | CSW1 (`G1/1/3`) | `10.0.0.53` | DSW-B1 (`G1/1/1`) | `10.0.0.54` | OSPF Area 0 |
| **10.0.0.56/30** | `/30` | CSW1 (`G1/1/4`) | `10.0.0.57` | DSW-B2 (`G1/1/1`) | `10.0.0.58` | OSPF Area 0 |
| **10.0.0.60/30** | `/30` | CSW2 (`G1/1/1`) | `10.0.0.61` | DSW-A1 (`G1/1/2`) | `10.0.0.62` | OSPF Area 0 |
| **10.0.0.64/30** | `/30` | CSW2 (`G1/1/2`) | `10.0.0.65` | DSW-A2 (`G1/1/2`) | `10.0.0.66` | OSPF Area 0 |
| **10.0.0.68/30** | `/30` | CSW2 (`G1/1/3`) | `10.0.0.69` | DSW-B1 (`G1/1/2`) | `10.0.0.70` | OSPF Area 0 |
| **10.0.0.72/30** | `/30` | CSW2 (`G1/1/4`) | `10.0.0.73` | DSW-B2 (`G1/1/2`) | `10.0.0.74` | OSPF Area 0 |

---

### Loopback Addresses (OSPF Router IDs)

| Device Name | Interface | IP Address | Mask | Purpose |
| --- | --- | --- | --- | --- |
| **R1** | `Loopback0` | `10.0.0.76` | `/32` | OSPF RID / DHCP Relay Target / NTP Server |
| **CSW1** | `Loopback0` | `10.0.0.77` | `/32` | OSPF RID |
| **CSW2** | `Loopback0` | `10.0.0.78` | `/32` | OSPF RID |
| **DSW-A1** | `Loopback0` | `10.0.0.79` | `/32` | OSPF RID |
| **DSW-A2** | `Loopback0` | `10.0.0.80` | `/32` | OSPF RID |
| **DSW-B1** | `Loopback0` | `10.0.0.81` | `/32` | OSPF RID |
| **DSW-B2** | `Loopback0` | `10.0.0.82` | `/32` | OSPF RID |

---

### End Hosts, Infrastructure & Access Switch Management

| Device | Interface / VLAN | IP Address | Subnet Mask | Default Gateway | Function / Role |
| --- | --- | --- | --- | --- | --- |
| **SRV1** | Static Port | `10.5.0.4` | `255.255.255.0` | `10.5.0.1` | DNS, Syslog, FTP Server |
| **WLC1** | Port 1 (VLAN 40) | `10.6.0.4` | `255.255.255.0` | `10.6.0.1` | Wireless LAN Controller Management |
| **ASW-A1** | `VLAN 99` | `10.0.0.4` | `255.255.255.240` | `10.0.0.1` | Access Switch Management |
| **ASW-A2** | `VLAN 99` | `10.0.0.5` | `255.255.255.240` | `10.0.0.1` | Access Switch Management |
| **ASW-A3** | `VLAN 99` | `10.0.0.6` | `255.255.255.240` | `10.0.0.1` | Access Switch Management |
| **ASW-B1** | `VLAN 99` | `10.0.0.20` | `255.255.255.240` | `10.0.0.17` | Access Switch Management |
| **ASW-B2** | `VLAN 99` | `10.0.0.21` | `255.255.255.240` | `10.0.0.17` | Access Switch Management |
| **ASW-B3** | `VLAN 99` | `10.0.0.22` | `255.255.255.240` | `10.0.0.17` | Access Switch Management |

---

### WAN, Dynamic PAT & IPv6 Addressing Scheme

| Link / Service | Address / Prefix | Type / Protocol | Notes |
| --- | --- | --- | --- |
| **R1 ISP Link 1** | `G0/0/0` | Dynamic (DHCP Client) | Primary Default Static Route |
| **R1 ISP Link 2** | `G0/1/0` | Dynamic (DHCP Client) | Floating Default Static Route (AD +1) |
| **Static NAT Target** | `203.0.113.113` | Static NAT | Maps to SRV1 (`10.5.0.4`) |
| **Dynamic PAT Pool** | `203.0.113.200 - 203.0.113.207 /29` | Dynamic PAT (`POOL1`) | Internal subnets to WAN |
| **R1 WAN 1 IPv6** | `2001:db8:a::2/64` | Static IPv6 | Next Hop: `2001:db8:a::1` |
| **R1 WAN 2 IPv6** | `2001:db8:b::2/64` | Static IPv6 | Next Hop: `2001:db8:b::1` (Floating) |
| **R1 <-> CSW1 Link** | `2001:db8:a1::/64` | EUI-64 Dynamic Host ID | Interface `G0/0` & `G1/0/1` |
| **R1 <-> CSW2 Link** | `2001:db8:a2::/64` | EUI-64 Dynamic Host ID | Interface `G0/1` & `G1/0/1` |
