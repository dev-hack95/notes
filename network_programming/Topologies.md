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
      A((Node 1)) ------ B((Node 2))
  ```

