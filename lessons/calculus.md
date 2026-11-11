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
