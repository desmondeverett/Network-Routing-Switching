# 🌐 Enterprise Network Routing & Switching Engineering Laboratory

Welcome to my network engineering sandbox. This repository serves as an open-source, hands-on instructional guide and implementation portfolio for designing, configuring, and verifying multi-department enterprise topologies using Cisco IOS configurations.

Whether you are a recruiter auditing my infrastructure skills or a student looking to replicate these environments step-by-step, this documentation provides full visibility into corporate network baselines.

---

## 🏗️ Core Laboratory Architecture
* **Emulation Environment:** Cisco Packet Tracer
* **Core Routing Architecture:** Router-on-a-Stick (RoaS) sub-interface design
* **Switching Fabric:** IEEE 802.1Q Trunking and Virtual Local Area Networks (VLANs)

---

## 🧭 Laboratory Index & Execution Milestones

### 🟢 [Lab 1: Corporate Core Architecture (Routing & Switching)](./Labs/Lab-01-Physical-Topology-Routing.md)
* **The Blueprint:** Segmenting broadcast domains and engineering logical Inter-VLAN routing gateways.
* **Key Skills Demonstrated:** 1. Constructing physical topologies using correct media types (straight-through/crossover).
  2. Isolating department traffic via Layer 2 VLAN database creation.
  3. Organizing multi-VLAN trunk links (`switchport mode trunk`).
  4. Building logical sub-interfaces on the Core Router to act as default gateways.
  5. Verifying cross-subnet communication using end-host ICMP pings.

### 🔵 Lab 2: Infrastructure Redundancy & High Availability *(Under Construction)*
* **The Blueprint:** Optimizing spanning-tree topologies and bundling link aggregation channels.
* **Key Skills Targeted:** LACP EtherChannel grouping, Rapid Spanning Tree Protocol (RSTP) priority tuning, and Hot Standby Router Protocol (HSRP) first-hop gateway redundancy.

### 🔵 Lab 3: Secure Enterprise Edge & Remote Access *(Under Construction)*
* **The Blueprint:** Implementing perimeter access filtering and address translation blocks.
* **Key Skills Targeted:** Standard/Extended Access Control Lists (ACLs), Dynamic NAT/PAT overload pools, and secure remote terminal configurations.

---

## 🛠️ How to Use This Repository
1. **Browse the Code:** Navigate to the `/Labs` directory to examine the underlying structural concepts.
2. **Follow the Steps:** Click on the active **Lab 1** hyperlink above to jump directly into the step-by-step instructional configuration guide, complete with command breakdowns and live verification screenshots.
