# Hexagonal Architecture

  * A pattern designed for loosely coupled application that are connected via ports and
    adapters.

  * In this pattern, the consumer opens the application at a port via an adapter, and the
    output is sent through a port to an adapter

  * **Actors**

    * Entities that interact with the application, which can be humans, other appications
      or hardware devices

      * There are two type of actors

        * **Driver(Primary) Actors** : Initiate communication with application

        * **Driven(Secondary) Actors** : Responds to the reuqest

  * **Ports**

    * Interfaces that define interactions b/w actors and application.

    * driver ports expose actions that can peform, while driven ports are used for reciving
      data  or commands from application
        

  * **Diagram**

    ![Hexa Arch](../assets/HexaArch.png)

  * **Adapters**

    * **Driver Adapter** : This `adapter` transform input from user actors into a format that
      the application can understand. It acts as bridge b/w user interface. It acts as a bridge
      b/w the user interface and the core logic

    * **Driven Adapter** : This `adapter` transform data from the application into a format
      suitable for external systems, such as database quaries or API calls

# Load Balancing

  * **Server-Side Load Balacing**

    * In server-side load balancing a client will make RPC call to the load-balacer and
      it will distribute the request among the available services


      ```mermaid
      stateDiagram-v2
          state "Server-Side Load Balancing" as ServerLB {
              [*] --> Client
              Client --> LoadBalancer : RPC Request
              LoadBalancer --> ServiceInstance1 : Distribute
              LoadBalancer --> ServiceInstance2 : Distribute
              LoadBalancer --> ServiceInstance3 : Distribute
          }
    
          state "Client-Side Load Balancing" as ClientLB {
              [*] --> Client
              Client --> ServiceInstance1 : Direct RPC
              Client --> ServiceInstance2 : Direct RPC
              Client --> ServiceInstance3 : Direct RPC
              ServiceInstance1 --> Client : Load Report
              ServiceInstance2 --> Client : Load Report
              ServiceInstance3 --> Client : Load Report
          }
      ```
