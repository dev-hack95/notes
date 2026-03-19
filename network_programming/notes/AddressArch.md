# `Address And Architecture`

  * Internet Protocol (IP) addresses serve as unique identifiers for devices connected to
    computer networks, enabling communication across internet. There are two primary versions
    are used in internet and these are IPv4 and IPv6 each with different notation format.


  * `IPv4`


    * IPv4 are 32-bit address denoted by dotted decimal notation. A 32-bit address contains two
      primary parts i.e the network prefix and the host number

      * **Example**

        * 192.168.1.1
        
        * 10.55.0.6

        * 172.19.0.1

    * `IPv4 Classful Addressing`

      * The 4-octet(32-bit) Ip address is devided into three class types

        * `Class-A`

           * A Class A IPv4 address has 8 network prefix bits. For example, consider 44.0.0.1,
             where 44 is the network address and 0.0.1 is the host address.

        * `Class-B`

           * A Class B IPv4 address has 16 network prefix bits. For example, consider 128.16.0.2,
             where 128.16 is the network address and 0.2 is the host address.

        * `Class-C`

           * A Class C IPv4 address has 24 network prefix bits. For instance, consider 192.168.1.100,
             where 192.168.1 is the network address and 100 is the host address.

        * Binary Notation
        
        ```text
          00000000 xxxxxxxx xxxxxxxx xxxxxxxx (Class A)
          00000000 00000000 xxxxxxxx xxxxxxxx (Class B)
          00000000 00000000 00000000 xxxxxxxx (Class C)
        ```

    * `IPv4 Subnetting`

      * Beacuse of the physical and architecctural limitations on the size of networks, you often
        must break large networks into smaller subnetted network


        * ![Subnets](https://github.com/dev-hack95/QuantPrep/blob/main/notes/networks/assets/subnets-ipv4.png)

        * Three devices are connected to the alpha subnet on the left, three devices connected to
          the beta subnet on the right. and third subnet named gamma that interconnects the left
          and right subnets over WAN link.

          
  * `IPv6`

    * IPv6 addresses are 128-bit address that provice a significantly larger address space compared
      to IPv4. The prefered IPv6 address representation is `x:x:x:x:x:x:x:x`, where each x represents
      the hexadecimal values of eight 16-bits pieces of the address

      * **Range** : `0000:0000:0000:0000:0000:0000:0000:0000` to `ffff:ffff:ffff:ffff:ffff:ffff:ffff:ffff`


      * **IPv6 Rules**


        * **Rule-1** : Leading zero omission, leading zero can be omitted from address


          * i.e: 1050:0000:0000:0000:0005:0600:300c:326b -- converts to -> 1050:0:0:5:600:300c:326b


        * **Rule-2** : Zero compression, consecutive segments of zeros can be replaces with double
                       column

          * i.e: ff06:0000:0000:0000:0000:0000:0000:00c3 -- converts to --> ff06::c3

          * i.e: 2001:0db8:0000:0000:0000:0000:0000:0002 -- converts to --> 2001:db8::2


      * `IPv6 Address types`

        * Ipv6 supports secveral types of addresses, ech with different communication purpose


          * `Unicast Addresses`

             * **Global Unicast** Internet routable address similar to public ipv4 addresses

             * **Link Local** : Used for communication within a single local network segment
                                typically prefixed with fe80::/10, Link local IPv6 address allow
                                communication b/w devices on single local link. It is not globally
                                routable i.e `inet6 fe80::5de:67ce:b090:e944  prefixlen 64  scopeid 0x20<link>`

          * `Multicast Addresses`

             * IPv6  multicast is one to many communication method where a single packet sent to
               multicast address is delivered to interfaces that have joined that specific multi-
               cast group. unlike unicast (one to one) or broadcast (ont to all). multicast provide
               efficient group communication.


             ```mermaid

                graph LR
                    A[Sender Host<br/>2001:db8::1] -->|Sends to ff02::1| B[Router R1<br/>Link-Local Segment]
    
                    B --> C[Host A<br/>2001:db8::10<br/>Joined ff02::1]
                    B --> D[Host B<br/>2001:db8::11<br/>Joined ff02::1]
                    B --> E[Host C<br/>2001:db8::12<br/>NOT in group]
                    B --> F[Router R2<br/>2001:db8::20]
    
                    F --> G[Host D<br/>2001:db8::21<br/>Joined ff02::1]
                    F --> H[Host E<br/>2001:db8::22<br/>NOT in group]
    
                      
                    subgraph "Multicast Group ff02::1 Members"
                        I[✓ Host A - Receives packet]
                        J[✓ Host B - Receives packet]
                        K[✓ Host D - Receives packet]
                    end
    
                    subgraph "Non-Members"
                        L[✗ Host C - No packet]
                        M[✗ Host E - No packet]
                    end
    
                    subgraph "Key Multicast Addresses"
                        N["ff02::1 - All Nodes<br/>(Link-Local Broadcast)"]
                        O["ff02::2 - All Routers<br/>(Link-Local)"]
                        P["ff02::5 - OSPFv3 Routers"]
                        Q["ff02::6 - OSPFv3 DR/BDR"]
                    end
             ```

          * `Anycast addresses`

            * Anycast addresses identify multiple interfaces, but packets are sent only to the closest
              interface as determined by routing protocols. It's able to discover multiple interfaces
              but allowed to send packet to only one.


          * `Special Addresses`

            * **Loopback addresses** : Used by node to send a IPv6 packet to itself. An IPv6 loopback
                                       address is `0000:0000:0000:0000:0000:0000:0000:0001/128` which can
                                       be represented as `::1`.
                                      
            * **Unspecified addresses** : It's a addresses type which is used to communicate when interface
                                          is not assigned with an ipv6 addresses and can be denoted as
                                          `0000:0000:0000:0000:0000:0000:0000:0000` which can be shortned to `::`

          * `IPv4-Mapped IPv6 Addresses`

            * IPv6 supports an alternative format that combines colon and dotted notation to embed
              IPv4 addresses within IPv6 addresses . This format specifies hexadecimal values for
              the left-most 96 bits and decimal values for the right-most 32 bits . Examples include:

              * 0:0:0:0:0:ffff:192.1.56.10

              * ::ffff:192.1.56.10/96 (shortened format)

          * ![IPv6 Address Types](https://github.com/dev-hack95/QuantPrep/blob/main/notes/networks/assets/ipv6-address-types.png)


          ```mermaid
          graph LR
              A[IPv6 Address Types<br/>128-bit Addresses] --> B[Unicast<br/>One-to-One]
              A --> C[Multicast<br/>One-to-Many]
              A --> D[Anycast<br/>One-to-Closest]
              A --> E[No Broadcast<br/>Replaced by Multicast]
    
              B --> F[Global Unicast<br/>2000::/3]
              B --> G[Link-Local<br/>FE80::/10]
              B --> H[Unique Local<br/>FC00::/7]
              B --> I[Loopback<br/>::1/128]
              B --> J[Unspecified<br/>::/128]
              B --> K[Embedded IPv4<br/>::IPv4-addr]
    
              C --> L[Well-known<br/>FF00::/12]
              C --> M[Solicited-Node<br/>FF02::1:FF00:0/104]
    
              F --> N[Aggregatable<br/>Hierarchical Allocation]
              F --> O[Internet Routable]
    
              G --> P[Auto-configured]
              G --> Q[Non-routable]
              G --> R[Link Scope Only]
    
              H --> S[Globally Unique]
              H --> T[Non-Internet Routable]
              H --> U[ISP Independent]
    
              L --> V[All Nodes FF02::1]
              L --> W[All Routers FF02::2]
              L --> X[Protocol Specific]
    
              M --> Y[Address Resolution]
              M --> Z[Neighbor Discovery]
              M --> AA[Duplicate Detection]
          ```


  * **Classful Addressing**

    * Classful addressing is a technique used to partition the 32-bit ip address into diferent
      classes to make the allocation of IP addressed more sustematic dusring early days until
      CIDR come into the picture

      * **IP Address Classes**

        * **Class A Networks**
          - **Range**: 1.0.0.0 to 126.255.255.255  
          - **First Octet Range**: 1–126  
          - **Binary Pattern**: First bit is always 0  
          - **Default Subnet Mask**: 255.0.0.0  
          - **Network/Host Division**: 8 bits for network, 24 bits for host  
          
          Class A addresses are designed for large organizations requiring extensive IP address space. The first 8 bits (first octet) represent the network portion, while the remaining 24 bits represent the host portion. This allows for **126 possible networks** (2⁷ − 2) and approximately **16.7 million hosts per network** (2²⁴ − 2).
        
          **Example**:  
          In the IP address `10.50.120.7`, the network portion is `"10"` and the host portion is `"50.120.7"`.
        
        ---
        
        * **Class B Networks**
          - **Range**: 128.0.0.0 to 191.255.255.255  
          - **First Octet Range**: 128–191  
          - **Binary Pattern**: First two bits are 10  
          - **Default Subnet Mask**: 255.255.0.0  
          - **Network/Host Division**: 16 bits for network, 16 bits for host  
          
          Class B addresses are suitable for medium to large networks. The first 16 bits (two octets) identify the network, while the remaining 16 bits identify the host. This provides **16,384 possible networks** (2¹⁴) and **65,534 hosts per network** (2¹⁶ − 2).
          
          **Example**:  
          In the IP address `172.16.55.13`, the network portion is `"172.16"` and the host portion is `"55.13"`.
        
        ---
        
        * **Class C Networks**

          - **Range**: 192.0.0.0 to 223.255.255.255  
          - **First Octet Range**: 192–223  
          - **Binary Pattern**: First three bits are 110  
          - **Default Subnet Mask**: 255.255.255.0  
          - **Network/Host Division**: 24 bits for network, 8 bits for host  
          
          Class C addresses are designed for smaller networks and local area networks. The first 24 bits (three octets) represent the network portion, while the last 8 bits represent the host portion. This allows for **2,097,152 possible networks** (2²¹) and **254 hosts per network** (2⁸ − 2).
          
          **Example**:  
          In the IP address `192.168.1.1`, the network portion is `"192.168.1"` and the host portion is `"1"`.
        
        ---
        
        * **Class D Networks**

          - **Range**: 224.0.0.0 to 239.255.255.255  
          - **First Octet Range**: 224–239  
          - **Binary Pattern**: First four bits are 1110  
          - **Purpose**: Reserved for multicasting  
          
          Class D addresses are used for multicast traffic, allowing data to be sent to multiple devices simultaneously. These addresses **do not have a traditional network/host division** and **do not use subnet masks**.
        
        ---
        
        * **Class E Networks**

          - **Range**: 240.0.0.0 to 255.255.255.255  
          - **First Octet Range**: 240–255  
          - **Binary Pattern**: First four bits are 1111  
          - **Purpose**: Reserved for experimental and research purposes  
          
          Class E addresses are reserved for future or experimental use and are **not commonly used in typical network configurations.

        ---
  

  * **Subnet Addressing**

    * Subnets are nothing but subnetworks or we can say that it is a collection of small networks
      connected to the main network


    ```mermaid
    flowchart TD
        A(Internet) e1@== All traffic to site border router ====> B(Site Border Router<br/>IP: 192.168.x.x)
        e1@{ animate: true }
    
        B e2@== IP Type: 192.168.1.x ====> C(Subrouter 1<br/>IP: 192.168.1.x)
        e2@{ animate: true }
    
        B e3@== IP Type: 192.168.2.x ====> D(Subrouter 2<br/>IP: 192.168.2.x)
        e3@{ animate: true }
    
        C e4@== 192.168.1.10 ====> E(Device 1A<br/>IP: 192.168.1.10)
        e4@{ animate: true }
    
        C e5@== 192.168.1.11 ====> F(Device 1B<br/>IP: 192.168.1.11)
        e5@{ animate: true }
    
        D e6@== 192.168.2.10 ====> G(Device 2A<br/>IP: 192.168.2.10)
        e6@{ animate: true }
    
        D e7@== 192.168.2.11 ====> H(Device 2B<br/>IP: 192.168.2.11)
        e7@{ animate: true }
    ```

  * **Subnet Masks**

    * Subnet mask is the process of assigning bits in network to determine the flow of data in
      network and sub-network. Masks are used byy routers and hosts to determine where the network
      and sub-network portion od an ip address ends and the host part begins


    ```text
    br-d94d0bd70fd7:
        inet 172.19.0.1  netmask 255.255.0.0  broadcast 172.19.255.255

    docker0:
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255

    lo:
        inet 127.0.0.1  netmask 255.0.0.0

    wlo1:
        inet 192.168.2.3  netmask 255.255.255.0  broadcast 192.168.2.255

    ```

    * In wlo1(i.e wlan or wifi) has netmask 255.255.255.0 when mean there are 254 possible
      connections you can have with your routers netmask also told us how many possibble
      hosts are possile per network and also also signify that first 3 octets are static
      and cant be changes i.e 192.168.2.x with netmask 255.255.255.0


        * 192.168.2.3 ------> 11000000.10101000.00100000.00000101

        * 255.255.255.0 -------> 11111111.11111111.11111111.00000000


    * In the given netmask the last octet is a part of host bits


    * Ref: https://www.spiceworks.com/tech/networking/articles/what-is-subnet-mask/


  * **Variable-Length Subnet Masks(VLSM)**

    ```mermaid
    graph TD
        A["Original Network: 192.168.1.0/24<br/>📊 Total Addresses: 256<br/>🖥️ Usable Hosts: 254<br/>🔢 Subnet Mask: 255.255.255.0<br/>📈 Binary: 11111111.11111111.11111111.00000000"] --> B["Subnetting Process<br/>💡 Borrowing bits from host portion<br/>🎯 To create multiple smaller networks"]
    
        B --> C{"How many subnets needed?<br/>📝 Formula: 2^n ≥ required subnets<br/>⚡ n = bits borrowed from host"}
    
        C -->|"Need 2 Subnets<br/>👉 Borrow 1 bit<br/>📐 2^1 = 2 subnets"| D["Subnet Mask: /25<br/>🔢 255.255.255.128<br/>📊 Binary: 11111111.11111111.11111111.10000000<br/>🖥️ Hosts per subnet: 2^7-2 = 126"]
    
        C -->|"Need 4 Subnets<br/>👉 Borrow 2 bits<br/>📐 2^2 = 4 subnets"| E["Subnet Mask: /26<br/>🔢 255.255.255.192<br/>📊 Binary: 11111111.11111111.11111111.11000000<br/>🖥️ Hosts per subnet: 2^6-2 = 62"]
    
        C -->|"Need 8 Subnets<br/>👉 Borrow 3 bits<br/>📐 2^3 = 8 subnets"| F["Subnet Mask: /27<br/>🔢 255.255.255.224<br/>📊 Binary: 11111111.11111111.11111111.11100000<br/>🖥️ Hosts per subnet: 2^5-2 = 30"]
    
        D --> G["Subnet 0: 192.168.1.0/25<br/>📍 Network ID: 192.168.1.0<br/>🏠 First Host: 192.168.1.1<br/>🏠 Last Host: 192.168.1.126<br/>📡 Broadcast: 192.168.1.127<br/>📊 Block Size: 128"]
    
        D --> H["Subnet 1: 192.168.1.128/25<br/>📍 Network ID: 192.168.1.128<br/>🏠 First Host: 192.168.1.129<br/>🏠 Last Host: 192.168.1.254<br/>📡 Broadcast: 192.168.1.255<br/>📊 Block Size: 128"]
    
        E --> I["Subnet 0: 192.168.1.0/26<br/>📍 Network: 192.168.1.0<br/>🏠 Range: 192.168.1.1-62<br/>📡 Broadcast: 192.168.1.63<br/>📊 Block Size: 64"]
    
        E --> J["Subnet 1: 192.168.1.64/26<br/>📍 Network: 192.168.1.64<br/>🏠 Range: 192.168.1.65-126<br/>📡 Broadcast: 192.168.1.127<br/>📊 Block Size: 64"]
    
        E --> K["Subnet 2: 192.168.1.128/26<br/>📍 Network: 192.168.1.128<br/>🏠 Range: 192.168.1.129-190<br/>📡 Broadcast: 192.168.1.191<br/>📊 Block Size: 64"]
    
        E --> L["Subnet 3: 192.168.1.192/26<br/>📍 Network: 192.168.1.192<br/>🏠 Range: 192.168.1.193-254<br/>📡 Broadcast: 192.168.1.255<br/>📊 Block Size: 64"]
    
        F --> M["8 Subnets (/27) Details:<br/>📊 Block Size: 32 addresses each<br/>🖥️ Usable Hosts: 30 per subnet<br/><br/>Subnet 0: 192.168.1.0/27 (1-30)<br/>Subnet 1: 192.168.1.32/27 (33-62)<br/>Subnet 2: 192.168.1.64/27 (65-94)<br/>Subnet 3: 192.168.1.96/27 (97-126)<br/>Subnet 4: 192.168.1.128/27 (129-158)<br/>Subnet 5: 192.168.1.160/27 (161-190)<br/>Subnet 6: 192.168.1.192/27 (193-222)<br/>Subnet 7: 192.168.1.224/27 (225-254)"]
    
        N["📚 Key Concepts:<br/>🔹 Network ID: First address (all host bits = 0)<br/>🔹 Broadcast: Last address (all host bits = 1)<br/>🔹 Usable Hosts: Total - 2 (exclude network & broadcast)<br/>🔹 Block Size: 256 ÷ 2^(borrowed bits)<br/>🔹 CIDR: /24 = 24 network bits, 8 host bits"]
    ```

    * VLSM are custom subnets created in network to route traffic efficently.


  * **Broadcast Addresses**

    * The subnet broadcast address is constructed by inverting the subnet mask

      * i.e converting all modifiable bits from 0 to 1

        * **Example**

          * `192.168.2.13` have net mask `255.255.255.0` and the binary format representation wll be
            `11111111.11111111.11111111.00000000` and the broad cast ip will be 192.168.1.255 the last
             octet is modifiable there all 0 bits are converted into 1

  * **IPv6 Address Scopes**

    * IPv6 has primarily 2 scope first one is link-local scope and another is global scope

      * **Link-Local Scope**

        * Link-Local addresses are valid only within a single network segment (link); the can't
          be routed beyond local link.

        * Usage: Local communication b/w nodes on same network segment and also used in essential
          network functions such as `Neighbour Discovery Protocol (NDP)` and address configuration

        * Note: Routers do not forward packets with local-link ipv6 address

        ```text
        inet6 fe80::4de:61ce:b090:e855  prefixlen 64  scopeid 0x20<link>
        ```

      * **Global Scope**

        * Global address are unique across the entire internet and are routable globally, and
          used in end-to-end communication across different networks including public internet

        ```text
        inet6 2402:e280:3e14:116:c70f:7320:a921:d9c9  prefixlen 64  scopeid 0x0<global>
        ```

  * **Classless Inter Domain  Routing**

    * Classless Inter Domain Routing(CIDR) is a method for allocating ip address and managing
      ip routing efficiently.

    * Following are core principle of CIDR

      1) **VLSM**

         * Instead of fixed 8, 16, or 24-bit network portions, CIDR allows any length from 1 to 32 bits:

            * Traditional Classful:

              ```text
              Class A: /8  (255.0.0.0)
              Class B: /16 (255.255.0.0)
              Class C: /24 (255.255.255.0)
              ```

            * CIDR Flexibility:

              ```text
              /8, /9, /10, /11, /12, /13, /14, /15, /16, /17, /18, /19, /20, 
              /21, /22, /23, /24, /25, /26, /27, /28, /29, /30, /31, /32
              ```

      2) **Prefix-Length Notation**

         * CIDR uses slash notation to indicate of network bits

           i.e 192.168.1.0/24 -> 24 its are for network and 8 bits are for host


      3) **Hierarchical Allocation**

         * CIDR enables hierarchical address distribution:

           ```text
           IANA (Internet Assigned Numbers Authority)
             ↓
           Regional Internet Registries (RIRs)
             ↓
           Local Internet Registries (LIRs) / ISPs
             ↓
           Organizations
             ↓
           End Users
          ```
          
       4) **Route Aggregation**

          * Multiple smaller networks can be combined into larger routing announcements:

            * Individual Routes:

              ```text
              192.168.0.0/24
              192.168.1.0/24
              192.168.2.0/24
              192.168.3.0/24
              ```

            * Aggregated Route:

              ```text
              192.168.0.0/22 (covers all four /24 networks)
              ```
