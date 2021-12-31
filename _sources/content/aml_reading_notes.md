# Notes for Adversarial Machine Learning Reading List

Notes to accompany [this AML reading list](https://nicholas.carlini.com/writing/2018/adversarial-machine-learning-reading-list.html).

## Preliminary Papers

### [Evasion Attacks Against Machine Learning at Test Time](https://arxiv.org/pdf/1708.06131.pdf)

**Important contributions:**  
Mimicry -- imitate features of known legitimate samples  
Kernel Density Estimation -- favor attacks in densely populated regions  

> classical performance evaluation techniques are not suitable to reliably assess the security of learning algorithms, i.e. the performance degradation caused by carefully crafted attacks.

This expands the definition of performance from accuracy metrics to runtime behavior.

> Proactive Protection
> 1. Find vulnerabilities
> 2. Investigate impact of corresponding attacks
> 3. Devise appropriate countermeasures

What other best practices can we borrow from traditional information security? A taxonomy for vulnerabilities, vulnerability management programs, semver and patching.

How reliably can we identify vulnerabilities without proof-of-concept exploits?

How often are countermeasures changes to the core model (hard/expensive) vs ETL steps (easier)?

> Two approaches have previously addressed security issues in learning. The min-max approach assumes the learner and attacker’s loss functions are antagonistic, which yields relatively simple optimization problems. A more general game-theoretic approach applies for non-antagonistic losses; e.g., a spam filter wants to accurately identify legitimate email while a spammer seeks to boost his spam’s appeal. Under certain conditions, such problems can be solved using a Nash equilibrium approach. Both approaches provide a secure counterpart to their respective learning problems; i.e., an optimal anticipatory classifier.

> Our approach is applicable to any classifier with a differentiable discriminant function.

> The adversary can transform attack points in the test data but must remain within a maximum distance of d<sub>max</sub> from the original attack sample. We use d<sub>max</sub> to simulate increasingly pessimistic attack scenarios by giving the adversary greater freedom to alter the data.

> The choice of a suitable distance measure is application specific.... should reflect the adversary's effort required to manipulate samples or the cost of these manipulations.

Creating a malicious sample is generally a non-linear optimization problem (gradient descent, Newton's method, BFGS, L-BFGS).

> Locally optimizing `g(x)` with gradient descent is particularly susceptible to failure due to the nature of a discriminant function.... may lead into unsupported regions.

We don't know how our adversarial sample will be classified in these regions.

> The attacker should favor attack points from densely populated regions of legitimate points.

![algo1.jpg](img/algo1.JPG)

> ... favors attack points that imitate features of known legitimate samples. In doing so, it reshapes the objective function and thereby biases the resulting gradient descent towards regions where the negative class is concentrated.... similar to _mimicry_ attacks in network intrusion detection.

> if `g` is non-differentiable or sufficiently smooth, one may still use the mimicry/KDE term of Eq 2 as a search heuristic.

> In discrete spaces, gradient approaches travel through infeasible portions of the feature space. In such cases, we need to find a feasible neighbor...

> Mimicry (lambda) may allow us to trade for a higher probably of evading the target classifier at the expense of a higher number of modifications.

> The PDF structure imposes natural constraints on attacks. Although it is difficult to remove an embedded object, it is rather easy to insert new objects.

I didn't know that; pretty interesting natural constraint.

> ... [in the limited knowledge case, we limited the number of samples] to demonstrate that even with a dataset as small as 20% of the original training set size, the adversary may be able to evade the targeted classifier with high reliability.

> It is worth noting that attacking a linear classifier amounts to always incrementing the value of the highest weighted feature until it reaches its upper bound. This continues with the next highest weighted non-bounded feature until termination.

> the RBF SVM provides a higher degree of security compared to linear SVMs.... interestingly, compared to SVMs, neural networks seem to be much more robust against the proposed evasion attack. This behavior can be explained by observing that the decision function in neural networks may be characterized by flat regions. Hence, the gradient descent algorithm sops after a few attack iterations for most malicious samples without being able to find a suitable attack.

> mimicking exhibits some beneficial aspects for the attacker, although the constraint on feature addition may make it difficult to properly mimic legitimate samples.

Canaries for alerting on illegitimate samples to detect ongoing adversarial tests?

> We believe the proposed attack formulation can be extended to classifiers with non-differentiable discriminant functions as well, such as decision trees and k-nearest neighbors by defining suitable search heuristics similar to our mimicry term.

### [Intriguing properties of neural networks](https://arxiv.org/pdf/1312.6199.pdf)

### [Explaining and Harnessing Adversarial Examples](https://arxiv.org/pdf/1412.6572.pdf)

## Attacks

### [The Limitations of Deep Learning in Adversarial Settings](https://arxiv.org/pdf/1511.07528.pdf)

### [DeepFool: a simple and accurate method to fool deep neural networks](https://arxiv.org/pdf/1511.04599.pdf)

### [Towards Evaluating the Robustness of Neural Networks](https://arxiv.org/pdf/1608.04644.pdf)
