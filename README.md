# Network-Routing-Switching

Enterprise networking portfolio featuring Cisco routing and switching labs, multi-department VLAN architectures, infrastructure redundancy (STP/HSRP), and secure edge VPN configurations.

---

## 🛠️ Network Lab Topology & Roadmap

### 🛑 Lab 1: Corporate Core Architecture (Routing & Switching)
- **Status:** ✅ Complete
- **Objective:** Design a multi-department network implementing VLSM, subinterfaces, Inter-VLAN routing, and DHCP relay configurations.
- **Core Technologies:** VLANs, 802.1Q Trunking, Router-on-a-Stick, Access Control Lists (ACLs).
- **Documentation:** [View Lab 1 Details & Configurations](Labs/Lab-01-Physical-Topology-Routing.md)

#### 📸 Verification Proof
*Network Topology Design:* ![Network Topology](Screenshots/physical-topology.png)

*Inter-VLAN Routing Verification (Successful Cross-Subnet Ping):* ![Ping Success Verification](Screenshots/inter-vlan-ping-success.png)

---

### 🛑 Lab 2: Infrastructure Redundancy & High Availability
- **Status:** ✅ Complete
- **Objective:** Eliminate single points of failure by engineering backup paths and optimizing layer 2 loop prevention.
- **Core Technologies:** EtherChannel (LACP), Rapid Spanning Tree Protocol (RSTP), Hot Standby Router Protocol (HSRP).
- **Documentation:** [View Lab 2 Details & Configurations](Labs/Lab-02-Infrastructure-Redundancy-%26-High-Availability.md)

#### 📸 Verification Proof
*LACP EtherChannel Verification:*
![EtherChannel Summary](Screenshots/01-etherchannel-summary.png)

*Control Plane Failover Verification:*
![Failover Test](Screenshots/03-failover-ping-test.png)

---

### 🛑 Lab 3: Secure Enterprise Edge & Remote Access
- **Status:** 🟦 Coming Soon
- **Objective:** Secure the network perimeter and establish encrypted communication channels for remote sites.
- **Core Technologies:** Static/Dynamic NAT, Port Address Translation (PAT), IPsec Site-to-Site VPN.

---

## 📁 Repository Directory Structure

- `/Labs` — Step-by-step markdown documentation, lessons learned, and verification walkthroughs.
- `/Topologies` — Cisco Packet Tracer (`.pkt`) and architecture design files.
- `/Text Files` — Device running-configurations (Cisco IOS) mapped to each lab.
- `/Screenshots` — Visual proof of successful command outputs and topology designs.
