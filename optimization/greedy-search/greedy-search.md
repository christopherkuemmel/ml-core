# Greedy Search

## Idea

Greedy search is an approach commonly used in encoder decoder architectures to pick the decoder in- and outputs.
By picking the most likely first value and using this as initial input for the decoder, the algorithm continues to pick the most likely values for each timestep.

## Improvement

In comparison to random sampling, greedy search does make use of the best values at each timestep.

## Concept

The greedy search algorithm always tries to pick the currently best value for each timestep and tries to maximize the probability for the predictions.

<!-- $max P(y^1, ..., y^{T_y} | x)$ -->
![](https://latex.codecogs.com/svg.latex?maxP(y^1,...,y^{T_y}|x))

### Problems

The greedy search algorithm may not result in the best probability, because the most likely first value does not always result in the best overall starting value.
Moreover, the algorithm tends to prefer common values.

## Evaluation

## Production

## References

1. [Greedy Search - Wikipedia](https://en.wikipedia.org/wiki/Greedy_algorithm)
