# `Link Layer`

![Link Layer 1](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_1.jpg)

```text

wlo1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.2.3  netmask 255.255.255.0  broadcast 192.168.2.255
        inet6 fe80::4dc:61ee:b080:e945  prefixlen 64  scopeid 0x20<link>
        inet6 2001:e280:3e14:116:bb07:9a4d:54a6:bd04  prefixlen 64  scopeid 0x0<global>
        inet6 2001:e280:3e14:116:1e12:478b:cd6a:8c75  prefixlen 64  scopeid 0x0<global>
        RX packets 230414  bytes 290634978 (290.6 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 57077  bytes 12135506 (12.1 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

* MTU is maximum transmission unit that is upperbound in data packet size which can be transferred
  MTU (Maximum Transmission Unit) size of 1500 refers to 1500 bytes

* The choice of 1500 bytes as the MTU is historical and balances efficiency and hardware limitations
  from early Ethernet days. Larger MTUs, called jumbo frames (up to around 9000 bytes) they are present
  but not recommeded to use beacuse of compatibility issues.


![Link Layer 2](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_2.jpg)

![Link Layer 3](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_3.jpg)

## IEEE 802 LAN/MAN  Standards

| Standard | Name | Description |
|----------|------|-------------|
| 802.1ak | Multiple Registration Protocol (MRP) | Protocol for multiple registration services |
| 802.1AE | MAC Security (MACSec) | Media Access Control security protocol |
| 802.1AX | Link Aggregation | Link aggregation protocol (formerly 802.3ad) |
| 802.1d | MAC Bridges | Media Access Control bridge protocol |
| 802.1p | Traffic Classes/Priority/QoS | Quality of Service and traffic prioritization |
| 802.1q | Virtual Bridged LANs | Virtual LAN protocol with corrections to MRP |
| 802.1s | Multiple Spanning Tree Protocol (MSTP) | Enhanced spanning tree protocol |
| 802.1w | Rapid Spanning Tree Protocol (RSTP) | Rapid convergence spanning tree protocol |
| 802.1X | Port-Based Network Access Control (PNAC) | Network access control protocol |
| 802.2 | Logical Link Control (LLC) | Logical link layer control protocol |
| 802.3 | Baseline Ethernet and 10Mb/s Ethernet | Standard Ethernet protocol |
| 802.3u | 100Mb/s Ethernet ("Fast Ethernet") | Fast Ethernet protocol |
| 802.3x | Full-duplex operation and flow control | Full-duplex Ethernet with flow control |
| 802.3z/802.3ab | 1000Mb/s Ethernet ("Gigabit Ethernet") | Gigabit Ethernet protocol |
| 802.3ae | 10Gb/s Ethernet ("Ten-Gigabit Ethernet") | Ten-Gigabit Ethernet protocol |
| 802.3ad | Link Aggregation | Link aggregation protocol |
| 802.3af | Power over Ethernet (PoE) | Power over Ethernet up to 15.4W |
| 802.3ah | Access Ethernet ("Ethernet in the First Mile (EFM)") | First mile Ethernet access |
| 802.3at | Frame format extensions | Frame format extensions up to 2000 bytes |
| 802.3ba | Power over Ethernet enhancements ("PoE+") | Enhanced PoE up to 30W and 40/100Gb/s Ethernet |
| 802.11a | 54Mb/s Wireless LAN at 5GHz | Wireless LAN protocol at 5GHz frequency |
| 802.11b | 11Mb/s Wireless LAN at 2.4GHz | Wireless LAN protocol at 2.4GHz frequency |
| 802.11e | QoS enhancement for 802.11 | Quality of Service enhancements for wireless |
| 802.11g | 54Mb/s Wireless LAN at 2.4GHz | High-speed wireless LAN at 2.4GHz |
| 802.11h | Spectrum/power management extensions | Spectrum and power management for wireless |
| 802.11i | Security enhancements/replaces WEP | Enhanced wireless security protocol |
| 802.11j | 4.9–5.0GHz operation in Japan | Japan-specific wireless frequency operation |
| 802.11n | 6.5–600Mb/s Wireless LAN | High-speed wireless with MIMO and 40MHz channels |
| 802.11s | Mesh networking, congestion control | Wireless mesh networking protocol |
| 802.11y | 54Mb/s wireless LAN at 3.7GHz (licensed) | Licensed wireless LAN at 3.7GHz |
| 802.16 | Broadband Wireless Access Systems (WiMAX) | Broadband wireless access standard |
| 802.16d | Fixed Wireless MAN Standard (WiMAX) | Fixed wireless metropolitan area network |
| 802.16e | Fixed/Mobile Wireless MAN Standard (WiMAX) | Fixed and mobile wireless MAN |
| 802.16h | Improved Coexistence Mechanisms | Enhanced coexistence for wireless systems |
| 802.16j | Multihop Relays in 802.16 | Multihop relay mechanisms for WiMAX |
| 802.16k | Bridging of 802.16 | Bridging mechanisms for WiMAX |
| 802.21 | Media Independent Handovers | Media-independent handover protocols |

## Ethernet Frame Format

* The Ethernet frame format is the standardized structure that defines how data is packaged
  and transmitted over Ethernet networks

![Link Layer 4](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_4.jpg)

## MPE (Manchester Phase Encoding)

![Link Layer 5](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_5.jpg)

![Link Layer 6](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_6.jpg)

## IEEE Packet

![Link Layer 7](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_7.jpg)

---

# 802.1p/q Virtual LANs and QoS Tagging

## Introduction to Virtual LANs (VLANs)

### Background and Problem Statement
With the widespread adoption of switched Ethernet networks, it became possible to interconnect all computers at a site on the same physical Ethernet LAN. While this approach offered several advantages, it also introduced significant challenges:

**Advantages:**
- Direct communication between any hosts using IP and network-layer protocols
- Minimal administrator configuration required
- Efficient broadcast and multicast traffic distribution
- Simplified network topology

**Challenges:**
- **Broadcast Storm Issues**: Broadcast traffic going to every computer can create an undesirable amount of network traffic when many hosts use broadcast
- **Security Concerns**: Complete any-to-any station communication may pose security risks
- **Network Segmentation**: Large, multiuse switched networks lack logical separation

### VLAN Solution
To address some of these problems with running large, multiuse switched networks, IEEE extended the 802 LAN standards with a capability called virtual LANs (VLANs) in a standard known as 802.1q. VLANs provide logical network segmentation within a single physical infrastructure.

**Key VLAN Characteristics:**
- Compliant Ethernet switches isolate traffic among hosts to common VLANs
- Two hosts on the same switch but different VLANs require a router for communication
- Provides broadcast domain separation without physical network changes

```mermaid
graph TD
    A[Traditional Flat Network] --> B[All devices in same broadcast domain]
    B --> C[Security Issues]
    B --> D[Broadcast Storms]
    B --> E[No Logical Separation]
    
    F[VLAN Solution] --> G[Logical Segmentation]
    G --> H[Separate Broadcast Domains]
    G --> I[Enhanced Security]
    G --> J[Traffic Isolation]
    
    K[Same Physical Infrastructure] --> L[Multiple Logical Networks]
    L --> M[VLAN 10: Accounting]
    L --> N[VLAN 20: Engineering]
    L --> O[VLAN 30: Marketing]
