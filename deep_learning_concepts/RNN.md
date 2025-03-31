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

    *  **Hidden State and Input Representation**:

       - The hidden state at time step \( t \) is denoted as \( H_t \in \mathbb{R}^{n \times h} \).
       - The input at time step \( t \) is represented as \( X_t \in \mathbb{R}^{n \times d} \), where:
       - \( n \): Number of samples.
       - \( d \): Number of input features per sample.
       - \( h \): Number of hidden units.

    *  **Weight Matrices and Bias**:
       - **Input-to-Hidden Weight Matrix (\( W_{xh} \))**: \( W_{xh} \in \mathbb{R}^{d \times h} \), transforms the input to the hidden layer.
       - **Hidden-to-Hidden Weight Matrix (\( W_{hh} \))**: \( W_{hh} \in \mathbb{R}^{h \times h} \), connects the previous hidden state to the current one.
       - **Bias Term (\( b_h \))**: \( b_h \in \mathbb{R}^{1 \times h} \), added to the computation for flexibility.

    *  **Activation Function**:
       - The non-linear activation function \( \phi_h \) prepares gradients for backpropagation.
       - Common choices include:
       - Logistic sigmoid function.
       - Hyperbolic tangent (\( tanh \)).

       * **Mathematical Formulation**
    
         * $$H_t = \phi_h(X_t W_{xh} + H_{t-1} W_{hh} + b_h)$$
    