-----------------------------------------------------------------------------------------------------------------------------------------
# IPv4 and IPv6 Special Use Address Tables

## IPv4 Special Use Addresses

| Prefix | Special Use |
|--------|-------------|
| 0.0.0.0/8 | Hosts on the local network. May be used only as a source IP address. |
| 10.0.0.0/8 | Address for private networks (intranets). Such addresses never appear on the public Internet. |
| 127.0.0.0/8 | Internet host loopback addresses (same computer). Typically only 127.0.0.1 is used. |
| 169.254.0.0/16 | "Link-local" addresses—used only on a single link and generally assigned automatically. |
| 172.16.0.0/12 | Address for private networks (intranets). Such addresses never appear on the public Internet. |
| 192.0.0.0/24 | IETF protocol assignments (IANA reserved). |
| 192.0.2.0/24 | TEST-NET-1 addresses approved for use in documentation. Such addresses never appear on the public Internet. |
| 192.88.99.0/24 | Used for 6to4 relays (anycast addresses). |
| 192.168.0.0/16 | Address for private networks (intranets). Such addresses never appear on the public Internet. |
| 198.18.0.0/15 | Used for benchmarks and performance testing. |
| 198.51.100.0/24 | TEST-NET-2. Approved for use in documentation. |
| 203.0.113.0/24 | TEST-NET-3. Approved for use in documentation. |
| 224.0.0.0/4 | IPv4 multicast addresses (formerly class D); used only as destination addresses. |
| 240.0.0.0/4 | Reserved space (formerly class E), except 255.255.255.255. |
| 255.255.255.255/32 | Local network (limited) broadcast address. |

