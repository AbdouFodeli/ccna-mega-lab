# CCNA Mega Lab

A large-scale networking lab based on Jeremy’s IT Lab CCNA Mega Lab, covering routing, switching, network services, security, and troubleshooting using Cisco Packet Tracer.

## Project Overview

The lab combines multiple networking technologies into a single enterprise-style topology connecting two sites, **Office A** and **Office B**. The network includes a redundant Layer 3 core, distribution and access layers, an edge router, and dual WAN connections.

The goal of the lab was to bring together the concepts covered throughout the CCNA course and practice configuring, verifying, and troubleshooting them in an integrated network environment.

## Network Topology

![Network Topology](docs/network-topology.png)

## Key Technical Features

* **Layer 2:** VLANs, trunking, VTPv2, L2 EtherChannel (PAgP/LACP), Rapid PVST+, root bridge configuration, PortFast, and BPDU Guard.
* **Layer 3 & Redundancy:** Layer 3 EtherChannel, HSRPv2, OSPFv2, DR/BDR configuration, IPv6 static routing, and EUI-64.
* **Network Services:** DHCP, DHCP relay, Dynamic PAT, Static NAT, NTP, Syslog, SNMPv2c, and SSHv2.
* **Security:** DHCP Snooping, Dynamic ARP Inspection (DAI), Port Security, and standard/extended ACLs.
* **Wireless:** Cisco WLC configuration, WPA2 authentication, dynamic VLAN assignment, and AP association.

## Key Implementation Requirements

* **Hierarchical Network Design:** Full 3-tier enterprise architecture (Access, Distribution, and Core layers) serving two physical office locations (Office A & Office B).
* **VLAN & Trunking Infrastructure:**

  * Configured VLANs for Data, Voice, and Management traffic across all access switches.
  * Implemented 802.1Q trunking with non-default native VLANs (`VLAN 1000`) for security.
  * Configured LACP/EtherChannel between Distribution switches for link aggregation.
* **First Hop Redundancy (FHRP):** Deployed **HSRPv2** across Distribution switches (`DSW-A1/A2` & `DSW-B1/B2`) to provide active/standby gateway redundancy for end hosts.
* **Spanning Tree Protocol:** Tuned **Rapid-PVST+** bridge priorities to align STP root bridges with HSRP primary gateways.
* **Dynamic Routing:** Configured **OSPFv2** (Area 0) across all Core, Distribution, and Edge devices with point-to-point network types and passive interfaces where appropriate.
* **Layer 2 Security & Hardening:**

  * Enabled **Port Security** (sticky MAC addresses and violation actions) on access interfaces.
  * Implemented **DHCP Snooping** and **Dynamic ARP Inspection (DAI)** to mitigate spoofing and rogue server attacks.
  * Configured **LLDP** explicitly while selectively disabling transmit/CDP on untrusted access ports.
* **Services & Edge Security:**

  * Configured `R1` as the central **DHCP Server** (using helper addresses on SVIs) and **NTP Master**.
  * Implemented **PAT (NAT Overload)** on `R1` for Internet egress.
  * Applied **Extended Access Control Lists (ACLs)** to control inter-VLAN communication between Office A and Office B.
  * Secured management planes using **SSH v2**, local authentication, line timeouts, and SNMP v2.

## Troubleshooting Example

During the lab, an HSRP issue occurred because the two distribution switches were running different HSRP versions.

One distribution switch was configured for HSRP version 1 while the other was configured for HSRP version 2. This resulted in HSRP-related errors and prevented the expected redundancy behavior.

The issue was identified using:

```text
show standby
```

The output revealed the HSRP version mismatch between the two switches. After configuring both switches to use HSRP version 2, the HSRP active/standby relationship was established successfully.

## Documentation & Files

* [IP Addressing Plan](docs/ip-addressing-plan.md) — IPv4/IPv6 addressing, VLAN allocation, HSRP addresses, infrastructure links, and device management addresses.
* [Network Topology](docs/network-topology.png) — High-level topology diagram.
* [Packet Tracer Lab File](lab-files/ccna-mega-lab.pka) — Complete Packet Tracer activity file.
* [Device Configurations](configs/) — Final device configurations organized by network layer.
