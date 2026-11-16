# The connection to optimization
In mathematics and computer science, optimization means finding the input values that make a function as small (minimization) or as large (maximization) as possible.
# When training a neural network:
- **The Goal:** Find the best possible values for all the internal parameters (called weights) so the network makes accurate predictions.
- **The Metric:** The loss function ($L$) measures how "wrong" the network's predictions are. A high loss means the model is performing poorly; a loss close to zero means it is performing very well.
- **The Process:** Since we want the model to be as correct as possible, training is entirely about minimizing the loss function by tuning the weights iteratively.
# How to Read the Symbols and Formulas
Mathematical formulas can look intimidating, but they are just shorthand for logical steps. Here is how to decode every symbol from the text:
# The Loss Function
$$L(w_1, w_2, \dots, w_n)$$

- $L$: Represents the Loss function. It takes the weights as inputs and outputs a single number representing the model's total error.
- $w_1, w_2, \dots, w_n$: Represent the individual weights (parameters) inside the neural network. The subscript numbers ($1, 2, \dots, n$) indicate that there are $n$ distinct weights. In modern AI, $n$ can be in the billions!
# The Gradient Descent Update Rule
$$w_{\text{new}} = w_{\text{old}} - \text{learning\_rate} \times \frac{dL}{dw}$$

- $w_{\text{new}}$: The updated weight value for the next step of training.
- $w_{\text{old}}$: The current value of the weight before the update.
- $-$ (Minus sign): We subtract because the derivative tells us which way is uphill. To minimize the loss, we want to go downhill, so we move in the opposite direction of the slope.
- $\text{learning\_rate}$: A scaling factor (hyperparameter) that controls how large of a step we take down the hill.
- $\frac{dL}{dw}$: The derivative (specifically, the partial derivative) of the loss $L$ with respect to the weight $w$. It tells us two things: how steep the slope is and which direction leads uphill.
# The Numerical Derivative (Central Difference)
$$f'(x) \approx \frac{f(x + h) - f(x - h)}{2h}$$
- $f'(x)$: The estimated derivative (slope) of a function $f$ at a specific point $x$.
- $\approx$: Means "approximately equal to," because this is a numerical approximation rather than an exact mathematical calculation.
- $h$: A tiny number (like $0.0001$) used to nudge $x$ slightly to the right and left.
- $f(x + h)$ and $f(x - h)$: The function evaluated just slightly ahead of $x$ and slightly behind $x$.
- $2h$: The total distance between the two evaluation points used to estimate the slope of the curve.
# Key Takeaways: Loss Landscapes and Derivatives
- **The Loss Landscape:** Imagine a hilly terrain in a high-dimensional space. Your starting weights place you somewhere on a mountain. Your goal is to walk down into the lowest valley (global minimum).
- **Derivatives:** Whether calculated analytically (using calculus rules) or numerically (using small steps $h$), the derivative acts like a compass telling you which way is downhill so gradient descent can guide your steps.
