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

      * **Header Compression** : HTTP/2 employes a compression algorithum known as HPACK to reduce
        the size of header data transmitted between clients and servers.

        * **HPACK**

          * HPACK is a compression algorithum used in HTTP/2 to efficiently encode header fields.
             It was developed to address the growing issue of bandwisth usage and improved prformance
             in web communiations

             **Key Features of HPACK**

               * **Reduces Header Size** : HPACK can reduce the size of HTTP headers by over 30% on
                 average, which significiently decreases the amount of data transmitted over the
                 network. This reduction leads faster contenet delivery and improved peformance
                 for web applications

               * **Static and Dynamic Tables** : HPACK employs two types of tables to manage header
                 fields:

                 * **Static Table** : This is a predefined directory containing 61 commonly used
                   header fields and their defult values. For instances headers like `:method`,
                   `:scheme` and `path` are included in this table aloowing for efficient encoding

                 * **Dynamic Table** : This table is built during the session based on headers
                   that have been sent. It allows frequently used headers to be refrenced without
                   needing to resend them fully, further optimizing data transfer.

               * **Huffman Encoding** : HPACK uses huffman coding to compress header field values.
                 This method assigns shorter binary codes to more frequently used characters. Which
                 will reduces the overall size of the header fields being transmitted.


             **How It Works**

               * **Encoding Process**

                 1. When a client sends a request, it first checks the static table for any matching
                    headers.

                 2. If a match is found, it sends the index of that header insted of the full string

                 3. For new headers or those not found in static table, thay are added to the dynamic
                    table and encoded using huffman coding


               * **Decoding Process**

                 1. The server recives the compressed headers and uses the same static and dynamic
                    table to decode them.

                 2. It retrives vakues from these tables or decodes huffman-encoded strings back into
                    their original form.

        ```mermaid
        flowchart LR
            A[Client Request] -->|Sends Headers| B[HPACK Encoder]
            B -->|Encodes Headers| C[Static Table]
            B -->|Updates Dynamic Table| D[Dynamic Table]
            C -->|References Static Headers| E[Compressed Header]
            D -->|Stores New Headers| E
            E --> F[Send to Server]

            F -->|Receives Compressed Headers| G[HPACK Decoder]
            G -->|Decodes Headers| H[Static Table]
            G -->|Updates Dynamic Table| I[Dynamic Table]
            H -->|Retrieves Static Headers| J[Decoded Header]
            I -->|Retrieves Dynamic Headers| J
            J --> K[Client Response]
        ```
