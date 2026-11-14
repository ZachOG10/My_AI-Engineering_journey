# THE GRADIENT: VECTOR OF ALL PARTIAL DIRAVATIVES
The gradiant collects every partial derivative into one vector.

# The Intuition:
A partial derivative isolates a single input (or weight). It answers the question: "If I nudge just this one weight slightly, how much will the total error (loss) go up or down?".
# The Gradient: Packing Partials into a Vector
When you have multiple partial derivatives, you combine them into a single vector called the gradient, written as $\nabla f$ (read "nabla $f$"):
$$\nabla f = \left[ \frac{\partial f}{\partial x}, \frac{\partial f}{\partial y} \right]$$

For our function $f(x, y) = x^2 + 3xy + y^2$, the gradient vector is:
$$\nabla f = [2x + 3y, \,\, 3x + 2y]$$
# Geometric Meaning
Imagine the function $f(x, y) = x^2 + y^2$ plotted in 3D. It forms a smooth, circular bowl where the bottom of the bowl (the minimum) sits at coordinates $(0, 0)$.
- The gradient points uphill: At any point on the bowl, the gradient vector points in the direction of steepest ascent—straight up the sides of the bowl, away from the minimum.
- Magnitude matters: The length (magnitude) of the vector tells you how steep the slope is at that exact spot. If you are halfway up the wall, the vector is long. If you are near the flat bottom, the vector shrinks to $[0, 0]$.

# Gradient Descent: Walking Downhill
Because the gradient $\nabla f$ always points in the direction of steepest ascent (uphill), moving in the exact opposite direction ($-\nabla f$) points straight down the slope toward the minimum.
- Here is a clean, from scratch Python implementation of gradient descent for multivariable function: $$f(x, y) = x^2 + 3xy + y^2$$
This script uses basic Python functions and a standard loop to iteratively step downhill toward the minimum at $(0, 0)$.
# python implementation:

# 1. Define the multivariable function (the "loss")
def compute_cost(x, y):
  return x**2 + 3 * x * y + y**2
# 2. Define the analytical gradient [df/dx, df/dy]
#Derived earlier as: [2x + 3y, 3x + 2y]
def compute_gradient(x, y):
  grad_x = 2 * x + 3 * y
  grad_y = 3 * x + 2 * y
  return grad_x, grad_y
# 3. Hyperparameters and starting point
x = 4.0  # Initial guess for x
y = -3.0  # Initial guess for y
learning_rate = 0.05  # Step size control
iterations = 15

print(f"Starting position: x = {x}, y = {y}")
print(f"Initial cost f(x, y) = {compute_cost(x, y):.4f}\n")
# 4. Gradient descent optimization loop
for i in range(iterations):
  # Step A: Calculate the gradient at our current location
  grad_x, grad_y = compute_gradient(x, y)
  # Step B: Update weights by stepping in the OPPOSITE direction of the gradient
  x = x - learning_rate * grad_x
  y = y - learning_rate * grad_y
  # Step C: Track progress
  cost = compute_cost(x, y)
  print(
      f"Iteration {i+1:2d}: x = {x:7.4f}, y = {y:7.4f} | Cost function ="
      f" {cost:8.4f}"
  )
print(f"\nFinal estimated minimum reached at: x = {x:.5f}, y = {y:.5f}")

# How the Code Works
1. compute_cost(): Represents the landscape or error surface we want to minimize. In a neural network, this would be your loss function comparing predictions to actual targets.
2. compute_gradient(): Returns the partial derivatives evaluated at the current coordinates $(x, y)$. This tells you the exact local slope and direction of steepest ascent.
3. The Update Step (x = x - learning_rate * grad_x):
- Multiplying by the learning rate ensures we take controlled, cautious steps rather than overshooting.
- Subtracting the gradient forces movement down the slope (away from uphill ascent).