## IPv6 Special Use Addresses

| Prefix | Special Use |
|--------|-------------|
| ::/0 | Default route entry. Not used for addressing. |
| ::/128 | The unspecified address; may be used as a source IP address. |
| ::1/128 | The IPv6 host loopback address; not used in datagrams sent outside the local host. |
| ::ffff:0:0/96 | IPv4-mapped addresses. Such addresses never appear in packet headers. For internal host use only. |
| ::{ipv4-address}/96 | IPv4-compatible addresses. Deprecated; not to be used. |
| 2001::/32 | Teredo addresses. |
| 2001:10::/28 | Overlay Routable Cryptographic Hash Identifiers. Such addresses never appear on the public Internet. |
| 2001:db8::/32 | Address range used for documentation and for examples. Such addresses never appear on the public Internet. |
| 2002::/16 | 6to4 addresses of 6to4 tunnel relays. |
| 3ffe::/16 | Used by 6bone experiments. Deprecated; not to be used. |
| 5f00::/16 | Used by 6bone experiments. Deprecated; not to be used. |
| fc00::/7 | Unique, local unicast addresses; not used on the global Internet. |
| fe80::/10 | Link-local unicast addresses. |
| ff00::/8 | IPv6 multicast addresses; used only as destination addresses. |

------------------------------------------------------------------------------------------------------------------------------------------

