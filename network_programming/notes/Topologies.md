# Network Topologies

  * Network topology defines the structure of a network, including how devices(nodes) are interconnectd

  * **Point-to-Point**

    * **Description**

      * Point-to-point topology is the simplest form of network topology where two nodes are directly connected by a dedicated link.
        This type can be implemented using wired connections (like a cable) or wireless connections (like Bluetooth).

      **Advantages**

        * **Simplicity** : Easy to set up and manage

        * **High Peformance** : Provides high-speed communication as there is no competition for bandwidth.

        * **Cost-Effective** : Requires minimal hardware.

      **Disadvantages**

        * **Scalability** : Limited to only two devices; not suitable for larger networks.
        * **Reliability** : If link failed communication is entirely disrupted

      **When to Use**

        * Ideal for scenarios requiring direct communication b/w two devices, such as connection a computer to a printer or establishing a
          dedicated WAN link b/w two sites.

  ```mermaid
  graph LR
    A((Node 1)) <------> B((Node 2))
  ```

  * **Bus Topology**

    * In bus topology, all devices share a single communication line known as the bus. Each deviece is connetced to this central cable,
      which acts backbone of the network.

    **Advantages**

      * **Cost-Effective** : Requires less cabling than other topologies.
      * **Easy Installation** : Simple to set up and extend by adding new devices.

    **Disadvantages**

      * **Single Point of failure** : If the main bus cable fails, the entire network goes down.
      * **Troubleshotting Difficlties** : Identifying faults can be challing due to multiple connections on the bus.
      

    **When to use**

      * Bus topologirs was commenly used in early ethernet networks in small office environments due to its low cost and simplicity

      * Best suited fro small networks where budget constraints are significant and peformance demands are low

  ```mermaid
  graph LR
      A[Main Cable] --- B((Device 1))
      A --- C((Device 2))
      A --- D((Device 3))
  ```

  * **Star Topology**

    * Star topology feature a central hub or switch to which all nodes are connected. Data transmitted b/w nodes passes through this central device

    **Advantages**

      * **Easy Troubleshotting and Management** : Centralizses control makes it easy to identify faults.

      * **Isolation of Devices** : Failure of one devicec does not affect others.

    **Disadvantages**

      * **Central Point of Failure** : If the hub fails, the entire network becomes inoperable

      * **Higher cabling Costs** : Requires more cables than bus topology due to indicidual connections

    **When to Use**

      * Most modern networks use start topology due to its relability and ease of management. Ideal for medium to large networks

  ```mermaid
  graph TB
      Hub((Hub/Switch)) --> A((Device 1))
      Hub --> B((Device 2))
      Hub --> C((Device 3))
  ```

  * **Ring Topology**

    * In ring topology, each node connects to exactly two other nodes, forming a circular pathway for data transmission. Data travels around the ring
      until it reaches its destination. It is a closed loop in which data travels in a single direction


    **Advantages**

      * **Predictable Performance** : Data packets travel in one direction, reducing collisions.

      * **Equal Access for All Nodes** : Each node gets a chance to transmit data based on token passing.

    **Disadvantages**

      * **Single Point of Failure Risk**: If one node or connection fails, it can disrupt the entire network unless dual-ring configurations are used.

      * **Difficult to Add/Remove Nodes**: Changes can disrupt the network operation.
    
