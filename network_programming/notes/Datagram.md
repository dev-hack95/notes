# `Datagram`

  * A datagram is a basic unit of information in the TCP/IP protocol suite. It is self
    contained and independent packet of data that carries sufficient information to be
    routed from source to destination therefore it don't require switch packets to route
    data

  * One of the important information about datagram is it maintain message boundries
    when more than one message sends in network it maintain boundries i.e a function
    return the data with the offset byte


  ```mermaid
  graph LR
    %% Left side - Application Writes
    subgraph "Application Writes to Network"
        direction TB
        WriteSection["Application Writes to\nNetwork"]
        
        subgraph WriteBoxes
            direction LR
            W3["W3"] --- W2["W2"] --- W1["W1 bytes"]
        end
        
        WriteText["Application invokes\n'write' function 3 times\nwith sizes W1, W2, W3"]
        
        subgraph WriteLower
            direction LR
            WL3["W3"] --- WL2["W2"] --- WL1["W1"]
        end
    end
    
    %% Middle boxes - Protocols
    Protocol1["Protocol That\nPreserves Message\nBoundaries"]
    Protocol2["Protocol That Does Not\nPreserve Message\nBoundaries"]
    
    %% Right side - Application Reads
    subgraph "Application Reads from Network"
        direction TB
        ReadSection["Application Reads from\nNetwork"]
        
        subgraph ReadBoxes
            direction LR
            R3["W3"] --- R2["W2"] --- R1["W1 bytes"]
        end
        
        ReadText["Application 'read'\nfunctions return same\nsize as corresponding\nwrites (W1, W2, W3)"]
        
        subgraph ReadLower
            direction LR
            RL1["R"] --- RL2["R"] --- RL3["R"] --- RL4["R"] --- RL5["R"] --- RL6["R"]
        end
        
        ReadLowerText["Application 'read' functions return\nhowever much application requests\n(e.g., 6 reads, R bytes each)"]
    end
    
    %% Connections
    WriteLower --> Protocol1
    Protocol1 --> ReadBoxes
    WriteLower --> Protocol2
    Protocol2 --> ReadLower

    %% Styling to make it more like the original
    classDef hidden fill:none,stroke:none
    class WriteSection,ReadSection hidden
  ```