```

---

## 802.1Q VLAN Standard

### Frame Structure and Tagging Process
The 802.1Q standard defines how VLAN information is embedded into Ethernet frames through a process called tagging.

**Tagging Process:**
1. The 802.1Q tag is inserted into the frame, situated between the source MAC address and payload
2. A 16-bit field set to a value of 0x8100 in order to identify the frame as an IEEE 802.1Q-tagged frame
3. It works by inserting a VLAN tag into the header of an Ethernet frame and allows switches and other network devices to identify and process the frame through something called a VLAN membership

### Frame Types
802.1Q trunks support two types of frames: tagged and untagged. An untagged frame does not carry any VLAN identification information. A tagged frame carries VLAN identification information.

```mermaid
graph LR
    A[Original Ethernet Frame] --> B[Destination MAC]
    B --> C[Source MAC]
    C --> D[EtherType/Length]
    D --> E[Payload]
    E --> F[FCS]
    
    G[802.1Q Tagged Frame] --> H[Destination MAC]
    H --> I[Source MAC]
    I --> J[802.1Q Tag<br/>4 bytes]
    J --> K[EtherType/Length]
    K --> L[Payload]
    L --> M[FCS]
    
    style J fill:#ffeb3b,stroke:#f57f17,stroke-width:3px
```

---

## VLAN Tag Structure

### 802.1Q Tag Components
802.1Q tag is a 32-bit (or 4-byte) field between the Source MAC address and the EtherType. It comprises two main fields, the Tag Protocol Identifier (TPID) field.

### VLAN Identifier Details
12-bit VLAN identifier (VID) field that supports up to 4,096 unique VLANs, though VLAN 0 and VLAN 4095 are reserved for special purposes.

```mermaid
graph TD
    A[802.1Q Tag Structure<br/>32 bits total] --> B[TPID<br/>16 bits<br/>0x8100]
    A --> C[TCI<br/>16 bits<br/>Tag Control Information]
    
    C --> D[PCP<br/>3 bits<br/>Priority Code Point<br/>0-7]
    C --> E[DEI<br/>1 bit<br/>Drop Eligible<br/>Indicator]
    C --> F[VID<br/>12 bits<br/>VLAN Identifier<br/>0-4095]
    
    G[VLAN ID Usage] --> H[VLAN 0: Priority Frames]
    G --> I[VLAN 1: Default VLAN]
    G --> J[VLAN 2-4094: User VLANs]
    G --> K[VLAN 4095: Reserved]
    
    style B fill:#e3f2fd,stroke:#1565c0
    style D fill:#f3e5f5,stroke:#7b1fa2
    style E fill:#fff3e0,stroke:#ef6c00
    style F fill:#e8f5e8,stroke:#2e7d32
```

---

## 802.1p Quality of Service (QoS)

### QoS Overview
802.1p is a quality of service (QoS)/class of service (CoS) method that operates at the MAC layer (Layer 2). Equipment that supports 802.1p can add and recognize a value that indicates the priority level of the Ethernet frame.

### Priority Code Point (PCP) Field
The QoS technique developed by the working group, also known as class of service (CoS), is a 3-bit field called the Priority Code Point.

```mermaid
graph TD
    A[802.1p Priority Classes] --> B[3-bit PCP Field<br/>8 Priority Levels]
    
    B --> C[Priority 7<br/>Network Control<br/>Critical routing/mgmt]
    B --> D[Priority 6<br/>Voice<br/>VoIP traffic]
    B --> E[Priority 5<br/>Video<br/>Video conferencing]
    B --> F[Priority 4<br/>Controlled Load<br/>Business critical apps]
    B --> G[Priority 3<br/>Excellent Effort<br/>Important data apps]
    B --> H[Priority 2<br/>Best Effort<br/>Standard user traffic]
    B --> I[Priority 1<br/>Background<br/>Bulk transfers/backup]
    B --> J[Priority 0<br/>Best Effort<br/>Default traffic class]
    
    K[Traffic Flow] --> L[Higher Priority<br/>Gets Processed First]
    K --> M[Lower Priority<br/>Can Be Dropped First]
    
    style C fill:#d32f2f,color:white
    style D fill:#f57c00,color:white
    style E fill:#fbc02d
    style F fill:#689f38,color:white
    style G fill:#1976d2,color:white
    style H fill:#7b1fa2,color:white
    style I fill:#5d4037,color:white
    style J fill:#616161,color:white
```

---

## VLAN Assignment Methods

### Assignment Options
Several methods are used to specify the station-to-VLAN mapping, each with distinct advantages and use cases.

```mermaid
graph TD
    A[VLAN Assignment Methods] --> B[Port-Based Assignment]
    A --> C[MAC Address-Based]
    A --> D[IP Address-Based]
    
    B --> E[Advantages:<br/>• Simple to configure<br/>• Easy to manage<br/>• Common method]
    B --> F[Disadvantages:<br/>• Limited flexibility<br/>• Device mobility issues]
    
    C --> G[Advantages:<br/>• Device mobility<br/>• Persistent assignment<br/>• User follows device]
    C --> H[Disadvantages:<br/>• Complex management<br/>• MAC address changes<br/>• Large tables required]
    
    D --> I[Advantages:<br/>• Network integration<br/>• Subnet alignment<br/>• DHCP integration]
    D --> J[Disadvantages:<br/>• IP dependency<br/>• Dynamic IP issues<br/>• Layer 3 requirement]
    
    K[Switch Port 1] --> L[VLAN 10]
    K --> M[All devices on port → VLAN 10]
    
    N[MAC Table] --> O[00:1A:2B → VLAN 20]
    N --> P[00:3C:4D → VLAN 30]
    
    Q[IP Range] --> R[192.168.10.x → VLAN 10]
    Q --> S[192.168.20.x → VLAN 20]
