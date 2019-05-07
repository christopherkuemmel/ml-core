# BEAM Search

## Idea

The key idea of *Beam Search* is to sample the most likely values for each time step and use them as input for the further.
Similar to [greedy search](../greedy-search/greedy-search.md) the *Beam Search* algorithm is commonly used in encoder decoder architectures.
However, the main difference is in not only using the most likey word, but the **B** most likely ones.
Based on those different parallel computations will be made to calculate the further best values with respect to the maximum probability of the prediction.

## Improvement

In comparison to [greedy search](../greedy-search/greedy-search.md) the beam search algorithm does not prefer common values since several likely will be selected for further calculations.

## Concept

1. Define the **Beam width:** ![](https://latex.codecogs.com/svg.latex?B=3)
   1. If you choose to define a large *B* you obtain better but slower results
   2. A small *B* will result worse but faster

<!-- Pick the most likely *B* values for the first timestep $\hat{y}^{<1>}$ -->
2. Pick the most likely *B* values for the first timestep ![](https://latex.codecogs.com/svg.latex?P(\hat{y}^{<1>}|x))

<!-- 3. Based on the first *B* values, pick the next *B* most likely ones $P(\hat{y}^{<2>}|x,\hat{y}^{<1>})$ -->
3. Based on the first *B* values, pick the next *B* most likely ones ![](https://latex.codecogs.com/svg.latex?P(\hat{y}^{<2>}|x,\hat{y}^{<1>}))
   
<!-- 4. $P(\hat{y}^{<1>}, \hat{y}^{<2>}|x) = P(\hat{y}^{<1>}|x)P(\hat{y}^{<2>}|x,\hat{y}^{<1>})$ (you have *B* copies of your network) -->
4. ![](https://latex.codecogs.com/svg.latex?P(\hat{y}^{<1>},\hat{y}^{<2>}|x)=P(\hat{y}^{<1>}|x)P(\hat{y}^{<2>}|x,\hat{y}^{<1>})$) (you have *B* copies of your network)

5. Repeat picking *B* values
   1. In each iteration only *B* values will propagate
   2. *B* values over all results

![BeamSearch](beam_search.svg) - [Reference](https://d2l.ai/chapter_recurrent-neural-networks/beam-search.html)

Refinement:

<!-- 1. $argmax_y=\prod^{T_y}_{t=1}{P(y^{<t>}|x,y^{<1>},...,y^{<t-1>})}$  -->
1. ![](https://latex.codecogs.com/svg.latex?argmax_y=\prod^{T_y}_{t=1}{P(y^{<t>}|x,y^{<1>},...,y^{<t-1>})})
   1. Prefers short predictions
   2. Rounding errors/ underflow
<!-- 2. $argmax_y=\sum^{T_y}_{t=1}{logP(y^{<t>}|x,y^{<1>},...,y^{<t-1>})}$  -->
3. ![](https://latex.codecogs.com/svg.latex?argmax_y=\sum^{T_y}_{t=1}{logP(y^{<t>}|x,y^{<1>},...,y^{<t-1>})})
   1. Insert log -> Sum of log
   2. Numerical more stable
   3. Prefers short predictions
<!-- 4. $\frac{1}{T^\alpha_y}\sum^{T_y}_{t=1}{logP(y^{<t>}|x,y^{<1>},...,y^{<t-1>})}$  -->
5. ![](https://latex.codecogs.com/svg.latex?\frac{1}{T^\alpha_y}\sum^{T_y}_{t=1}{logP(y^{<t>}|x,y^{<1>},...,y^{<t-1>})})
   <!-- 1. Where $\alpha=0.7$ (Normalisation factor) -->
   2. Where ![](https://latex.codecogs.com/svg.latex?\alpha=0.7) (normalization factor)

## Evaluation

<!-- Error Analysis: $P(y^{*}|x) vs. P(\hat{y}|x)$ -->
Error Analysis: ![](https://latex.codecogs.com/svg.latex?P(y^{*}|x)) vs. ![](https://latex.codecogs.com/svg.latex?P(\hat{y}|x))

* where ![](https://latex.codecogs.com/svg.latex?y^{*}): human prediction
* and ![](https://latex.codecogs.com/svg.latex?\hat{y}): machine prediction

**Case 1:**

![](https://latex.codecogs.com/svg.latex?P(y^{*}|x)) > ![](https://latex.codecogs.com/svg.latex?P(\hat{y}|x))

* Beam search is at faul -> change *B width*

**Case 2:**

![](https://latex.codecogs.com/svg.latex?P(y^{*}|x)) <= ![](https://latex.codecogs.com/svg.latex?P(\hat{y}|x))

* RNN is at fault -> change architecture

## Production

## References

1. [Dive into DeepLearning](https://d2l.ai/chapter_recurrent-neural-networks/beam-search.html)
2. [Beam Search — A Search Strategy](https://hackernoon.com/beam-search-a-search-strategy-5d92fb7817f)
