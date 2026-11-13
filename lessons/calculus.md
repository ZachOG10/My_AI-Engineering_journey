# Diravatives:
- To truly master derivatives, it helps to look at them through three distinct lenses: geometry, algebra, and code.

# The Geometric Intuition: From Secant to Tangent
You already know that the slope of a straight line is constant ($m = \frac{\text{rise}}{\text{run}}$). But curves change their slope at every single point.
To find the slope of a curve at a specific point $x$:
- Pick a second point slightly further down the curve at $x + h$ (where $h$ is a tiny horizontal nudge).
- Draw a straight line connecting these two points. This is called a secant line. Its slope is:
$$\text{Slope of Secant} = \frac{f(x + h) - f(x)}{h}$$

- Now, imagine shrinking $h$ closer and closer to $0$. As $h$ shrinks, the second point slides down the curve toward your original point.

- When $h$ effectively becomes infinitesimal, the secant line pivots into a tangent line—a line that just grazes the curve at that exact point. That instantaneous slope is the derivative.

# Dissecting the Formal Limit Definition
- The formal definition of a derivative is written as:
$$f'(x) = \lim_{h \to 0} \frac{f(x + h) - f(x)}{h}$$

- Why do we need the limit ($\lim_{h \to 0}$)? Because if you try to set $h = 0$ directly in the fraction, you get:
$$\frac{f(x + 0) - f(x)}{0} = \frac{0}{0}$$

Division by zero is undefined. The limit is a mathematical mechanism that lets us get infinitely close to $0$ without ever actually letting $h$ equal $0$, allowing us to compute the exact instantaneous rate of change.

# Partial derivatives: one variable at a time
- A partial derivative is how we extend single-variable calculus to functions with multiple inputs.
When you have a function like $f(x, y)$, you can't just take "the" derivative because changing $x$ and changing $y$ might have completely different effects on the output. To solve this, calculus gives us a powerful rule: isolate and freeze.
- The Core Rule: Freeze Everything Except One
To find the partial derivative with respect to a single variable, you treat every other variable in the equation as a boring, ordinary constant number while you differentiate.

Let's look closely at your example function:

$$f(x, y) = x^2 + 3xy + y^2$$

# Finding $\frac{\partial f}{\partial x}$ (Partial derivative with respect to $x$)
We treat $y$ as a constant. Let's break down each term:
- $x^2$: The standard power rule gives $2x$.
- $3xy$: Since $y$ is treated as a constant, $3y$ is just a coefficient multiplier attached to $x$ (like $5x$). The derivative of $3yx$ with respect to $x$ is just the coefficient: $3y$.
- $y^2$: Since $y$ is a constant, $y^2$ is a pure constant. The derivative of any constant is $0$.
Putting it together:

$$\frac{\partial f}{\partial x} = 2x + 3y$$
# Finding $\frac{\partial f}{\partial y}$ (Partial derivative with respect to $y$)
Now we flip the script and treat $x$ as a constant:
- $x^2$: A pure constant with respect to $y$, so it evaluates to $0$.$3xy$: Here, $3x$ acts as the constant coefficient attached to $y$.
- Its derivative with respect to $y$ is $3x$.
- $y^2$: The power rule gives $2y$.

Putting it together:
$$\frac{\partial f}{\partial y} = 3x + 2y$$

$$\mathbf{f(x, y) = x^2 + 3xy + y^2}$$

