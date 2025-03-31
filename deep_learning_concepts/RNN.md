# `RNN(Recurrent Neural Network)`

  * **Introduction**

    * Recurrent Neural Networks (RNNs) are type of neural network architecture which is mainly used to
      detect patterns in sequence data. such as handwriting, genomes, text or numerical time series
      i.e stock market or sensors


  * Before further taking lets discuss abount MLP vs RNN and what seperates them


| **Feature**              | **MLP (Multilayer Perceptron)**                           | **RNN (Recurrent Neural Network)**                             |
|--------------------------|-----------------------------------------------------------|----------------------------------------------------------------|
| **Architecture**          | Feedforward fully connected layers                        | Cyclic connections with hidden states                          |
| **Data Handling**         | Fixed-size input vectors                                  | Sequential/temporal data                                       |
| **Connectivity**          | Unidirectional (input → hidden → output)                  | Looped connections (time-unfolded)                              |
| **Memory**                | No internal memory                                        | Maintains hidden state memory                                   |
| **Parameter Sharing**     | No temporal parameter sharing                             | Shares parameters across time steps                             |
| **Input Structure**       | Independent data points                                   | Time-dependent sequences                                       |
| **Common Use Cases**      | Image classification, Regression                          | Time series, NLP, Speech recognition                           |
| **Typical Layers**        | Dense layers with activation functions                    | LSTM/GRU cells with recurrent layers                            |
| **Processing Style**      | Parallel processing                                       | Sequential processing                                           |
| **Handling Sequences**    | Requires fixed window size                                | Variable length sequences                                       |


  * MLP

    ```mermaid
    graph LR
       I1((Input 1)) --> H1((Hidden 1))
       I2((Input 2)) --> H1
       I3((Input 3)) --> H1
       H1 --> O1((Output 1))
       H1 --> O2((Output 2))
    ```

  * RNN

    ```mermaid
    graph LR
       Xt((Input t)) --> Ht((Hidden t))
       Ht --> Ot((Output t))
       Ht --> Ht+1((Hidden t+1))
       Xt+1((Input t+1)) --> Ht+1
       Ht+1 --> Ot+1((Output t+1))
       Ht+1 -.-> Ht+2((...))
    ```

    
    * $$H_t = \phi_h(X_t W_{xh} + H_{t-1} W_{hh} + b_h)$$
    
