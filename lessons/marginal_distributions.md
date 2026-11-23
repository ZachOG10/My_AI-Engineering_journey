# Joint and Marginal Distributions
These topics bridge core probability theory with the day-to-day mechanics of neural networks, probabilistic modeling, and numerical computing.
A joint distribution $P(X, Y)$ gives the probability that two random variables take specific values together at the same time. For discrete variables, $P(X = x, Y = y)$ is the joint PMF, and every cell in the table must satisfy $P(X=x, Y=y) \ge 0$ with all cells summing to $1.00$.
# Symbols and Terms
- $P(X, Y)$ / $P(X=x, Y=y)$: Joint probability of $X$ and $Y$ occurring together.
- $P(X)$ / $P(Y)$: Marginal distributions—the probability distribution of one variable alone, obtained by summing (or integrating, in the continuous case) over all values of the other variable ("summing out" or "marginalizing out" the nuisance variable).
- $\sum_y$: Sum over every possible value $y$ that random variable $Y$ can take.
# Weather and Umbrella Table
Let $X$ be weather ($0 =$ sun, $1 =$ rain) and $Y$ be umbrella use ($0 =$ no umbrella, $1 =$ umbrella):
Y=0 (No umbrella)  Y=1 (Umbrella)  Marginal P(X)
$X = 0$ (Sun)  $0.40$  $0.10$  $0.50$
$X = 1$ (Rain) $0.05$  $0.45$  $0.50$
Marginal $P(Y)$ $0.45$ $0.55$  $1.00$
- Marginal for $X=1$ (rain): $P(X=1) = P(X=1, Y=0) + P(X=1, Y=1) = 0.05 + 0.45 = 0.50$.
- Marginal for $Y=1$ (umbrella): $P(Y=1) = P(X=0, Y=1) + P(X=1, Y=1) = 0.10 + 0.45 = 0.55$.
- Check independence: Here $P(X=1, Y=1) = 0.45$, whereas $P(X=1)P(Y=1) = 0.50 \times 0.55 = 0.275$. Because $0.45 \neq 0.275$, $X$ and $Y$ are not independent—rain makes carrying an umbrella much more likely.
