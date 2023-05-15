# Neural Networks - ELEC 320 Notes

This is the reviewing notes for ELEC 320: Neural Networks, which will sort by chapters. 

### Chapter 1: Introduction

- Advantages of ANNs:
  - Nonlinearity
  - Input-to-output mapping
  - Adaptivity
  - Evidential response
  - Contextual information
  - Fault tolerance
  - Massively parallel structure
  - Uniformity of analysis and design
  - Neurobiological analogy
- Basic structures:
  - Neurons in Brain:
    ![image-20230424130713002](C:\Users\10598\AppData\Roaming\Typora\typora-user-images\image-20230424130713002.png)
  - Neurons in ANNs:
    ![image-20230424130955309](C:\Users\10598\AppData\Roaming\Typora\typora-user-images\image-20230424130955309.png)
- Decision boundaries:
  - Underfitting: a machine learning model is not complex enough to accurately capture relationships between a dataset’s features and the target variable
  - Overfitting: a machine learning model is too closely fit to a limited set of data points and does not generalise well to unseen data points.
     ![image-20230424130511931](C:\Users\10598\AppData\Roaming\Typora\typora-user-images\image-20230424130511931.png)

### Chapter 2

- Mathematical aspects:
  ![image-20230424130955309](C:\Users\10598\AppData\Roaming\Typora\typora-user-images\image-20230424130955309.png)

  - $$
    \Large v_k = \sum _ {j = 1} ^ {m} w_{kj}x_{j} + b_k = W^TX + b_k
    $$

  - $$
    \Large y_k =  \phi(v_k)
    $$

- Types of activation functions

  - Threshold or Heaviside function:
    ![image-20230424132257930](C:\Users\10598\AppData\Roaming\Typora\typora-user-images\image-20230424132257930.png)
  - Piecewise linear function:
    ![image-20230424133011276](C:\Users\10598\AppData\Roaming\Typora\typora-user-images\image-20230424133011276.png)
  - Sigmoid and hyperbolic tangent functions
    ![image-20230424133034112](C:\Users\10598\AppData\Roaming\Typora\typora-user-images\image-20230424133034112.png)
  - Rectified linear unit (ReLU)：
    ![image-20230424133057226](C:\Users\10598\AppData\Roaming\Typora\typora-user-images\image-20230424133057226.png)

- Network architectures：

  -  Single-layer feedforward nets

    $$
    \Large y_k(x) = \phi(\sum _ {j=0} ^p w_{kj}x_j)
    $$
    ![image-20230424133149232](C:\Users\10598\AppData\Roaming\Typora\typora-user-images\image-20230424133149232.png)

  - Multi-layer feedforward nets:
    $$
    \Large y_k(x) = \phi (\sum _ {j=0} ^ {p_{hidden}} \phi(\sum _{i=0} ^{p_{input}} w_{ji} x_i) )
    $$
    ![image-20230424133211750](C:\Users\10598\AppData\Roaming\Typora\typora-user-images\image-20230424133211750.png)

  - Convolutional neural networks:
    ![image-20230424133230813](C:\Users\10598\AppData\Roaming\Typora\typora-user-images\image-20230424133230813.png)

  - Recurrent nets:

    $$
    \Large y_k(n) = y_k(x(n),n) = \phi (\sum _ {i=0} ^ {p_{input}} w_{ki}x_i(n) + \sum _ {j=0} ^ {p_{output}} w_{kj}y_j(n-1) )
    $$
    ![image-20230424133248779](C:\Users\10598\AppData\Roaming\Typora\typora-user-images\image-20230424133248779.png)

- To  measure similarity between two vectors
  $$X_i= [x_{i1},..,x_{ip}]$$ and $$X_j= [x_{j1},..,x_{jp}]$$

  - Euclidean distance:
    $$
    \Large d_{euc}(x_i,x_j) = ||x_i-x_j||_2 = (\sum _{k=1}^p(x_{ik}-x_{jk})^2)^{\frac{1}{2}}
    $$

  -  Inner or dot product
    $$
    \Large d_{euc}^2(x_i,x_j) = (x_i-x_j)^T(x_i-x_j) = 2 - 2X_i^TX_j
    $$
    ![image-20230424134722663](C:\Users\10598\AppData\Roaming\Typora\typora-user-images\image-20230424134722663.png)

  - Mahalanobis distance
    $$
    \Large d_{mah}(x_i,x_j) = \sqrt {\frac{(x_i - \mu)^T} {\sum _ {k=0} ^p E[(x_{jk}-\mu )(x_{jk}-\mu)^T] } }
    $$
    ![image-20230424140152313](C:\Users\10598\AppData\Roaming\Typora\typora-user-images\image-20230424140152313.png)

- Key for a NN:

  - Activation function, eg. Step, ReLU, sigmoid
  - NN architecture, eg. MLP, CNN, RNN
  - Error function

### Chapter 3

- Primary characteristics of a NN: learn from its environment, via adapting its structure in order to improve its performance

- Error-correction learning:

  - $e_k(n) = d_k(n) - y_k(n)$ for $k_{th}$ neuron

  - Objective: minimising the cost function $E(n)$, eg. the squared error $E(n) = \frac {1}{2} e_k^2(n)$ 

  - Weights adjustment: Delta or Widrow-Hoff rule:
    $$
    \large \Delta w_{kj}(n) = \eta e_k(n)x_j(n)
    $$

    $$
    \large w_{kj}(n+1) = w_{kj}(n)+\Delta w_{kj}(n)
    $$

    

- Memory-based learning:
  - Memory set $D_{train}$ to store pairs $(x_i, d_i)$ samples $x_i$ and known desired responses $d_i$. 
  - Weights adjustment:
    A new data $x^*$ is added with $d^* = argmin||x^*-x_i||, x_i \in D_{train} $ 

- Hebbian learning:

  - uses a time-dependent, highly local and strongly interactive mechanism to increase synaptic efficiency, Neurons that fire together wire together.

  - Weights adjustment - activity product rule:
    $$
    \large \Delta w_{kj}(n) = \eta y_k(n)x_j(n)
    $$
    

  - Problem: exponential growth, to solve with:
    $$
    \large \Delta w_{kj}(n) = \eta (y_k-\overline{y})(x_j-\overline{x})
    $$
    

- Competitive learning:
  - only one output neuron can be active, more suitable for classification problems
    ![image-20230424154141778](C:\Users\10598\AppData\Roaming\Typora\typora-user-images\image-20230424154141778.png)
  - Weights adjustment: 
    $\large \Delta w_{ki} = \eta (x_i - w_{ki}) $ if $k_{th}$ neuron wins, else $\large \Delta w_{ki} = 0$
  - Application: Clustering of input patterns
- Boltzmann Learning:
  - TODO
- Types of learning:
  - Supervised learning
  - Unsupervised learning 
  - Reinforcement learning

### Chapter 4

