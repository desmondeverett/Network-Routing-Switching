# Network-Routing-Switching

Deployment documentation and standard operating procedures (SOPs) for the enterprise network architecture, including high availability (STP/HSRP) and secure edge VPN configurations.

## 🛠️ Network Topology & Deployment Roadmap

## ✅ Phase 1: Corporate Core Architecture Provisioning
- **Status:** ✅ Completed
- **Documentation:** View Phase 1 SOP
- **Description:** Multi-department enterprise network deployment implementing VLSM, subinterfaces, Inter-VLAN routing (Router-on-a-Stick), and DHCP relay configurations using 802.1Q Trunking and Access Control Lists (ACLs).

### 📸 Phase 1 Quality Assurance (QA) Validation
*1. Network Topology Design* *2. Inter-VLAN Routing Validation* ## ✅ Phase 2: High Availability & Redundancy Implementation
- **Status:** ✅ Completed
- **Documentation:** View Phase 2 SOP
- **Description:** Eliminating single points of failure by engineering backup paths and optimizing layer 2 loop prevention using EtherChannel (LACP), Rapid Spanning Tree Protocol (RSTP), and Hot Standby Router Protocol (HSRP).

### 📸 Phase 2 Quality Assurance (QA) Validation
*1. LACP EtherChannel Validation* *2. Control Plane Failover Validation* ## ✅ Phase 3: Secure Edge & Remote Access Provisioning
- **Status:** ✅ Completed
- **Documentation:** View Phase 3 SOP
- **Description:** Securing the network perimeter and establishing encrypted communication channels for remote sites utilizing Static/Dynamic NAT, Port Address Translation (PAT), and IPsec Site-to-Site VPNs.

### 📸 Phase 3 Quality Assurance (QA) Validation
*1. NAT/PAT Translation Table* *2. IPsec VPN Tunnel Status* ## 📁 Repository Directory Structure
- **/SOPs** — Step-by-step deployment documentation, configuration guides, and validation walkthroughs.
- **/Topologies** — Architecture design files and network maps.
- **/Configurations** — Device running-configurations (Cisco IOS) mapped to each deployment phase.
- **/Validation-Evidence** — Visual proof of successful command outputs and topology integrations.
