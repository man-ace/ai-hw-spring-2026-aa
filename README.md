Adversarial Setup Constraints
To provide a uniform evaluation framework, the mathematical boundaries for creating the
adversarial noise vectors were configured as follows:

● Maximum Perturbation Bound (Epsilon / ε): 0.3 (Dictates the maximum pixel value
alteration allowed, preserving human readability).

● Iterative Step Modifier (Alpha / α): 0.01 (The incremental rate of change applied to the
image pixel values during optimization loops).

● Iteration Capacity (Steps): 40 (Total optimization iterations performed for multi-step
frameworks).

● Decay Coefficient: 1.0 (The momentum preservation factor utilized exclusively inside the
MIFGSM algorithm).


Fast Gradient Sign Method (FGSM)

● Algorithmic Approach: A single-step, non-iterative attack vector. It calculates the loss
gradient with respect to the input image coordinates, determines the direction of the
gradient using a sign function, and introduces a one-time pixel displacement scaled
exactly by Epsilon.

● Result Breakdown: Successfully disrupted 3,543 of the 9,898 correct baseline samples,
mapping a final adversarial breakthrough rate of 35.80%. This confirms that even
single-step noise vectors can bypass primitive convolutional borders on over a third of test
samples.


Momentum Fast Gradient Sign Method (MIFGSM)

● Algorithmic Approach: An iterative attack spanning 40 steps that integrates a velocity
vector (momentum) into the gradient computation loops. By scaling historical gradient
states by the decay coefficient and adding a normalized step, it stabilizes optimization
direction and prevents getting trapped in local extrema.

● Result Breakdown: Completely bypassed almost all defensive limits within the
convolutional filters, logging 9,878 successful overrides out of the 9,898 clean images to
yield a 99.80% failure rate in the model.


Projected Gradient Descent (PGD / IFGSM)

● Algorithmic Approach: A comprehensive iterative optimization framework. It initializes
by introducing a uniform random perturbation within the defined Epsilon boundaries. It
then carries out 40 progressive steps of gradient sign maximization, systematically
clamping the resulting image space back into the valid [0, 1] pixel value region and the
local Epsilon-ball.

● Result Breakdown: Successfully manipulated every single instance presented, creating
9,898 successful misclassifications out of 9,898 valid attempts. This yielded a definitive
100.00% attack success rate, exposing the absolute vulnerability of standard
convolutional boundaries to iterative pixel constraints.

Final result
| Adversarial Attack Strategy | Total Targeted Samples | Successful Adversarial Overrides | Final Successful Attack Rate |
| :--- | :--- | :--- | :--- |
| **Fast Gradient Sign Method (FGSM)** | 9,898 | 3,543 | 35.80% |
| **Momentum Fast Gradient Sign Method (MIFGSM)** | 9,898 | 9,878 | 99.80% |
| **Projected Gradient Descent (PGD / IFGSM)** | 9,898 | 9,898 | **100.00%** |
