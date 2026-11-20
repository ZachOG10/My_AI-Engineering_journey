# Multivariable Chain Rule in a Computation Graph
In a single-line function, derivatives just multiply in a straight line. In a neural network, values flow through a computation graph (nodes = operations/values, edges = flow of data).
# The Two Golden Rules of Graph Gradients
1. Along a single path: Multiply the local derivatives step by step.
2. When paths merge (fan-in): Add the contributions coming from every path that affects that variable.
# Walkthrough: Tiny Neuron + Binary Cross-Entropy Loss
Suppose we have input $x$, weight $w$, bias $b$, and true target $y$:
**Forward pass (left to right):** 
1. $z_1 = w \cdot x$
2. $z_2 = z_1 + b$ (so $z_2 = w x + b$)
3. $a = \text{sigmoid}(z_2)$
4. L=−[ylog⁡(a)+(1−y)log⁡(1−a)]L=−[ylog(a)+(1−y)log(1−a)]
# Backward pass (right to left):
Start at the end with $\frac{\partial L}{\partial L} = 1$, then multiply local slopes backward:
1. $\frac{\partial L}{\partial a} = -\frac{y}{a} + \frac{1 - y}{1 - a}$
2. $\frac{\partial L}{\partial z_2} = \frac{\partial L}{\partial a} \cdot \big(a(1 - a)\big)$
3. $\frac{\partial L}{\partial w} = \frac{\partial L}{\partial z_2} \cdot x$ (because $\frac{\partial z_2}{\partial w} = x$)
4. $\frac{\partial L}{\partial b} = \frac{\partial L}{\partial z_2} \cdot 1$ (because $\frac{\partial z_2}{\partial b} = 1$)
Notice how clean that is: if $x$ is large, $\frac{\partial L}{\partial w}$ scales up proportionally with $x$; the bias gradient $\frac{\partial L}{\partial b}$ passes straight through with a multiplier of $1$.
# The Jacobian Matrix (Vector-to-Vector Derivatives)
When a layer takes $n$ inputs and produces $m$ outputs—say $\mathbf{x} \in \mathbb{R}^3$ goes into a layer producing $\mathbf{f}(\mathbf{x}) \in \mathbb{R}^2$—there isn't just one derivative. Every output $f_i$ has a partial derivative with respect to every input $x_j$.
- Putting all of them into a grid gives the $m \times n$ Jacobian:
$$J = \begin{bmatrix} \frac{\partial f_1}{\partial x_1} & \frac{\partial f_1}{\partial x_2} & \cdots & \frac{\partial f_1}{\partial x_n} \\ \frac{\partial f_2}{\partial x_1} & \frac{\partial f_2}{\partial x_2} & \cdots & \frac{\partial f_2}{\partial x_n} \\ \vdots & \vdots & \ddots & \vdots \\ \frac{\partial f_m}{\partial x_1} & \frac{\partial f_m}{\partial x_2} & \cdots & \frac{\partial f_m}{\partial x_n} \end{bmatrix}$$
# Why Shapes Matter in Backprop
- Forward maps $\mathbb{R}^n \to \mathbb{R}^m$ using an $m \times n$ Jacobian.
- Backward pulls gradients from the output side back to the input side using the transpose ($n \times m$).
- You rarely build full Jacobians manually in deep learning (frameworks compute vector-Jacobian products directly), but knowing the shape rule saves you from countless matrix-dimension bugs.
# Tangent Lines & Critical Points ($f(x) = x^3 - 3x$)
The note at the bottom ties everything back to what a derivative actually looks like geometrically:
- Function: $f(x) = x^3 - 3x$
- Derivative (slope): $f'(x) = 3x^2 - 3$
- Tangent line at $x_0$: $y_{\text{tan}}(x) = f(x_0) + f'(x_0)(x - x_0)$
Setting the slope to zero (3x2−3=0  ⟹  x2=13x2−3=0⟹x2=1) gives critical points at x=−1x=−1 and x=+1x=+1, where the tangent line flattens out horizontally before the curve changes direction.
# Backward Pass Through Sigmoid + Binary Cross-Entropy
import math

def sigmoid(z):
  return 1.0 / (1.0 + math.exp(-z))

#Inputs and target
x = 2.0
w = 0.5
b = -0.5
y = 1.0  # true label

#Forward pass
z1 = w * x
z2 = z1 + b
a = sigmoid(z2)
loss = -(y * math.log(a) + (1.0 - y) * math.log(1.0 - a))

#Backward pass (chain rule right to left)
dL_da = -(y / a) + ((1.0 - y) / (1.0 - a))
da_dz2 = a * (1.0 - a)
dL_dz2 = dL_da * da_dz2

dL_dw = dL_dz2 * x
dL_db = dL_dz2 * 1.0

print(f"Prediction a = {a:.4f}, Loss L = {loss:.4f}")
print(f"dL/dw = {dL_dw:.4f}, dL/db = {dL_db:.4f}")

# Numerical Jacobian for a 2-Input to 3-Output Function
import numpy as np

#Maps R^2 -> R^3
def f(v):
  x1, x2 = v
  return np.array([x1 * x2, x1**2 + x2, math.sin(x1) + 2.0 * x2])

def numerical_jacobian(func, v, h=1e-5):
  v = np.asarray(v, dtype=float)
  out0 = func(v)
  jac = np.zeros((out0.size, v.size))
  for j in range(v.size):
    step = np.zeros_like(v)
    step[j] = h
    jac[:, j] = (func(v + step) - func(v - step)) / (2.0 * h)
  return jac

pt = [1.0, 2.0]
J = numerical_jacobian(f, pt)
print(f"Jacobian shape for R^2 -> R^3: {J.shape}")
print(J)
