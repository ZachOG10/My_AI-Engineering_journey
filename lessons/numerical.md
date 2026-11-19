# Numerical vs. Analytical Derivatives
Suppose you want to know the steepness of a hill at a specific spot. There are two classic ways to find the derivative:
# Analytical Derivative (Using the Formula Rulebook)
Calculus gives you shortcuts so you get the exact slope formula without guessing.
- For $f(x) = x^2$, the rule says bring the exponent $2$ to the front and subtract $1$ from the power: $f'(x) = 2x$.
- Pros: Super fast and exact.
- Cons: You have to do the algebra/calculus to find the formula first.
# Numerical Derivative (The Tiny-Step Trick)
If you don't want to derive a formula or a function is messy you take two tiny steps around $x$: one slightly right ($x + h$) and one slightly left ($x - h$), with $h = 0.0001$:
$$f'(x) \approx \frac{f(x + h) - f(x - h)}{2h}$$

- Pros: Works on almost any function you can evaluate in code.
- Cons: Slower (you call the function extra times) and slightly approximate because $h$ is not truly zero.
# Real ML Example: Mean Squared Error (MSE)
Suppose a model predicts a number $\hat{y}$, and the true answer is $y = 10$. If the model guesses 
$\hat{y} = 7$, the squared error is $(7 - 10)^2 = 9$.
- Letting error $e = \hat{y} - y$, the loss is $L(e) = e^2$.
- Analytically, $\frac{dL}{de} = 2e$. At $e = -3$ (guessed too low), the slope is $-6$. Because the slope is negative, increasing $\hat{y}$ lowers the error.
- Numerically, with $h = 0.0001$, $\frac{(-2.9999)^2 - (-3.0001)^2}{2 \times 0.0001} \approx -6.0$.
* Note on Modern ML: Deep learning frameworks (like PyTorch or JAX) mostly use automatic differentiation breaking code into tiny elementary math operations and applying calculus rules automatically behind the scenes rather than hand-coding formulas or relying on slow finite differences during training.

# The Chain Rule: Backpropagation in Plain English
Imagine a nested set of boxes (like Russian nesting dolls):
- Inside is a line machine: $u = g(x) = 3x + 1$.
- Outside is a squaring machine: $y = f(u) = u^2$.
Together, $y = (3x + 1)^2$. How fast does $y$ change when $x$ changes?
# The Chain Rule says: multiply the rates of change along the chain:$$\frac{dy}{dx} = f'(g(x)) \cdot g'(x)$$
$$\frac{dy}{dx} = f'(g(x)) \cdot g'(x)$$

1. Outer slope with respect to $u$: $f'(u) = 2u = 2(3x + 1)$.
2. Inner slope with respect to $x$: $g'(x) = 3$.
3. Multiply them: $\frac{dy}{dx} = 2(3x + 1) \cdot 3 = 6(3x + 1)$.
# Why This Is Backpropagation
A neural network is just a long chain of steps:
$$\text{input} \rightarrow \text{linear layer} \rightarrow \text{activation} \rightarrow \text{linear layer} \rightarrow \text{loss}$$
Backpropagation simply starts at the final loss (mistake) at the end of the network and uses the chain rule backward to see how each weight $w$ and bias $b$ helped cause that mistake.

# The Hessian Matrix: Curvature, Bowls, and Saddles
A gradient (or first derivative) tells you the slope (which way is downhill).
The Hessian is a grid (matrix) of second derivatives that tells you the curvature—whether the ground bends upward like a bowl or downward like a dome.
For two variables $x$ and $y$, the Hessian is:
$$H = \begin{bmatrix} \frac{\partial^2 f}{\partial x^2} & \frac{\partial^2 f}{\partial x \partial y} \\ \frac{\partial^2 f}{\partial y \partial x} & \frac{\partial^2 f}{\partial y^2} \end{bmatrix}$$

