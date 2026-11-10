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