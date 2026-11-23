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
# AI and Machine Learning Connections
Data & latent variables: A dataset of inputs $X$ and labels $Y$ comes from a joint distribution $P(X, Y)$. Latent-variable models (like VAEs) work with joint distributions over observed data $x$ and latent code $z$, marginalizing out $z$ via $p(x) = \int p(x, z)\,dz$.
# Why the Normal Distribution Shows Up Everywhere (Central Limit Theorem)
The Central Limit Theorem (CLT) states that if you take independent random variables from any distribution with a finite variance, their average (or sum), once properly centered and scaled, approaches a Normal (Gaussian) distribution as the sample size grows.
# Symbols and Terms
- i.i.d. (independent and identically distributed): Samples drawn independently from the same underlying distribution.
- $\mu$ and $\sigma$: Mean and standard deviation of the normal curve. The curve is symmetric around $\mu$, and roughly $68\%$, $95\%$, and $99.7\%$ of probability mass fall within $\mu \pm 1\sigma$, $\mu \pm 2\sigma$, and $\mu \pm 3\sigma$, respectively.
# Intuition with Dice
- 1 die: Discrete uniform distribution ($1/6$ for each face $1$–$6$).
- 2 dice average/sum: Peaked triangular shape (more ways to roll a $7$ than a $2$ or $12$).
- 30+ dice average/sum: Smooth bell curve—even though a single die isn't bell-shaped at all.
# AI and Machine Learning Connections
- Measurement & observation noise: Real sensors aggregate many small disturbances, making noise approximately Gaussian.
- Mini-batch SGD gradients: A mini-batch gradient is an average over many examples, so its noise behaves approximately normally around the true gradient.
- Weight initialization & priors: Gaussian distributions are smooth, analytically tractable, and well-behaved for random weight initialization and latent priors.
# Log Probabilities and Numerical Stability
Multiplying many small probabilities together—such as token probabilities along a sentence:

$$P(\text{sentence}) = \prod_{t=1}^{n} P(\text{word}_t \mid \text{context}_{<t})$$

quickly shrinks toward $0$. For instance, multiplying $30$ numbers around $0.01$ gives $10^{-60}$, which can underflow to exact 0.0 in standard floating-point arithmetic.
Taking logarithms turns products into sums:
$$\log P(\text{sentence}) = \sum_{t=1}^{n} \log P(\text{word}_t \mid \text{context}_{<t})$$
# Rules and Terms
- Product rule: $\log(a \cdot b) = \log(a) + \log(b)$.
- Sign of log probabilities: Since a probability satisfies $0 < P \le 1$, its log probability satisfies $\log(P) \le 0$ (assuming natural log $\ln$, or any base greater than $1$).
- Ordering: A probability closer to $0$ has a more negative log probability (for example, $\ln(0.01) \approx -4.61$ vs. $\ln(0.5) \approx -0.69$).
- Cross-entropy link: For a one-hot true class $c$, cross-entropy loss is $-\log(q_c)$, the negative log probability of the correct class.
# Softmax, The Softmax Trick, and Log-Softmax
Neural networks for multi-class classification or next-token prediction usually output raw, unnormalized scores called logits, denoted $z = [z_1, z_2, \dots, z_K]$ (which can be negative, zero, or greater than $1$).The softmax function converts logits into a valid probability distribution:
$$\text{softmax}(z_i) = \frac{\exp(z_i)}{\sum_{j=1}^{K} \exp(z_j)}$$
# Properties and Pitfalls
- Every output lies strictly between $0$ and $1$, and all outputs sum to $1$.
- Exponentiating amplifies differences between logits: a higher logit gets exponentially more weight.
- Overflow hazard: If $z = [100, 101, 102]$, computing $\exp(102) \approx 2.28 \times 10^{44}$ can overflow (inf) in float32/float64.
- The Softmax Trick: Subtract $m = \max_j z_j$ from every logit before exponentiating:
$$\text{softmax}(z_i) = \frac{\exp(z_i - m)}{\sum_{j=1}^{K} \exp(z_j - m)}$$

Because $e^{c}$ factors out of both numerator and denominator, the exact mathematical value is unchanged, while the largest exponent becomes $\exp(0) = 1$—preventing overflow.
- Log-softmax: Computing $\log(\text{softmax}(z_i))$ directly via log-sum-exp:

$$\text{log-softmax}(z_i) = (z_i - m) - \log\!\left(\sum_{j=1}^{K} \exp(z_j - m)\right)$$

avoids both overflow from $\exp(\cdot)$ and precision loss from taking $\log$ of tiny probabilities near $0$. Frameworks like PyTorch fuse log-softmax with negative log-likelihood (nn.CrossEntropyLoss) for numerical stability.
# Sampling in AI and Machine Learning
Sampling means drawing random realizations from a probability distribution rather than only taking the single highest-probability choice (argmax).
# Where Sampling Appears in Machine Learning
- LLM text generation: Sampling from the next-token distribution introduces variety and creativity instead of repetitive greedy decoding; adjusting temperature scales logits before softmax to sharpen or flatten the distribution.
- Dropout and data augmentation: Randomly masking activations or applying random crops/flips regularizes training and improves generalization.
- Diffusion models & VAEs: Diffusion models sample Gaussian noise and iteratively denoise it into data; VAEs sample from learned latent distributions (using the reparameterization trick, e.g., $z = \mu + \sigma \odot \epsilon$ with $\epsilon \sim \mathcal{N}(0, I)$, so gradients can flow through $\mu$ and $\sigma$).