At a critical point (where the ground is flat, so the gradient is zero), the Hessian's eigenvalues (special numbers summarizing the bend along main directions) tell you what kind of spot you're standing on:
Surface TypeHessian EigenvaluesWhat It Feels LikeLocal minimumAll positive (greater than 0)Bottom of a bowl—every direction curves upLocal maximumAll negative (less than 0)Top of a hill—every direction curves downSaddle pointMixed (some positive, some negative)A horse saddle—uphill in one direction, downhill in another

# Real Example: Bowl vs. Saddle
- Bowl: $f(x, y) = x^2 + y^2$. Second derivatives are $2$ and $2$. Both eigenvalues are positive $\rightarrow$ minimum at $(0, 0)$.
- Saddle: $f(x, y) = x^2 - y^2$. Second derivatives are $2$ and $-2$. One is positive and one is negative $\rightarrow$ saddle point at $(0, 0)$.
# Optimization: Gradient Descent vs. Newton's Method vs. Adam
- Gradient Descent takes steps proportional to the slope: $w_{\text{new}} = w_{\text{old}} - \text{lr} \cdot \text{gradient}$. If a canyon is narrow and steep in one direction and wide and flat in another, it can zigzag.
- Newton's Method divides by curvature (multiplying by $H^{-1}$), adjusting step sizes based on how curved the terrain is. However, for a model with $N$ parameters, the Hessian has $N \times N$ entries—for $1\text{ million}$ parameters, that is $1\text{ trillion}$ numbers!
- Adam is the go-to deep learning optimizer because it tracks running averages of gradients and squared gradients per parameter—getting a cheap, practical approximation of curvature without building a giant $N \times N$ matrix.

# Taylor Series: Zooming In on a Curve
If you zoom in close enough to almost any smooth curve, it starts looking simple. A Taylor series builds a polynomial (powers of $h$) around a point $x$ to approximate $f(x + h)$ nearby:
$$f(x + h) = f(x) + f'(x)h + \frac{1}{2!}f''(x)h^2 + \frac{1}{3!}f'''(x)h^3 + \cdots$$
Think of it as adding more detail as you look closer near $x$:
- 0th order ($f(x)$): Just the height right where you stand.
- 1st order ($f(x) + f'(x)h$): A straight line tangent to the curve—this is the idea behind gradient descent.
- 2nd order ($f(x) + f'(x)h + \frac{1}{2}f''(x)h^2$): A parabola (curve) fitting the slope and bend—this leads to Newton's method.

Because smooth loss functions like MSE and cross-entropy have well-behaved Taylor expansions locally, optimizers can predictably step toward lower loss.

# Integrals in Machine Learning: Adding Up Tiny Pieces
While derivatives measure rates of change (how fast something changes right now), integrals measure accumulation (adding up tiny pieces to get a total, like the area under a curve).
In ML, integrals show up whenever you deal with continuous ranges or uncertainty:
1. Probability over a range: For a probability density $p(x)$, the chance that a continuous value $X$ falls between $a$ and $b$ is the area under the curve from $a$ to $b$:
$$P(a < X < b) = \int_a^b p(x)\,dx$$

2. Expected value (average outcome): Weighting every possible outcome $f(x)$ by how likely it is ($p(x)$) and summing across all values:
$$\mathbb{E}[f(X)] = \int f(x)p(x)\,dx$$

Training a model on a dataset is like estimating an expected loss using a finite sample of examples.
3. KL Divergence: Measures how much one probability distribution $q(x)$ differs from a reference distribution $p(x)$:
$$KL(p \parallel q) = \int p(x)\log\frac{p(x)}{q(x)}\,dx$$

Used heavily in Variational Autoencoders (VAEs), reinforcement learning/policy updates, and distilling big models into smaller ones.
4. Normalization constants (Bayesian inference): To turn unnormalized scores into proper probabilities that sum/integrate to $1$, you divide by the integral over all possibilities:
$$p(w \mid \text{data}) = \frac{p(\text{data} \mid w)p(w)}{\int p(\text{data} \mid w)p(w)\,dw}$$

Because that bottom integral is often huge or impossible to compute exactly, ML uses sampling (like MCMC) or optimization approximations (like variational inference).
