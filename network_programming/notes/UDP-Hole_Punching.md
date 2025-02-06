# UDP-Hole Punching

  * UDP hole punching is a networking technique that enables two devices behind seperate NAT (Network Access Translations) routes to establish a direct
    connection with each other. This method is widely used in `peer-to-peer(P2P)` applications like online gaming and VoIP(Voice-over-IP) services to
    bypass the restrictions imposed by NAT.

  * **How UDP Hole Punching Works**

    1. **Initial contact with a `Third-Party Server`**

       * Both devices (e.g Client A and Client B) initiate communication with a third-party server (Server C) that is publicly accessible.

       * This step creates temporary NAT entries for both clients, which map their private IP addresses and ports to public IP address and ports

    2. **Exchange of Public Address**


       * The third-party server records the public IP address and port of each client as seen by their respective NATs.

       * It then shares this information with both clients so they can attempt direction communication.

    3. **Direct Communication Attempt**

       * Each client sends UDP packets to the other public IP address and port.

       * The NATS recognize these outbound packets and create new entries that allow incoming packets from the specifies external IP and port.

    4. **Hole Creation in NAT**

       * The first packet from each client may be dropped by the other's NAT.

       * However, subsequent packets succeed beacuse the NAT's now have entries permitting traffic from the other client's public address.

    5. **Keep-Alive Mechanism**

       * To maintain the connection, both clienrs periodically send keep-alive packets to prevent the NAt entries from expiring.


    ```mermaid
    graph TD
        ClientA(Client A):::client
        NATA(NAT A):::nat
        ServerC(Server C):::server
        NATB(NAT B):::nat
        ClientB(Client B):::client

        ClientA -- Sends UDP packet --> ServerC
        ClientB -- Sends UDP packet --> ServerC
        ServerC -- Shares Client B's public IP & port --> ClientA
        ServerC -- Shares Client A's public IP & port --> ClientB
        ClientA -- Sends packet to Client B's public IP & port --> NATB
        ClientB -- Sends packet to Client A's public IP & port --> NATA
        NATA -- Allows incoming packets from Client B --> ClientA
        NATB -- Allows incoming packets from Client A --> ClientB
        ClientA <--> ClientB[Direct communication established]

        classDef client fill:#f9f,stroke:#333,stroke-width:2px;
        classDef nat fill:#bbf,stroke:#333,stroke-width:2px;
        classDef server fill:#ffcc00,stroke:#333,stroke-width:2px;
    ```
