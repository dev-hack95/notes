# `gRPC`
  * gPRC is an opensource remote procedure call framework that has some cool inbilt functionaties
    which are load-balancer, tracing fault tolerence and security

  * gRPC use protocl buffers i.e protobuffers/protobuf

  * gPRC works on HTTP/2 which enables the peformance with, `server-side push`, `multiplexing` and
    `header compression`

      * **server-side push** : server side push allows server to send resources to the client
      proactvely, without wating for the client to request them explicity. This feature is particul
      arly benefical when the server anicipates that the client will need certain resources after
      making an initial request.

        * **How it Works**

          a) **Connection Extablishment** : The client establish an HTTP/2 connection with the server
          
          b) **Initial Request** : The client request a resource(i.e HTML page)

          c) **Push Promises** : Upon recieving the request, the server identifies addition resources
             that the client will likely need.


      ```mermaid
      graph LR;
          A[Client Request] -->|Request for index.html| B[Server]
          B -->|Sends index.html| C[Client]
          B -->|Pushes styles.css| C
          B -->|Pushes script.js| C
          C -->|Uses index.html, styles.css, script.js| D[Render Page]
      ```

      * **Multiplexing** : Multiplexing in HTTP/2 allows streams of datat to be sent simultanously over
        a single tcp connection. This capability eliminates the `head-of-line blocking problem` present
        in HTTP/1. Where only one request could be processed at time per connection

        * **How it Works**

          a) Each stream is assigned a unique identifer and an carry multiple messages(requests and response)

          b) Data is broken down into frame, which are interleaved on connection. These frames are then
             reassembled on arrival


      ```mermaid
      graph LR;
          A[Client] -->|Sends Request 1| B[Server]
          A -->|Sends Request 2| B
          A -->|Sends Request 3| B
    
          B -->|Response 1 Stream 1| A
          B -->|Response 2 Stream 2| A
          B -->|Response 3 Stream 3| A

          subgraph Multiplexing Mechanism
              direction TB;
              Stream1[Stream 1: Data for Request 1]
              Stream2[Stream 2: Data for Request 2]
              Stream3[Stream 3: Data for Request 3]
        
              B --> Stream1
              B --> Stream2
              B --> Stream3
        
              Stream1 --> A
              Stream2 --> A
              Stream3 --> A
          end

          style A fill:#f9f,stroke:#333,stroke-width:2px;
          style B fill:#bbf,stroke:#333,stroke-width:2px;
          style Stream1 fill:#afa,stroke:#333,stroke-width:1px;
          style Stream2 fill:#afa,stroke:#333,stroke-width:1px;
          style Stream3 fill:#afa,stroke:#333,stroke-width:1px;
      ```
