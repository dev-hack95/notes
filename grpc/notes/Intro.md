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