```

---

## VLAN Trunking

### Trunking Concept and Purpose
The primary idea behind this is to be able to transport frames from multiple VLANs over a single physical link between switches.

### Trunking Configuration Requirements
In many cases, the administrator must configure the ports of the switch to be used to send 802.1p/q frames by enabling trunking on the appropriate ports.

```mermaid
graph TB
    A[Switch A] --> B[VLAN 10<br/>Accounting]
    A --> C[VLAN 20<br/>Engineering]
    A --> D[VLAN 30<br/>Marketing]
    
    B --> E[Trunk Link<br/>Tagged Frames<br/>Carries Multiple VLANs]
    C --> E
    D --> E
    
    E --> F[Switch B]
    
    F --> G[VLAN 10<br/>Accounting]
    F --> H[VLAN 20<br/>Engineering]
    F --> I[VLAN 30<br/>Marketing]
    
    J[Access Ports] --> K[Untagged<br/>Single VLAN<br/>End devices]
    L[Trunk Ports] --> M[Tagged<br/>Multiple VLANs<br/>Inter-switch links]
    
    N[Frame on Trunk] --> O[VLAN 10 Tag + Data]
    N --> P[VLAN 20 Tag + Data]
    N --> Q[VLAN 30 Tag + Data]
    
    style E fill:#4caf50,color:white
    style K fill:#2196f3,color:white
    style M fill:#ff9800,color:white
```

---

## Native VLAN Concept

### Native VLAN Definition and Purpose
The native VLAN, within the context of VLAN trunk links, is a default VLAN that carries untagged traffic.

### Native VLAN Benefits
Native VLAN concept has been introduced as a way to provide backward compatibility to a device that doesn't support VLAN tagging.

```mermaid
graph TD
    A[Trunk Port Configuration] --> B[Tagged VLANs<br/>10, 20, 30]
    A --> C[Native VLAN<br/>Default: VLAN 1<br/>Untagged]
    
    D[Incoming Frames] --> E{Frame Tagged?}
    E -->|Yes| F[Extract VLAN ID<br/>Process normally]
    E -->|No| G[Assign to Native VLAN<br/>Default: VLAN 1]
    
    F --> H[Forward to correct VLAN]
    G --> H
    
    I[Legacy Device<br/>No VLAN support] --> J[Sends untagged frames]
    J --> K[Native VLAN<br/>Provides compatibility]
    
    L[Benefits] --> M[Backward compatibility]
    L --> N[Legacy device support]
    L --> O[Simplified configuration]
    L --> P[STP compatibility]
    
    Q[Native VLAN Security] --> R[VLAN hopping attacks]
    Q --> S[Change from default VLAN 1]
    Q --> T[Proper trunk configuration]
    
    style C fill:#4caf50,color:white
    style G fill:#ff9800,color:white
    style K fill:#2196f3,color:white
```

---

## Implementation and Configuration

### Linux VLAN Configuration
The Linux command for manipulating 802.1p/q information is called vconfig.

### Advanced Configuration Options
An 802.1Q VLAN tagging interface can be created on top of bridge, bond, and team interfaces.

```mermaid
graph TD
    A[Linux VLAN Tools] --> B[vconfig Command]
    
    B --> C[Add VLAN Interface<br/>vconfig add eth0 10]
    B --> D[Remove VLAN Interface<br/>vconfig rem eth0.10]
    B --> E[Set Priority<br/>vconfig set_flag eth0.10 1 1]
    B --> F[Change Naming<br/>vconfig set_name_type DEV_PLUS_VID_NO_PAD]
    
    G[Interface Types] --> H[Physical Interfaces<br/>eth0, eth1]
    G --> I[Bridge Interfaces<br/>br0]
    G --> J[Bond Interfaces<br/>bond0]
    G --> K[Team Interfaces<br/>team0]
    
    L[Configuration Flow] --> M[Create VLAN Interface]
    M --> N[Assign IP Address]
    N --> O[Configure QoS Priority]
    O --> P[Enable Interface]
    P --> Q[Test Connectivity]
    
    R[QoS Integration] --> S[IP Precedence → 802.1p]
    S --> T[Layer 3 → Layer 2 mapping]
    T --> U[PCP field population]
    
    style B fill:#4caf50,color:white
    style M fill:#2196f3,color:white
    style S fill:#ff9800,color:white
```

---

## Benefits and Limitations

### VLAN Benefits
VLANs provide logical separation without physical changes, broadcast domain control, enhanced security through traffic isolation, and flexible network design.

### Current Industry Perspective
Combination switch/router devices have been created to address this need, and ultimately the performance of routers has been improved to match the performance of VLAN switching. Thus, the appeal of VLANs has diminished somewhat, in favor of modern high-performance routers.

```mermaid
graph TD
    A[VLAN Benefits] --> B[Network Segmentation]
    A --> C[Security Enhancement]
    A --> D[Broadcast Control]
    A --> E[Operational Flexibility]
    
    B --> F[Logical separation<br/>without physical changes]
    C --> G[Traffic isolation<br/>Access control]
    D --> H[Separate broadcast domains<br/>Reduced network congestion]
    E --> I[Easy moves/adds/changes<br/>Centralized management]
    
    J[Modern Challenges] --> K[High-performance routers]
    J --> L[Software-defined networking]
    J --> M[Container networking]
    J --> N[Cloud networking paradigms]
    
    O[Continued Relevance] --> P[Enterprise campus networks]
    O --> Q[Data center environments]
    O --> R[Legacy system integration]
    O --> S[Cost-sensitive deployments]
    O --> T[Educational requirements]
    
    U[Evolution Path] --> V[Traditional VLANs]
    V --> W[VLAN + High-perf routing]
    W --> X[SDN integration]
    X --> Y[Cloud-native networking]
    
    style A fill:#4caf50,color:white
    style J fill:#ff9800,color:white
    style O fill:#2196f3,color:white
    style U fill:#9c27b0,color:white
