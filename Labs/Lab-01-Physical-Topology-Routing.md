# Lab 1: Corporate Core Architecture (Routing & Switching)

## Installation & Configuration Steps

## Phase 1: Physical Topology Design
1. Launch Cisco Packet Tracer and deploy the hardware inventory: 1 Core Router, 2 Managed Layer 2 Switches, and 4 End-User Workstations.
2. Establish the physical infrastructure connections using straight-through copper cabling for all host-to-switch links.
3. Configure Gigabit Ethernet copper trunk links for switch-to-switch and switch-to-router connections to support backbone data frames.
4. Segment the topology logically into separate, distinct subnets to isolate department broadcast domains and maximize address space efficiency.


---

## Phase 2: Switch Layer 2 Architecture & Trunking
1. Access the CLI of both Access Switches and create the required VLAN database entries for each department.
2. Assign the designated interface ranges to their respective access VLAN ports to drop the workstations into their isolated domains.
3. Configure the interconnecting uplink interfaces as IEEE 802.1Q Trunks to pass multi-VLAN tagged traffic up the fabric.
4. Verify the active mappings using the `show vlan brief` command to confirm no ports are misallocated.


---

## Phase 3: Router Inter-VLAN Configuration & Verification
1. Access the Core Router CLI and enable the primary physical interface facing the switch fabric using the `no shutdown` command.
2. Initialize sub-interfaces for each corporate VLAN using the `interface gigabitEthernet 0/0.X` naming convention.
3. Provision the appropriate 802.1Q encapsulation tags (`encapsulation dot1Q X`) before applying the default gateway IP addresses.
4. Open a command prompt on an end-user workstation in one VLAN and execute a cross-subnet ICMP ping to a host in a completely separate VLAN to verify active routing.

---

## Outcome
The physical network design and Inter-VLAN routing matrix were successfully deployed and verified. The logical sub-interfaces on the core router successfully translate and route packets across separate broadcast domains. This setup allows secure, predictable communication between isolated corporate subnets without data leaks or broadcast storms.

## Lessons Learned
* **Encapsulation Command Order:** Confirmed that the encapsulation type and VLAN ID must be explicitly declared via `encapsulation dot1Q <vlan-id>` before the Cisco IOS will accept an IP address configuration on a sub-interface.
* **Trunk Port Consistency:** Emphasized the importance of configuring matching trunking modes on both ends of the switch uplinks to prevent spanning-tree protocol blocking or native VLAN mismatches.

---

## Screenshots

### 1. Converged Network Topology Diagram
![Network Topology](../Screenshots/physical-topology.png)

### 2. Switch VLAN Configuration Verification
![VLAN Verification](../Screenshots/vlan-verification.png)

### 3. Switch Port Assignment Details
![VLAN Port Assignment](../Screenshots/vlan-port-assignment.png)

### 4. Router Sub-Interface Status
![Router Interfaces](../Screenshots/router-interfaces.png)

### 5. Inter-VLAN Routing Verification (Successful Cross-Subnet Ping)
![Ping Success Verification](../Screenshots/inter-vlan-ping-success.png)
