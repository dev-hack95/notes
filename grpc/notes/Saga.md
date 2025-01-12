# `Saga`
  * A sequence algorithum based on triggered ordered, `saga pattern` is crucial architectureal design in
    microservices particularly for managing distributed transction across microservices. It allows the
    co-ordination of multiple microservices to ensure data consistency across different services without
    requiring tight coupling.

  * **Working of the Saga Pattern**

    1. **Local Tranction** : Each step in saga correspongs to the local transction with a microservice.
       when one steps completes, it publishes event to trigger next step.

       ```mermaid
       flowchart LR
           A@{ shape: stadium, label: "TASK_1"} --success--> B@{ shape: stadium, label: "TASK_2" }
           B@{ shape: stadium, label: "TASK_2"} --success--> C@{ shape: stadium, label: "TASK_3" }
           C@{ shape: stadium, label: "TASK_3"} --success--> D@{ shape: stadium, label: "TASK_4" }
          
           B --failure execute c1--> A
           C --failure execute c2--> B
           D --failure execute c3--> C
       ```

    2. **Compensation Transctions** : If steps failed, compensating transctions are executed to undo
       the effects of previous steps. i.e when `TASK_3` fails the C1 and C2 are executed and it will
       revert all changes in database.


    ```mermaid
    sequenceDiagram
        participant O as Order Service
        participant P as Payment Service
        participant S as Shipping Service

        O->>P: Create Order
        P-->>O: Order Created
        O->>S: Reserve Shipping
        S-->>O: Shipping Reserved
        O->>P: Process Payment
        alt Payment Successful
            P-->>O: Payment Processed
            O->>S: Ship Order
            S-->>O: Order Shipped
        else Payment Failed
            P-->>O: Payment Failed
            O->>S: Cancel Shipping
            S-->>O: Shipping Canceled
        end
    ```

  * **Options for Implementing Saga**

    1. Orchestration-Based Approach

       * Centralized control via an orchestrator that directs the flow of transctions.

       * Easier to manage but introduces a single point of failure

    2. Choregraphy-Based Approach

       * Decentralized where each service responds to events.

       * More resilient but harder to maanage comples workflows.