```

---

## Network Topology Example

```mermaid
graph TB
    A[PC1<br/>VLAN 10<br/>Accounting] --> B[Access Port<br/>Untagged<br/>VLAN 10]
    C[PC2<br/>VLAN 20<br/>Engineering] --> D[Access Port<br/>Untagged<br/>VLAN 20]
    E[Server<br/>VLAN 30<br/>DMZ] --> F[Access Port<br/>Untagged<br/>VLAN 30]
    
    B --> G[Switch 1<br/>Access Layer]
    D --> G
    
    F --> H[Switch 2<br/>Distribution Layer]
    
    G --> I[Trunk Port<br/>Tagged: 10,20,30<br/>Native: VLAN 1]
    I --> J[Trunk Link<br/>802.1Q Tagged Frames]
    J --> K[Trunk Port<br/>Tagged: 10,20,30<br/>Native: VLAN 1]
    K --> H
    
    H --> L[Router<br/>Inter-VLAN Routing<br/>Layer 3 Gateway]
    
    M[Traffic Flow Examples] --> N[VLAN 10 → Priority 2<br/>Standard business data]
    M --> O[VLAN 20 → Priority 5<br/>Engineering CAD files]
    M --> P[VLAN 30 → Priority 6<br/>Server traffic]
    
    style G fill:#4caf50,color:white
    style H fill:#2196f3,color:white
    style J fill:#ff9800,color:white
    style L fill:#9c27b0,color:white
```

---

## Frame Processing Workflow

```mermaid
graph TD
    A[Frame Arrives at Switch] --> B{Is Frame Tagged?}
    
    B -->|Yes| C[Extract 802.1Q Tag]
    B -->|No| D[Assign to Native VLAN<br/>Default: VLAN 1]
    
    C --> E[Read VLAN ID<br/>12-bit VID field]
    C --> F[Read Priority<br/>3-bit PCP field]
    
    E --> G{VLAN Exists on Switch?}
    G -->|Yes| H[Forward to VLAN Members]
    G -->|No| I[Drop Frame<br/>Log Error]
    
    F --> J[Apply QoS Policy<br/>Based on Priority]
    J --> K[Queue Frame<br/>According to Priority]
    
    D --> L[Process as Native VLAN]
    L --> H
    
    H --> M{Destination Port Type?}
    M -->|Access Port| N[Remove VLAN Tag<br/>Send Untagged]
    M -->|Trunk Port| O[Keep/Add VLAN Tag<br/>Send Tagged]
    
    N --> P[Frame Delivered<br/>to End Device]
    O --> Q[Frame Sent<br/>to Next Switch]
    
    style C fill:#4caf50,color:white
    style J fill:#ff9800,color:white
    style M fill:#2196f3,color:white
```

---

## VLAN

![Link Layer 8](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_8.jpg)

![Link Layer 9](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_9.jpg)

![Link Layer 10](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_10.jpg)

![Link Layer 11](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_11.jpg)

![Link Layer 12](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_12.jpg)

# Link Aggrigation (802.1AX)

![Link Layer 13](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_13.jpg)

![Link Layer 14](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_14.jpg)

![Link Layer 15](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_15.jpg)

![Link Layer 16](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_16.jpg)

![Link Layer 17](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_17.jpg)

![Link Layer 18](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_18.jpg)

## Real-Time Industry Applications

1. Enterprise Data Centers
  
  * Application: Server-to-Switch Connectivity
    
    * Implementation: Multiple 10/25/40 Gbps links bonded per server
    
    * Benefits: Higher bandwidth for virtualized environments, redundancy for critical applications
    
    * Configuration: Typically uses Mode 4 (802.3ad) with LACP for automatic failover
    
    * Case Study: Large enterprises bond 4 × 10 Gbps links to achieve 40 Gbps effective bandwidth with 3+1 redundancy. If one link fails, remaining three continue operation with 30 Gbps capacity.

2. Cloud Service Providers
  
  * Application: Inter-Switch Links (ISLs)
    
    * Implementation: High-density 100 Gbps+ aggregated links between core switches
    
    * Benefits: Massive bandwidth scaling, seamless failover
    
    * Advanced Feature: Dynamic load balancing based on real-time traffic patterns

    * Real Example: AWS data centers use link aggregation for spine-leaf architectures, bonding multiple 100 Gbps links between leaf and spine switches to handle massive east-west traffic flows.

3. Financial Services
  
  * Application: High-Frequency Trading (HFT) Networks

    * Implementation: Ultra-low latency trading systems with redundant paths

    * Benefits: Microsecond-level failover, guaranteed connectivity to exchanges
    
    * Specialized Configuration: Custom bonding with hardware timestamping

    * Critical Requirement: Sub-millisecond failover times require specialized network interface cards with hardware-based link aggregation and immediate path switching capabilities.

4. Telecommunications
  * Application: 5G Network Infrastructure
    
    * Implementation: Carrier aggregation at base stations and core network
    
    * Benefits: Bandwidth scaling for massive IoT and mobile broadband
    
    * Integration: Combined with Software-Defined Networking (SDN) for dynamic resource allocation

    * 5G Specific Use: Link aggregation enables combining multiple fiber optic connections from cell towers to core networks, providing the backhaul capacity needed for 5G's high data rates.

5. Healthcare Systems
    
  * Application: Medical Imaging and Telemedicine

    * Implementation: Hospital network infrastructure with guaranteed bandwidth

    * Benefits: Reliable transfer of large medical images, real-time video consultations

    * Compliance: Meets HIPAA requirements for network reliability and redundancy

    * Critical Application: Remote surgery systems require guaranteed network availability and bandwidth. Link aggregation provides the redundancy and performance needed for life-critical applications.

6. Content Delivery Networks (CDNs)
  
  * Application: Edge Server Connectivity
  
    * Implementation: CDN edge servers with multiple high-bandwidth connections
    
    * Benefits: Improved content delivery speeds, geographic load distribution
    
    * Performance: Reduces latency for streaming services and web content

    * Industry Impact: Major streaming platforms use link aggregation at edge locations to ensure consistent 4K/8K video delivery during peak usage periods.

7. Educational Institutions

  * Application: Campus Network Backbone

    * Implementation: University networks connecting dormitories, academic buildings
    
    * Benefits: Cost-effective bandwidth scaling, future-proof infrastructure
    
    * Scale: Supports thousands of simultaneous users with varying bandwidth needs

    * Research Networks: Universities conducting data-intensive research use link aggregation to connect to national research networks like Internet2, enabling collaboration on big data projects.


### Advanced Technical Implementations

1. Multi-Chassis Link Aggregation (MLAG)
  
  * Concept: Extends link aggregation across multiple physical switches
  
  * Benefit: Eliminates single points of failure in network design
  
  * Implementation: Requires specialized switch hardware and synchronization protocols

  * Use Case: Data centers deploy MLAG to connect servers to two different switches simultaneously, ensuring network availability even if an entire switch fails.

2. Dynamic Load Balancing Algorithms
  
  * Hash-Based Distribution:

  * Layer 2: Source/Destination MAC addresses

  * Layer 3: Source/Destination IP addresses
  
  * Layer 4: TCP/UDP port numbers
  
  * Custom: Application-specific flow identification


## Network Interface Concepts: Full Duplex, Power Save, Auto-negotiation, 802.1X, and Flow Control

```bash
$ sudo ethtool eth0
Settings for eth0:
        Supported ports: [ TP    MII ]
        Supported link modes:   10baseT/Half 10baseT/Full
                                100baseT/Half 100baseT/Full
                                1000baseT/Half 1000baseT/Full
        Supported pause frame use: Transmit-only
        Supports auto-negotiation: Yes
        Supported FEC modes: Not reported
        Advertised link modes:  10baseT/Half 10baseT/Full
                                100baseT/Half 100baseT/Full
                                1000baseT/Half 1000baseT/Full
        Advertised pause frame use: Transmit-only
        Advertised auto-negotiation: Yes
        Advertised FEC modes: Not reported
        Link partner advertised link modes:  10baseT/Half 10baseT/Full
                                             100baseT/Half 100baseT/Full
                                             1000baseT/Half 1000baseT/Full
        Link partner advertised pause frame use: Symmetric Receive-only
        Link partner advertised auto-negotiation: Yes
        Link partner advertised FEC modes: Not reported
        Speed: 1000Mb/s
        Duplex: Full
        Auto-negotiation: on
        master-slave cfg: preferred slave
        master-slave status: slave
        Port: Twisted Pair
        PHYAD: 1
        Transceiver: external
        MDI-X: Unknown
        Supports Wake-on: ag
        Wake-on: d
        Link detected: yes
