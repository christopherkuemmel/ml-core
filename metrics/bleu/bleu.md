# BLEU

## Idea

BLEU (bilingual evaluation understudy) is an algorithm for evaluating the quality of text which has been machine-translated from one natural language to another. (Wikipedia)
Since there are possibly multiple good translations to one input, the question remains which is the best one.
BLEU provides a metric to compute a score wheter the generated words are in the references.

## Improvement

## Concept

In general the BLEU metric counts the generated words in the translation and compares them to the occurrences in the references.

* Generated words = machine output
* References = human labels

**Precision:**

<!-- $prec=\frac{\sum\:occurrences\:in\:ref}{\sum\#words\:of\:output}$ -->
![](https://latex.codecogs.com/gif.latex?prec%3D%5Cfrac%7B%5Csum%5C%3Aoccurrences%5C%3Ain%5C%3Aref%7D%7B%5Csum%5C%23words%5C%3Aof%5C%3Aoutput%7D)

**Modified precision:**

<!-- $mod\_prec=\frac{\sum\:clipped\:occurrences\:in\:ref}{\sum\#words\:of\:output}$ -->
![](https://latex.codecogs.com/gif.latex?mod%5C_prec%3D%5Cfrac%7B%5Csum%5C%3Aclipped%5C%3Aoccurrences%5C%3Ain%5C%3Aref%7D%7B%5Csum%5C%23words%5C%3Aof%5C%3Aoutput%7D)

![BLEU example](bleu-example.png)

<!-- $prec = \frac{7}{7} \qquad mod\_prec = \frac{2}{7}$ -->
![](https://latex.codecogs.com/gif.latex?prec%20%3D%20%5Cfrac%7B7%7D%7B7%7D%20%5Cqquad%20mod%5C_prec%20%3D%20%5Cfrac%7B2%7D%7B7%7D)

**N-gram precision:**

<!-- $P_n = \frac{\sum_{n-gram\in\hat{y}}count_{clip}(n-gram)}{\sum_{n-gram\in\hat{y}}count(n-gram)}$ -->
![](https://latex.codecogs.com/svg.latex?P_n=\frac{\sum_{n-gram\in\hat{y}}count_{clip}(n-gram)}{\sum_{n-gram\in\hat{y}}count(n-gram)})

* if machine translation equals one ref -> P = 1.0

**BLEU Score:**

<!-- * $P_n$ = n-gram
  * compute for $P_1, P_2, P_3, P_4$ -->
* ![](https://latex.codecogs.com/svg.latex?P_n) = n-gram
  * compute for ![](https://latex.codecogs.com/svg.latex?P_1,P_2,P_3,P_4)

<!-- $BP \exp(\frac{1}{4}\sum^4_{n=1}P_n)$ -->
![](https://latex.codecogs.com/svg.latex?BP\exp(\frac{1}{4}\sum^4_{n=1}P_n))

where 

<!-- $BP \{ {{1 \quad\:if\:out\:length>ref\:length}\atop{\exp(1-out\:length/ref\:length)}}$ -->
![](https://latex.codecogs.com/gif.latex?BP%20%5C%7B%20%7B%7B1%20%5Cquad%5C%3Aif%5C%3Aout%5C%3Alength%3Eref%5C%3Alength%7D%5Catop%7B%5Cexp%281-out%5C%3Alength/ref%5C%3Alength%29%7D%7D)

* BP: penalizes score for short sentences
  * short sentences tend to have good scores, because of the number of word occurrences
  
The BLEU metric is useful for NMT and Image Captioning, but bad for speech recognition (mostly one ground truth).

## Evaluation

## Production

## References

1. [BLEU Wikipedia](https://en.wikipedia.org/wiki/BLEU)
