# Multicast Addresses

Multicast addressing is supported by both IPv4 and IPv6. Unlike unicast addressing, which identifies a single host interface, multicast addresses identify a **group of host interfaces**. These groups can span various scopes, from a single computer to the entire Internet.

---

## 1. Multicast Addressing Overview

- **Multicast Address (Group Address):** Identifies a group of hosts.
- **Group Scope:** Defines the portion of the network covered by the group.
- **Common Scopes:**
  - Node-local (same computer)
  - Link-local (same subnet)
  - Site-local (within a site)
  - Global (entire Internet)
  - Administrative (manually configured boundaries)

> Administrative scoped addresses restrict multicast traffic within configured routers and are only available for multicast addressing.

- Hosts can **join or leave multicast groups** dynamically.
- When sending to a multicast group, the source uses its unicast IP and the destination is the multicast address.
- The sender is generally unaware of how many or which hosts receive the datagram.

---

## 2. Multicast Service Models

### 2.1 Any-Source Multicast (ASM)
- Any sender may send to any group.
- Receivers join by specifying only the group address.

### 2.2 Source-Specific Multicast (SSM)
- Uses a single sender per group.
- Receivers join by specifying both the group address and the source IP.
- Developed to simplify deployment complexities of ASM.
- Increasingly favored for adoption on the Internet.

---

## 3. IPv4 Multicast Addresses

### 3.1 Address Range
- IPv4 multicast addresses are in **Class D**: 224.0.0.0 to 239.255.255.255.
- 28 bits available → \(2^{28} = 268,435,456\) possible multicast groups.

### 3.2 Major Sections of IPv4 Class D Address Space

| Range (Inclusive)       | Special Use                   |
|------------------------|--------------------------------|
| 224.0.0.0–224.0.0.255  | Local network control; not forwarded |
| 224.0.1.0–224.0.1.255  | Internetwork control; forwarded normally |
| 224.0.2.0–224.0.255.255| Ad hoc block I                 |
| 224.1.0.0–224.1.255.255| Reserved                      |
| 224.2.0.0–224.2.255.255| SDP/SAP (Session Directory, SAP) |
| 224.3.0.0–224.4.255.255| Ad hoc block II               |
| 224.5.0.0–224.255.255.255| Reserved                    |
| 225.0.0.0–231.255.255.255| Reserved                    |
| 232.0.0.0–232.255.255.255| Source-specific multicast (SSM) |
| 233.0.0.0–233.251.255.255| GLOP (AS-number based)       |
| 233.252.0.0–233.255.255.255| Ad hoc block III            |
| 234.0.0.0–234.255.255.255| Unicast-prefix-based multicast (UBM) |
| 235.0.0.0–238.255.255.255| Reserved                    |
| 239.0.0.0–239.255.255.255| Administrative scope         |

### 3.3 Special Notes on IPv4 Multicast Blocks

- **Local Network Control Block (224.0.0.0/24):** Used for local subnet control, not forwarded by routers. Example: All Hosts group (224.0.0.1).
- **Internetwork Control Block (224.0.1.0/24):** Routed beyond local subnet. Example: NTP multicast group (224.0.1.1).
- **SDP/SAP Block:** Used for session announcements.
- **SSM Block (232.0.0.0/8):** For source-specific multicast.
- **GLOP Addressing (233.0.0.0/16):** Uses 16-bit AS number embedded in multicast address.
- **Unicast-Prefix-Based Multicast (UBM) (234.0.0.0/8):** Associates multicast addresses with IPv4 unicast prefixes, allowing easier allocation and ownership mapping.

#### Example of UBM Address:
- Unicast prefix: 192.0.2.0/24
- Corresponding UBM multicast address: 234.192.0.2

---

## 4. IPv6 Multicast Addresses

### 4.1 Address Range and Format
- IPv6 multicast addresses use prefix **ff00::/8**.
- 112 bits available for group ID → \(2^{112}\) groups possible.
- Format includes:
  - 4-bit Flags (0, R, P, T)
  - 4-bit Scope field (defines multicast scope)
  - 112-bit Group ID

### 4.2 IPv6 Scope Field Values

| Hex Value | Scope               |
|-----------|---------------------|
| 0         | Reserved            |                            
| 1         | Interface-/machine-local |                        
| 2         | Link-/subnet-local  |                            
| 3         | Reserved            |                            
| 4         | Admin               |                            
| 5         | Site-local          |                            
| 6–7       | Unassigned          |                            
| 8         | Organizational-local|                            
| 9–d       | Unassigned          |                            
| e         | Global              |                            
| f         | Reserved            |                            

### 4.3 Special IPv6 Multicast Addresses by Scope

| Address       | Scope        | Special Use                   |
|---------------|--------------|-------------------------------|
| ff01::1       | Node-local   | All nodes                     |
| ff01::2       | Node-local   | All routers                   |
| ff02::1       | Link-local   | All nodes                     |
| ff02::2       | Link-local   | All routers                   |
| ff02::4       | Link-local   | DVMRP routers                 | 
| ff02::5       | Link-local   | OSPF routers                  | 
| ff02::6       | Link-local   | OSPF designated routers       |
| ff02::9       | Link-local   | RIPng routers                 |
| ff02::a       | Link-local   | EIGRP routers                 |
| ff02::d       | Link-local   | PIM routers                   |
| ff02::16      | Link-local   | MLDv2-capable routers         |
| ff02::fb      | Link-local   | mDNSv6                        |
| ff05::2       | Site-local   | All routers                   |
| ff05::fb      | Site-local   | mDNSv6                        |
| ff0x::        | Variable     | Reserved                      |
| ff3x::/32     | Variable     | SSM block                     |

### 4.4 Unicast-Prefix-Based Multicast in IPv6
- Allows multicast addresses to be formed using a unicast prefix.
- Useful for local multicast without complex coordination.
- Example: A host with IID `02-11-22-33-44-55-66-77` can form multicast addresses like `ff3x:0011:0211:2233:4455:6677:gggg:gggg` where `x` is scope and `gggg:gggg` is group ID.

### 4.5 Rendezvous Point (RP) Embedding
- IPv6 multicast addresses can embed the unicast address of an RP.
- RP helps coordinate multicast senders and receivers across subnets.
- RP address is derived from parts of the multicast address (prefix, RIID, prefix length).
- Example: Multicast address `ff75:940:2001:db8:dead:beef:f00d:face` corresponds to RP `2001:db8:dead:beef::9`.

---

## 5. Notes

- Multicast routing and deployment are complex; many protocols exist (e.g., PIM-SM).
- IPv6 uses multicast more aggressively than IPv4.
- Administrative scoped multicast addresses act like private multicast addresses.
- The large multicast address spaces allow for extensive grouping and scoped communication.

---