```

![Link Layer 19](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_19.jpg)


![Link Layer 21](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_21.jpg)

![Link Layer 20](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_20.png)

![Link Layer 22](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_22.jpg)

  * `The negotiation process`

     
    * Advertisement Phase: Each device advertises its capabilities
      ```bash
      Advertised link modes:  10baseT/Half 10baseT/Full
                       100baseT/Half 100baseT/Full
                       1000baseT/Half 1000baseT/Full
      ```

    * Partner Detection: Devices detect what the other end supports

      ```bash
      Link partner advertised link modes:  10baseT/Half 10baseT/Full
                                    100baseT/Half 100baseT/Full
                                    1000baseT/Half 1000baseT/Full
      ```

![Link Layer 23](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_23.jpg)

![Link Layer 24](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_24.jpg)

---

# Bridges and Switches

![Link Layer 25](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_25.jpg)

![Link Layer 26](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_26.jpg)   

![Link Layer 27](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/link_layer_27.jpg)

![Link Layer 28](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_28.jpg)

![Link Layer 29](https://github.com/dev-hack95/notes/blob/main/network_programming/notes/assets/link_layer_29.jpg)

---

# STP Port States and Roles

## Overview
Spanning Tree Protocol (STP) uses a state machine for each port on every bridge/switch to prevent loops in Ethernet networks. Understanding port states and roles is crucial for network topology management.

## Port States in STP

### The Five Port States

1. **Blocking State**
   - Initial state after initialization
   - **Cannot**: Learn MAC addresses, forward frames, or transmit BPDUs
   - **Can**: Monitor and receive BPDUs
   - Purpose: Wait for potential inclusion in spanning tree path

2. **Listening State** 
   - Transition from blocking when port might be needed
   - **Can**: Send and receive BPDUs
   - **Cannot**: Learn MAC addresses or forward data frames
   - Duration: Temporary state during topology calculation

3. **Learning State**
   - Follows listening state after forwarding delay (15 seconds)
   - **Can**: Learn MAC addresses, send/receive BPDUs
   - **Cannot**: Forward data frames yet
   - Purpose: Build MAC address table before forwarding

4. **Forwarding State**
   - Final operational state for active ports
   - **Can**: Do everything - learn addresses, forward frames, handle BPDUs
   - Duration: Another forwarding delay (15 seconds) from learning state

5. **Disabled State**
   - Administratively shut down
   - **Cannot**: Participate in any STP operations
   - Triggered by: Manual configuration or hardware failure

### State Transition Timing
- **Forwarding Delay**: 15 seconds (typical)
- **Total Transition Time**: Blocking → Listening → Learning → Forwarding = ~30 seconds
- **Max Age**: Time to wait for BPDUs before declaring topology change

## Port Roles in STP

### Root Port
- **Definition**: Port with best path toward root bridge
- **Characteristics**:
  - One per bridge (except root bridge)
  - Always in forwarding state when active
  - Receives BPDUs from root direction
- **Selection Criteria**: Lowest root path cost

### Designated Port
- **Definition**: Port responsible for forwarding to attached segment
- **Characteristics**:
  - One per network segment
  - Always in forwarding state
  - Sends BPDUs to segment
  - Represents least-cost path to root for that segment

### Alternate Port
- **Definition**: Backup path to root bridge
- **Characteristics**:
  - Higher cost path than current root port
  - Remains in blocking state
  - Can become root port if primary path fails
  - Provides redundancy

### Backup Port
- **Definition**: Secondary port on same segment as designated port
- **Characteristics**:
  - Connected to same segment as another port on same bridge
  - Remains in blocking state
  - Can replace failing designated port quickly
  - Doesn't provide alternate root path

## Key Concepts Explained

### Why Port States Matter
The gradual transition through states prevents:
- **Temporary loops** during topology changes
- **MAC address table corruption** 
- **Broadcast storms**

### RSTP State Names (in parentheses from diagram)
- Blocking → **Discarding**
- Listening → **Discarding** 
- Learning → **Learning**
- Forwarding → **Forwarding**
- Disabled → **Discarding**

### Administrative vs. Automatic Transitions
- **Solid arrows**: Normal STP operations
- **Dashed arrows**: Manual configuration changes
- **Topology changes** can trigger state transitions

## Important Timing Values

| Parameter | Typical Value | Purpose |
|-----------|---------------|---------|
| Forwarding Delay | 15 seconds | Time between state transitions |
| Max Age | 20 seconds | BPDU timeout period |
| Hello Time | 2 seconds | BPDU transmission interval |

## Practical Implications

### Network Convergence
- **Convergence Time**: Up to 50 seconds for complete topology change
- **Port Recovery**: 30 seconds for port to become operational
- **Impact**: Temporary connectivity loss during transitions

### Troubleshooting Tips
1. **Stuck in Learning**: Check for BPDU conflicts
2. **Frequent State Changes**: Look for unstable links
3. **Long Convergence**: Verify timer configurations
4. **Disabled Ports**: Check physical connections and admin status

### Modern Improvements
- **RSTP (802.1w)**: Faster convergence (2-3 seconds)
- **Per-VLAN STP**: Separate spanning trees per VLAN
- **MST**: Multiple spanning trees for better load balancing

## Best Practices

1. **Root Bridge Placement**: Position at network core
2. **Port Priorities**: Manually configure for predictable paths  
3. **PortFast**: Enable on end-device ports to skip listening/learning
4. **BPDU Guard**: Protect against unauthorized bridges
5. **Monitor State Changes**: Log transitions for troubleshooting

---

```mermaid
graph TD
    A[Initialize] --> B[Blocking State]
    B --> |"Max Age Timeout<br/>or Topology Change"| C[Listening State]
    C --> |"Forward Delay<br/>(15 seconds)"| D[Learning State] 
    D --> |"Forward Delay<br/>(15 seconds)"| E[Forwarding State]
    
    %% Administrative transitions (dashed)
    B -.-> |"Admin Disable"| F[Disabled State]
    C -.-> |"Admin Disable"| F
    D -.-> |"Admin Disable"| F
    E -.-> |"Admin Disable"| F
    E -.-> |"Topology Change"| B
    F -.-> |"Admin Enable"| B
    
    %% State descriptions
    B --> B1["❌ Cannot:<br/>• Learn MAC addresses<br/>• Forward frames<br/>• Transmit BPDUs<br/><br/>✅ Can:<br/>• Monitor BPDUs"]
    C --> C1["❌ Cannot:<br/>• Learn MAC addresses<br/>• Forward frames<br/><br/>✅ Can:<br/>• Send/Receive BPDUs"]
    D --> D1["❌ Cannot:<br/>• Forward frames<br/><br/>✅ Can:<br/>• Learn MAC addresses<br/>• Send/Receive BPDUs"]
    E --> E1["✅ Can do everything:<br/>• Learn MAC addresses<br/>• Forward frames<br/>• Send/Receive BPDUs"]
    F --> F1["❌ Admin shutdown:<br/>• No STP participation"]
    
    style A fill:#e1f5fe
    style B fill:#ffebee
    style C fill:#fff3e0
    style D fill:#f3e5f5
    style E fill:#e8f5e8
    style F fill:#fafafa
    
    style B1 fill:#ffebee
    style C1 fill:#fff3e0
    style D1 fill:#f3e5f5
    style E1 fill:#e8f5e8
    style F1 fill:#fafafa

