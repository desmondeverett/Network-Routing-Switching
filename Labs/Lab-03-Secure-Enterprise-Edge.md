# Lab 3: Secure Enterprise Edge & Remote Access

## 📖 Scenario
With the *Everett Technologies* core architecture and redundancy protocols in place, the company is expanding to a new remote branch office. To allow internal users access to the public internet while securing confidential inter-site traffic, this phase deploys Port Address Translation (PAT) at the perimeter and establishes a secure, encrypted IPsec Site-to-Site VPN tunnel across the public WAN.

## 🎯 Objectives
- Define internal/external routing boundaries for Network Address Translation.
- Deploy Port Address Translation (PAT) using Access Control Lists (ACLs) to allow internet access.
- Configure ISAKMP (Phase 1) policies and pre-shared keys for secure peer authentication.
- Configure IPsec (Phase 2) transform sets and crypto maps to encrypt branch-to-HQ data.
- Verify active NAT translations and successful ISAKMP/IPsec security associations.

## 🛠️ Execution Steps

### Phase 1: Port Address Translation (PAT) Configuration
First, define the inside and outside interfaces on the edge router, then create an ACL to define which internal traffic is allowed to be translated to the public internet.
```text
Router(config)# interface GigabitEthernet0/1
Router(config-if)# ip nat inside
Router(config-if)# exit

Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip nat outside
Router(config-if)# exit

Router(config)# access-list 1 permit 10.0.0.0 0.255.255.255
Router(config)# ip nat inside source list 1 interface GigabitEthernet0/0 overload
```

### Phase 2: VPN Phase 1 (ISAKMP) Configuration
Configure the IKE Phase 1 policy to authenticate the remote branch router using a secure pre-shared key.
```text
Router(config)# crypto isakmp policy 10
Router(config-isakmp)# encryption aes
Router(config-isakmp)# hash sha
Router(config-isakmp)# authentication pre-share
Router(config-isakmp)# group 2
Router(config-isakmp)# exit
Router(config)# crypto isakmp key EverettSec123 address 203.0.113.2
```

### Phase 3: VPN Phase 2 (IPsec) Configuration
Define the interesting traffic (what gets encrypted) using an extended ACL, create the transform set, and bind it all together using a crypto map.
```text
Router(config)# ip access-list extended VPN-TRAFFIC
Router(config-ext-nacl)# permit ip 10.0.10.0 0.0.0.255 10.0.20.0 0.0.0.255
Router(config-ext-nacl)# exit

Router(config)# crypto ipsec transform-set TS esp-aes esp-sha-hmac
Router(config)# crypto map VPNMAP 10 ipsec-isakmp
Router(config-crypto-map)# set peer 203.0.113.2
Router(config-crypto-map)# set transform-set TS
Router(config-crypto-map)# match address VPN-TRAFFIC
```

### Phase 4: Applying Cryptography to the WAN Interface
Attach the completed crypto map to the outside-facing interface to begin actively monitoring for interesting traffic.
```text
Router(config)# interface GigabitEthernet0/0
Router(config-if)# crypto map VPNMAP
```

---

## 🧠 Lessons Learned & Troubleshooting

During the deployment of the secure edge, several classic enterprise routing challenges were encountered and successfully resolved. Documenting these traps is critical for future deployments:

### 1. NAT vs. VPN Order of Operations (NAT Exemption)
- **Concept:** When traffic hits a Cisco router, NAT translation occurs *before* crypto map encryption.
- **Application:** If internal traffic destined for the remote branch matches the standard NAT ACL, the router translates the private IP into the public interface IP. Consequently, the traffic no longer matches the VPN's "interesting traffic" ACL (which looks for original private 10.x.x.x addresses), and the VPN tunnel fails to trigger.
- **Resolution:** A *NAT Exempt* rule was implemented. A `deny` statement is placed at the top of the NAT ACL to explicitly prevent VPN-destined traffic from being translated, allowing it to pass untouched to the crypto engine.

### 2. Physical Interface Naming Conventions
- **Issue:** Applying configurations to `GigabitEthernet0/0` on newer router models (like the Cisco 4331) caused the router to silently reject the VPN configuration blocks because the actual physical interfaces use a 3-number format (e.g., `GigabitEthernet0/0/0`).
- **Resolution:** Verified physical interfaces using `show run` and `show ip int brief`, then completely rewrote and reapplied the NAT and Crypto Map configurations to target the exact hardware interface format.

### 3. Subnet Misalignments on Point-to-Point Links
- **Issue:** A single-digit typo on a /30 point-to-point WAN link (e.g., configuring `192.51.100.1` instead of `198.51.100.1`) caused complete routing failure, resulting in "Destination host unreachable" errors when PCs attempted to ping the ISP.
- **Resolution:** Tracked the packet drop to the local gateway, verified interface IPs using `show ip int brief`, and corrected the IP address on the specific interface to restore connectivity to the target subnet.

### 4. IPsec "On-Demand" Tunnels & Privilege Modes
- **Issue:** Attempting to verify the VPN yielded "Invalid input detected" and "No SAs found" errors.
- **Resolution:** 1. **Privilege Levels:** Realized that advanced cryptography verification commands (`show crypto ipsec sa`) are hidden in User EXEC mode (`Router>`) and must be executed in Privileged EXEC mode (`Router#`).
  2. **Waking the Tunnel:** Cisco IPsec VPNs are "on-demand." They sit dormant until "interesting traffic" triggers them. Sent continuous pings specifically from the internal PC's private IP (not the router's public IP) to force Phase 1 and Phase 2 negotiations to wake up and establish the Security Associations.
---

## 📸 Verification & Screenshots

**1. NAT/PAT Translation Table**
![NAT/PAT Translation Table](../Screenshots/nat-pat-translations.png)

**2. IPsec VPN Tunnel Status**
![IPsec VPN Tunnel Status](../Screenshots/ipsec-vpn-tunnel-status.png)