# Read aloud:
- "f of x and y equals x squared, plus three x y, plus y squared."
# What it means:
- $f$ is our function (representing something like a neural network's loss), and it takes two independent inputs, $x$ and $y$. Because there are two inputs, changing $x$ or $y$ alters the output differently. To isolate them, we use partial derivatives.
#  Finding the Partial Derivative with Respect to $x$

- $$\mathbf{\frac{\partial f}{\partial x} = 2x + 3y} \quad (\text{treat } y \text{ as a constant})$$
# Read aloud:
- "Partial f, partial x equals two x plus three y, treating y as a constant."
# Breaking down the symbols:
- $\partial$ (the curly "d"): Read as "del" or "partial". Unlike an ordinary $d$, the curly symbol warns you: "This function has multiple variables, and we are only looking at the rate of change along one axis."
- $\frac{\partial f}{\partial x}$: Read as "The partial derivative of f with respect to x" or "partial f, partial x". It literally translates to: "How fast does the output change when I nudge $x$, while locking $y$ completely frozen?"

# Walking through the terms (treating $y$ as a constant):
1. $x^2$ ("x squared"): Using the standard power rule, bring the $2$ down and subtract $1$ from the exponent to get $2x$ ("two x").
2. $+ 3xy$ ("plus three x y"): Since $y$ is frozen as a constant, $3y$ acts as a coefficient multiplier attached to $x$ (just like $5x$). The derivative of a constant times $x$ is just the constant itself: $+ 3y$ ("plus three y").
3. $+ y^2$ ("plus y squared"): There is no $x$ here. Because $y$ is frozen as a constant, $y^2$ is a pure, unchanging constant number. The derivative of any constant is $0$.

Putting those pieces together gives us our first result: $\frac{\partial f}{\partial x} = 2x + 3y$.

# Finding the Partial Derivative with Respect to $y$
$$\mathbf{\frac{\partial f}{\partial y} = 3x + 2y} \quad (\text{treat } x \text{ as a constant})$$

# Read aloud:
- "Partial f, partial y equals three x plus two y, treating x as a constant."
# Breaking down the symbols:
- $\frac{\partial f}{\partial y}$: Read as "The partial derivative of f with respect to y" or "partial f, partial y". It translates to: "How fast does the output change when I nudge $y$, while locking $x$ completely frozen?"

# Walking through the terms (treating $x$ as a constant):
1. $x^2$ ("x squared"): Because $x$ is frozen as a constant, $x^2$ is a pure constant number. Its derivative is $0$.
2. $+ 3xy$ ("plus three x y"): Here, $3x$ acts as the constant coefficient multiplying our active variable $y$. Differentiating with respect to $y$ drops the variable and leaves the coefficient: $+ 3x$ ("plus three x").
3. $+ y^2$ ("plus y squared"): Now $y$ is our active variable, so we apply the power rule to $y^2$, bringing the $2$ down to get $+ 2y$ ("plus two y").

Putting those pieces together gives us our second result: $\frac{\partial f}{\partial y} = 3x + 2y$.

# Finding the Partial Derivative with Respect to $y$
$$\mathbf{\frac{\partial f}{\partial y} = 3x + 2y} \quad (\text{treat } x \text{ as a constant})$$

- Read aloud: "Partial f, partial y equals three x plus two y, treating x as a constant."
# Breaking down the symbols:
- $\frac{\partial f}{\partial y}$: Read as "The partial derivative of f with respect to y" or "partial f, partial y". It translates to: "How fast does the output change when I nudge $y$, while locking $x$ completely frozen?"
# Walking through the terms (treating $x$ as a constant):
1. $x^2$ ("x squared"): Because $x$ is frozen as a constant, $x^2$ is a pure constant number. Its derivative is $0$.
2. $+ 3xy$ ("plus three x y"): Here, $3x$ acts as the constant coefficient multiplying our active variable $y$. Differentiating with respect to $y$ drops the variable and leaves the coefficient: $+ 3x$ ("plus three x").
3. $+ y^2$ ("plus y squared"): Now $y$ is our active variable, so we apply the power rule to $y^2$, bringing the $2$ down to get $+ 2y$ ("plus two y").

Putting those pieces together gives us our second result: $\frac{\partial f}{\partial y} = 3x + 2y$.
# Manual Implementation (Using Our Derived Formulas)
# Define our original function: f(x, y) = x^2 + 3xy + y^2
def f(x, y):
    return x**2 + 3*x*y + y**2

# Our derived partial derivative with respect to x: 2x + 3y
def partial_f_x(x, y):
    return 2*x + 3*y

# Our derived partial derivative with respect to y: 3x + 2y
def partial_f_y(x, y):
    return 3*x + 2*y

# Test at coordinates x = 2, y = 1
x_val, y_val = 2, 1

print(f"Function value f({x_val}, {y_val}): {f(x_val, y_val)}")
print(f"Slope along x (∂f/∂x): {partial_f_x(x_val, y_val)}")  # Expected: 2(2) + 3(1) = 7
print(f"Slope along y (∂f/∂y): {partial_f_y(x_val, y_val)}")  # Expected: 3(2) + 2(1) = 8

# Symbolic Differentiation (Using SymPy)
If you don't want to derive the calculus formulas by hand, Python has a library called SymPy (Symbolic Python) that can solve derivatives algebraically, exactly like a human mathematician.

import sympy as sp

#Declare x and y as mathematical symbols (not just regular variables)
x, y = sp.symbols('x y')

#Define the function symbolically
f = x**2 + 3*x*y + y**2

#Take the partial derivative with respect to x (freezing y)
df_dx = sp.diff(f, x)

#Take the partial derivative with respect to y (freezing x)
df_dy = sp.diff(f, y)

print("Original function:", f)
print("Partial derivative w.r.t x (∂f/∂x):", df_dx)
print("Partial derivative w.r.t y (∂f/∂y):", df_dy)

#You can also evaluate them at specific points using .subs()
slope_x = df_dx.subs({x: 2, y: 1})
print(f"Slope at x=2, y=1 along x: {slope_x}")

# Numerical Approximation (Finite Differences)
In deep learning and complex software systems, equations can be so massive or wrapped in black-box code that you can't easily find a clean formula for the derivative. Instead, computers use finite differences—they take a tiny step ($h$) and check how much the output changes, exactly mirroring our definition of a slope ($\frac{\text{rise}}{\text{run}}$).

def f(x, y):
    return x**2 + 3*x*y + y**2

def numerical_partial_x(func, x, y, h=1e-5):
    # Hold y constant, nudge x by a tiny amount h
    return (func(x + h, y) - func(x, y)) / h

def numerical_partial_y(func, x, y, h=1e-5):
    # Hold x constant, nudge y by a tiny amount h
    return (func(x, y + h) - func(x, y)) / h

x_val, y_val = 2.0, 1.0

#Approximate the partial derivatives
approx_dx = numerical_partial_x(f, x_val, y_val)
approx_dy = numerical_partial_y(f, x_val, y_val)

print(f"Approximate ∂f/∂x: {approx_dx:.4f}")  # Very close to 7.0
print(f"Approximate ∂f/∂y: {approx_dy:.4f}")  # Very close to 8.0