```
---

```mermaid
graph TB
    subgraph "STP Network Topology Example"
        RB[Root Bridge<br/>Priority: 0]
        
        subgraph "Bridge A"
            BA_RP[Root Port<br/>Cost: 4<br/>State: Forwarding]
            BA_DP1[Designated Port<br/>State: Forwarding]
            BA_BP[Backup Port<br/>State: Blocking]
        end
        
        subgraph "Bridge B" 
            BB_RP[Root Port<br/>Cost: 8<br/>State: Forwarding]
            BB_DP[Designated Port<br/>State: Forwarding]
            BB_AP[Alternate Port<br/>Cost: 12<br/>State: Blocking]
        end
        
        subgraph "Bridge C"
            BC_RP[Root Port<br/>Cost: 10<br/>State: Forwarding] 
            BC_DP[Designated Port<br/>State: Forwarding]
        end
        
        subgraph "Segments"
            S1[Segment 1]
            S2[Segment 2] 
            S3[Segment 3]
            S4[Segment 4]
        end
        
        %% Root bridge connections
        RB --- BA_RP
        RB --- BB_RP
        RB --- BC_RP
        
        %% Inter-bridge connections
        BA_DP1 --- S1
        S1 --- BB_AP
        BA_BP --- S2
        BA_DP1 --- S2
        BB_DP --- S3
        S3 --- BC_DP
        
        %% Port role legends
        RP_Legend["🟢 Root Port:<br/>• Best path to root<br/>• One per bridge<br/>• Always forwarding"]
        DP_Legend["🔵 Designated Port:<br/>• Best path from segment to root<br/>• One per segment<br/>• Always forwarding"]
        AP_Legend["🟡 Alternate Port:<br/>• Backup path to root<br/>• Higher cost than root port<br/>• Blocking state"]
        BP_Legend["🟠 Backup Port:<br/>• Same segment as designated port<br/>• Same bridge<br/>• Blocking state"]
        
    end
    
   
```

---

```mermaid
gantt
    title STP Port State Convergence Timeline
    dateFormat X
    axisFormat %s
    
    section Port Activation
    Blocking State          :blocking, 0, 20
    Listening State         :listening, 20, 35  
    Learning State          :learning, 35, 50
    Forwarding State        :active, forwarding, 50, 80
    
    section Key Events
    BPDU Reception         :milestone, bpdu1, 5
    Topology Decision      :milestone, decision, 20
    Start Learning MACs    :milestone, mac_learn, 35
    Begin Forwarding       :milestone, forward_start, 50
    Full Operation         :milestone, full_op, 50
    
    section Timing Parameters
    Max Age (20s)          :crit, max_age, 0, 20
    Forward Delay 1 (15s)  :crit, fd1, 20, 35
    Forward Delay 2 (15s)  :crit, fd2, 35, 50
    
    section Recovery Scenario  
    Link Failure           :milestone, failure, 60
    Topology Change        :topo_change, 60, 65
    Reconvergence          :reconv, 65, 95

