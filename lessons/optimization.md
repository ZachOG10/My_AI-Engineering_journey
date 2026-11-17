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

# A Step-by-Step Optimization Loop
Let’s trace an explicit numerical example. Suppose our loss function is a simple quadratic equation:
$$L(w) = (w - 3)^2$$
Our goal is to find the weight $w$ that minimizes this loss. Obviously, looking at the equation, the optimal weight is $w = 3$ (where the loss becomes $0$). But let's see how gradient descent finds this blindly through math.
# Find the analytical derivative (the slope):
- Using the power rule of calculus, the derivative of $L(w)$ with respect to $w$ is:
$$\frac{dL}{dw} = 2(w - 3)$$
- Set your hyperparameters and starting point:
- Learning rate ($\alpha$): $0.1$
- Initial weight ($w_{\text{old}}$): $6.0$ (a bad starting guess)
# Execute the optimization loop:
Iteration 1:
- Current weight: $w = 6.0$
- Compute loss: $L(6) = (6 - 3)^2 = 9.0$
- Compute gradient (slope): $\frac{dL}{dw} = 2(6 - 3) = 6.0$ (Positive slope means we are to the right of the minimum; increasing $w$ increases loss).
- Apply update rule ($w_{\text{new}} = w_{\text{old}} - \text{learning\_rate} \times \frac{dL}{dw}$):
$$w_{\text{new}} = 6.0 - (0.1 \times 6.0) = 6.0 - 0.6 = 5.4$$
# Iteration 2:
- Current weight: $w = 5.4$
- Compute loss: $L(5.4) = (5.4 - 3)^2 = 5.76$ (Loss went down!).
- Compute gradient: $\frac{dL}{dw} = 2(5.4 - 3) = 4.8$
- Apply update rule:
$$w_{\text{new}} = 5.4 - (0.1 \times 4.8) = 5.4 - 0.48 = 4.92$$

# Iteration 3:
- Current weight: $w = 4.92$
- Compute loss: $L(4.92) = 3.6864$
- Compute gradient: $\frac{dL}{dw} = 2(4.92 - 3) = 3.84$
- Apply update rule:
$$w_{\text{new}} = 4.92 - (0.1 \times 3.84) = 4.536$$

As the steps repeat, the weight gradually shrinks from $6.0$ toward $3.0$, and the gradient approaches $0$. Once the gradient is $0$, the updates stop because $\text{learning\_rate} \times 0 = 0$.
