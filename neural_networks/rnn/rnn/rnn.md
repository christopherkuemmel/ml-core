# RNN - Recurrent Neural Networks

## Idea

Recurrent Neural Networks are especially useful when it comes to modelling sequences, like text, audio or video.
Similar to *standard* Neural Networks those process inputs and return the desired output(s) with the difference in sharing hidden states among forward and backward propagation.
Activations between timesteps are shared and therefore enable classification through time.
However, only previous steps are considered.
Future information is not available.

## Improvement

* Different in- and output sizes are possible
* Sharing features
  * Across different positions (e.g. in text)
* Sequence modelling

## Concept

### Calculus

**Forward propagation:**

* Activations are passed through states/ timesteps
* Often *tanh* as activation
  
<!-- $a^{<i>} = g_i (W_{aa} a^{<i-1>} + W_{ax} X^{<i>} + b_a)$ -->
![](https://latex.codecogs.com/svg.latex?a^{<i>}=g_i(W_{aa}a^{<i-1>}+W_{ax}X^{<i>}+b_a))

<!-- $\hat{y}^{<i>} =  g_i (W_{ya} a^i + b_y)$ -->
![](https://latex.codecogs.com/svg.latex?\hat{y}^{<i>}=g_i(W_{ya}a^i+b_y))

simplifies to

<!-- $a^{<i>} = g_i (W_a [a^{<i-1>}, X^{<i>}] + b_a)$ -->
![](https://latex.codecogs.com/svg.latex?a^{<i>}=g_i(W_a[a^{<i-1>},X^{<i>}]+b_a))

<!-- $\hat{y}^{<i>} =  g_i (W_{y} a^i + b_y)$ -->
![](https://latex.codecogs.com/svg.latex?\hat{y}^{<i>}=g_i(W_{y}a^i+b_y))

where

<!-- $W_a = concat((W_{aa}, W_{ax}), axis=1)$ -->
![](https://latex.codecogs.com/svg.latex?W_a=concat((W_{aa},W_{ax}),axis=1))

<!-- $[a^{<i-1>}, X^{<i>}] = concat((a^{<i-1>}, X^{<i>}), axis=0)$  -->
![](https://latex.codecogs.com/svg.latex?[a^{<i-1>},X^{<i>}]=concat((a^{<i-1>},X^{<i>}),axis=0))

*Notes on the notation:*

<!-- * $W_{ax}$ -->
* ![](https://latex.codecogs.com/svg.latex?W_{ax})
  * *a* is defined to describe the value calculated by this matrix
  * *x* is defined to describe the value which the matrix is multiplied by 

**Backward propagation:**

* Individual loss foreach timestep
* Summary over all timesteps

<!-- $L(\hat{y}, y) = \sum_{t=1}^{T_y} L^{<t>}(\hat{y}^{<t>}, y^{<t>})$ -->
![](https://latex.codecogs.com/svg.latex?L(\hat{y},y)=\sum_{t=1}^{T_y}L^{<t>}(\hat{y}^{<t>},y^{<t>}))

### Architectures

![rnn-architectures](rnn-architectures.jpg) - [Reference](https://karpathy.github.io/2015/05/21/rnn-effectiveness/)

#### One-to-One

* Classic ANN
* Image classification

#### Many-to-One

* Sentiment classification
  
#### One-to-Many

* Music generation
  
#### Many-to-Many

* Named-Entity Recognition
* Machine translation (splitted in encoder-decoder)
* Video classification

#### BiRNN

*Bidirectional RNNs* consider the whole input from two directions.
The benefit is that not only previous information are considered but also following.
However, this comes with the cost of having the whole sequence at computation time.
Real-time translation is therefore more complex.

![BiRNN](birnn.png) - [Reference](https://towardsdatascience.com/understanding-bidirectional-rnn-in-pytorch-5bd25a5dd66)

<!-- $\hat{y}^{<i>} =  g_i (W_{y} [\overrightarrow{a}^i, \overleftarrow{a}^i] + b_y)$ -->
![](https://latex.codecogs.com/svg.latex?\hat{y}^{<i>}=g_i(W_{y}[\overrightarrow{a}^i,\overleftarrow{a}^i]+b_y))

#### Deep RNN

*Deep RNNs* are simply on top stacked RNNs, which will use temporal information as inputs.
Usually you choose a small amount of layers, because of backpropagation through time there is a very large computational effort to compute stacked RNNs.
Often Deep RNNs are combined with an classic linear layer or deep net as output layers.

### Problems

* Long-term dependencies are hard to compute
* Vanishing gradients are a problem, since backpropagation is computed * timestep
* For exploding gradients, *gradient clipping* is a common used practice

## Evaluation

## Production

## References

1. [Karpathy - The Unreasonable Effectiveness of Recurrent Neural Networks](https://karpathy.github.io/2015/05/21/rnn-effectiveness/)
2. [Introduction RNN](https://medium.com/explore-artificial-intelligence/an-introduction-to-recurrent-neural-networks-72c97bf0912)
3. [Animated RNN](https://towardsdatascience.com/animated-rnn-lstm-and-gru-ef124d06cf45)