```

# BPDU Structure and Format

## Overview
Bridge Protocol Data Units (BPDUs) are the control messages used by Spanning Tree Protocol (STP) to build and maintain loop-free network topologies. Understanding BPDU structure is crucial for network troubleshooting and STP operation.

## BPDU Frame Structure

### Ethernet Header (14 bytes)
- **Destination (DST)**: `01:80:C2:00:00:00` (Bridge group multicast address)
- **Source (SRC)**: MAC address of sending bridge port
- **Length/Type (L/T)**: Frame length or EtherType field

### LLC/SNAP Header (3 bytes)
- **LLC/SNAP**: `0x424203` (constant value for BPDUs)
- **Purpose**: 802.1 standard encapsulation
- **Note**: Not all BPDUs use LLC/SNAP, but it's common

## BPDU Payload Fields

### Protocol Identification
| Field | Size | Value | Description |
|-------|------|-------|-------------|
| **Protocol (Prot)** | 2 bytes | 0 | Protocol ID number |
| **Version (Vers)** | 1 byte | 0 or 2 | STP=0, RSTP=2 |
| **Type** | 1 byte | 0 or 2 | Message type |

### Flags Field (1 byte)
Critical for STP operation and RSTP enhancements:

#### Original STP Flags
- **TC (Topology Change)**: Bit indicates topology change
- **TCA (Topology Change Acknowledgment)**: Acknowledges TC

#### RSTP Additional Flags  
- **P (Proposal)**: Port role negotiation
- **Port Role** (2 bits): 
  - 00 = Unknown
  - 01 = Alternate/Backup
  - 10 = Root  
  - 11 = Designated
- **L (Learning)**: Port learning state
- **F (Forwarding)**: Port forwarding state
- **A (Agreement)**: Agreement to proposal

### Bridge Identification Fields

#### Root ID (8 bytes)
- **Structure**: 2-byte Priority + 6-byte MAC Address
- **Purpose**: Identifies root bridge as seen by sender
- **Priority**: Default varies (Cisco uses 0x8000/32768)
- **Selection**: Lowest combined value becomes root

#### Bridge ID (8 bytes)  
- **Structure**: 2-byte Priority + 6-byte MAC Address
- **Purpose**: Identifies the sending bridge
- **Usage**: Used in root bridge election process

### Path Information
| Field | Size | Description |
|-------|------|-------------|
| **Root Path Cost** | 4 bytes | Cost to reach root bridge |
| **Port ID (PID)** | 2 bytes | 1-byte Priority + 1-byte Port Number |

### Timing Parameters (All in 1/256 second units)
| Field | Size | Default | Purpose |
|-------|------|---------|---------|
| **Message Age (MsgA)** | 2 bytes | Variable | Hop count from root |
| **Maximum Age (MaxA)** | 2 bytes | 20s | BPDU timeout value |
| **Hello Time** | 2 bytes | 2s | BPDU transmission interval |
| **Forward Delay** | 2 bytes | 15s | Learning/Listening state duration |

## Message Age Field Operation

### Special Behavior
- **Root Bridge**: Sets Message Age = 0 when sending
- **Receiving Bridges**: Increment by 1 before forwarding
- **Function**: Acts as hop counter through spanning tree
- **Timeout Calculation**: (MaxA - MsgA) = remaining lifetime

### Timeout Process
1. BPDU received with Message Age value
2. Information stored for (MaxA - MsgA) time
3. If no new BPDU received before timeout:
   - Root bridge declared "dead"
   - Root election process restarts

## BPDU Types and Versions

### Standard STP (802.1D)
- **Version**: 0
- **Type**: 0 (Configuration BPDU)
- **Special**: TCN (Topology Change Notification) BPDUs exist

### RSTP (802.1w/802.1D-2004)
- **Version**: 2  
- **Type**: 2
- **Improvement**: Single BPDU type for all messages
- **Enhanced**: Uses all 6 bits in Flags field

## BPDU Transmission Rules

### Addressing
- **Destination**: Always `01:80:C2:00:00:00`
- **Scope**: Link-local multicast
- **Forwarding**: Never forwarded unchanged through bridges

### Frequency
- **STP**: Sent by root bridge every Hello Time (2s default)
- **RSTP**: All bridges send as keepalives every Hello Time

### Processing
- **Reception**: All bridge ports monitor BPDUs
- **Modification**: Bridges update fields before forwarding
- **Filtering**: End stations ignore BPDUs

## Practical Example Analysis

### Real BPDU Capture (52 bytes total)
```
Ethernet Header (14 bytes):
- DST: 01:80:C2:00:00:00 (Bridge group)
- SRC: 00:07:e9:14:a9:c1 (Sending bridge)
- Length: 38 bytes (payload)

