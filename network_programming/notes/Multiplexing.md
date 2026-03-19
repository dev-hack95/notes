# `Multiplexing(muxing)`

  * A infomration i.e packets coming from different sources or senders can be mixed
    together and can be pulled apart later which is called multiplexing, and this data
    can be moved on different switches to recieve at their destination

  * When packets are received at packet switch they are normally stored in **buffer memory**
    or **queue** and processed based on FIFO(First Input First Output)

  * FIFO buffer management and on-demand scheduling are easly combined to implement
    stastical multiplexing, modern network protocol uses Frame realy to talk with
    each other 


  * **Frame Realy**

    * Its is a Wide Area Network(WAN) technology that operates primarily at the physical and
      data link layers of the OSI model


    * **Key Characters of Frame Realy**

      * **Packet Switching**: Frame realy transmits data in varible-length units called
        frames, Unlike x.25 it does not peform error correction withing network. If the
        frame is corrupted, it is simply dropped, and error recovery is handled by the
        endpoints.

      * **Virtual Circuits**: Frame relay uses virtual circuits identified by data link
        connection identifiers(DLCIs). These virtual circuits can ve permanent(PVCs) or
        switched (SVCs), allowing multiple logical connections over a single physical link

      * **Efficiency and Speed**: By eliminating the overhead of error correction and
        retansmission within the network, frame realy achives higher throughputs


    * Devices attached to frame relay falles into two categories one is DTE(data terminal
      equipements) and DCE(Data circuit-terminating equipments), DTE can be computers,
      routes ..etc and DCE can be Frame Relay switches and Modems

    * **Virtual Circuits**

      * **SVC (Switched Virtual Circuits)**

        * Switched Virtual Circuits(SVCs) are temporary connections used in situations
          requring only sporadic data transfer b/w DTE devices across frame relay

          * **Call Setup** : The virtual circuit b/w two frame realy DTE devices is
            established

          * **Data Transfer** : Data is transmitted b/w DTE devices over virtual
            circuit

          * **Idle** : The connection b/w DTE devices is still active, but no data is
            transferred. If an SVC remains in an idle state for a defined period of
            time, the call can be terminated

          * **Call Termination** : The virtual circuits b/w DTE devices is terminated


      * **PVC (Permanent Virtual Circuits)**

        * Permanent virtual circuits (PVCs) are permanently established that arew used
          for frequent and consistent data transfers DTE devices across the frame relay
          network.

          * **Data Transfer** :  Data is transmitted b/w the DTE devices over virtual circuit.

          * **Idle** : The connection b/w DTE devices is active, but no data is transferred