BPDU Fields:
- Version: 0 (Standard STP)
- Root ID: 8000.0007e914a9c1 (Priority 32768)
- Bridge ID: 8000.0007e914a9c1 (Same as root - this IS root)
- Port ID: Port 2, Priority 0x80
- Timers: MaxAge=20s, Hello=2s, FwdDelay=15s
```

## Key Concepts Explained

### Priority Manipulation
- **Purpose**: Force specific root bridge selection
- **Method**: Lower priority values win election
- **Default**: 32768 (0x8000) common default
- **Admin**: Can be configured via management software

### Path Cost Calculation
- **10 Mbps Ethernet**: Cost = 100
- **100 Mbps Ethernet**: Cost = 19  
- **1 Gbps Ethernet**: Cost = 4
- **Rule**: Higher speed = lower cost

### BPDU Aging Process
1. **Reception**: BPDU received and stored
2. **Timer Start**: (MaxAge - MsgAge) countdown begins
3. **Refresh**: New BPDU resets timer
4. **Timeout**: Information purged, topology recalculated

## Troubleshooting with BPDUs

### Common Issues
- **BPDU Filtering**: Blocks BPDU transmission/reception
- **BPDU Guard**: Shuts port if BPDU received
- **Root Bridge Flapping**: Inconsistent priority/MAC values
- **Timing Mismatches**: Different Hello/MaxAge values

### Analysis Tools
- **Wireshark**: Capture and decode BPDUs
- **Switch Commands**: `show spanning-tree detail`
- **Linux**: `brctl showstp <bridge>`

### Key Indicators
- **Message Age**: Shows distance from root
- **Port Role**: Indicates expected forwarding behavior
- **Flags**: Reveal topology change events
- **Timers**: Help identify timing issues

## RSTP Improvements

### Enhanced Flag Usage
- **Proposal/Agreement**: Faster convergence negotiation
- **Port Roles**: Explicit role communication
- **State Sync**: Learning/Forwarding status sharing

### Operational Changes
- **Keepalive BPDUs**: All bridges send periodic updates
- **Immediate Topology Changes**: No root notification required
- **Edge Port Detection**: Skip unnecessary state transitions

### Convergence Benefits
- **STP**: 30-50 seconds typical convergence
- **RSTP**: Sub-second convergence in most cases
- **Method**: Eliminates timer dependencies where possible

## Best Practices

### Network Design
1. **Root Bridge**: Place centrally with lowest priority
2. **Backup Root**: Configure secondary with slightly higher priority
3. **Port Priorities**: Set manually for predictable paths
4. **Edge Ports**: Configure PortFast on end-device connections

### Monitoring
1. **Regular BPDU Analysis**: Check for anomalies
2. **Topology Change Tracking**: Monitor TC flag frequency
3. **Timer Verification**: Ensure consistent values network-wide
4. **Root Stability**: Alert on unexpected root changes


```mermaid
graph TB
    subgraph "BPDU Frame Structure (52 bytes typical)"
        subgraph "Ethernet Header (14 bytes)"
            ETH_DST["Destination<br/>01:80:C2:00:00:00<br/>(6 bytes)"]
            ETH_SRC["Source MAC<br/>Bridge Port Address<br/>(6 bytes)"]
            ETH_LEN["Length/Type<br/>Frame Length<br/>(2 bytes)"]
        end
        
        subgraph "LLC/SNAP Header (3 bytes)"
            LLC["LLC/SNAP<br/>0x424203<br/>(3 bytes)"]
        end
        
        subgraph "BPDU Payload (35+ bytes)"
            PROT["Protocol ID<br/>0<br/>(2 bytes)"]
            VERS["Version<br/>0=STP, 2=RSTP<br/>(1 byte)"]
            TYPE["Type<br/>0=Config, 2=RSTP<br/>(1 byte)"]
            
            subgraph "Flags (1 byte)"
                FLAGS["Bits 7-6: Unused<br/>Bit 5: TC Ack<br/>Bit 4: Agreement (RSTP)<br/>Bit 3-2: Port Role (RSTP)<br/>Bit 1: Learning (RSTP)<br/>Bit 0: TC"]
            end
            
            ROOT_ID["Root Bridge ID<br/>Priority (2) + MAC (6)<br/>(8 bytes)"]
            ROOT_COST["Root Path Cost<br/>Cost to Root<br/>(4 bytes)"]
            BRIDGE_ID["Bridge ID<br/>Priority (2) + MAC (6)<br/>(8 bytes)"]
            PORT_ID["Port ID<br/>Priority (1) + Port# (1)<br/>(2 bytes)"]
            MSG_AGE["Message Age<br/>Hop Count * 1/256s<br/>(2 bytes)"]
            MAX_AGE["Max Age<br/>20s default * 1/256s<br/>(2 bytes)"]
            HELLO["Hello Time<br/>2s default * 1/256s<br/>(2 bytes)"]
            FWD_DELAY["Forward Delay<br/>15s default * 1/256s<br/>(2 bytes)"]
        end
    end
    
    ETH_DST --> ETH_SRC
    ETH_SRC --> ETH_LEN
    ETH_LEN --> LLC
    LLC --> PROT
    PROT --> VERS
    VERS --> TYPE
    TYPE --> FLAGS
    FLAGS --> ROOT_ID
    ROOT_ID --> ROOT_COST
    ROOT_COST --> BRIDGE_ID
    BRIDGE_ID --> PORT_ID
    PORT_ID --> MSG_AGE
    MSG_AGE --> MAX_AGE
    MAX_AGE --> HELLO
    HELLO --> FWD_DELAY
```


---

```mermaid

graph LR
    subgraph "BPDU Flags Field (8 bits)"
        subgraph "Standard STP Usage"
            BIT7[Bit 7<br/>Unused<br/>0]
            BIT6[Bit 6<br/>Unused<br/>0] 
            BIT5[Bit 5<br/>TC Ack<br/>Topology Change ACK]
            BIT4[Bit 4<br/>Unused in STP<br/>0]
            BIT3[Bit 3<br/>Unused in STP<br/>0]
            BIT2[Bit 2<br/>Unused in STP<br/>0]
            BIT1[Bit 1<br/>Unused in STP<br/>0]
            BIT0[Bit 0<br/>TC<br/>Topology Change]
        end
        
        subgraph "RSTP Enhanced Usage"
            BIT7_R[Bit 7<br/>Unused<br/>0]
            BIT6_R[Bit 6<br/>Unused<br/>0]
            BIT5_R[Bit 5<br/>TC Ack<br/>Topology Change ACK]
            BIT4_R[Bit 4<br/>Agreement<br/>Proposal Response]
            BIT3_R[Bit 3<br/>Port Role<br/>MSB]
            BIT2_R[Bit 2<br/>Port Role<br/>LSB]
            BIT1_R[Bit 1<br/>Learning<br/>Port Learning State]
            BIT0_R[Bit 0<br/>TC<br/>Topology Change]
        end
    end
    
    subgraph "Port Role Encoding (Bits 3-2)"
        ROLE00[00<br/>Unknown<br/>Role not defined]
        ROLE01[01<br/>Alternate/Backup<br/>Blocked port]
        ROLE10[10<br/>Root Port<br/>Path to root]
        ROLE11[11<br/>Designated<br/>Forwarding port]
    end
    
    subgraph "Flag Combinations Example"
        EX1["Normal Operation:<br/>TC=0, TCA=0<br/>Role=11 (Designated)<br/>Learning=1, Forwarding=1"]
        EX2["Topology Change:<br/>TC=1, TCA=0<br/>Role=10 (Root)<br/>Learning=1, Forwarding=1"]  
        EX3["Proposal/Agreement:<br/>Agreement=1<br/>Role=11 (Designated)<br/>Learning=0, Forwarding=0"]
    end
    
    BIT7 --> BIT6
    BIT6 --> BIT5  
    BIT5 --> BIT4
    BIT4 --> BIT3
    BIT3 --> BIT2
    BIT2 --> BIT1
    BIT1 --> BIT0
    
    BIT7_R --> BIT6_R
    BIT6_R --> BIT5_R
    BIT5_R --> BIT4_R
    BIT4_R --> BIT3_R
    BIT3_R --> BIT2_R
    BIT2_R --> BIT1_R
    BIT1_R --> BIT0_R
    
    BIT3_R -.-> ROLE00
    BIT3_R -.-> ROLE01
    BIT2_R -.-> ROLE10
    BIT2_R -.-> ROLE11
```

