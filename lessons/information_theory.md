# Information Theory
**Information Content (Surprise)**
Information content measures how surprising an outcome $x$ is when it occurs. Rare events carry high information; guaranteed events carry zero information.

$$I(x) = -\log(p(x))$$

# Reading and Computing It
- Why the minus sign: A probability $p(x)$ is between $0$ and $1$. The logarithm of a number less than $1$ is negative, so the negative sign makes surprise positive (or zero).
- Log base sets the unit: Base $2$ gives bits ($\log_2$). Natural log gives nats ($\ln$). They differ only by a constant scale factor ($\ln(a) = \ln(2) \log_2(a)$).
# Concrete Numerical Check
Suppose we use base $2$ (bits):
- Certain event ($p = 1.0$): $I(x) = -\log_2(1.0) = 0\text{ bits}$. Zero surprise.
- Fair coin heads ($p = 0.5$): $I(x) = -\log_2(0.5) = -\log_2(2^{-1}) = 1.0\text{ bit}$.
- Rare event ($p = 0.001$): $I(x) = -\log_2(0.001) \approx 9.97\text{ bits}$. Much higher surprise.
In machine learning, if a model assigns a very low probability $q(y)$ to the true class $y$, then $-\log q(y)$ is large—the model was caught off guard.

# Entropy (Average Surprise)
Entropy $H(P)$ is the expected (average) surprise of outcomes drawn from probability distribution $P$.

$$H(P) = -\sum_{x} p(x)\log(p(x))$$

Each outcome's surprise $-\log p(x)$ is weighted by how often that outcome actually happens, $p(x)$.
# Concrete Numerical Check
For a binary event with probabilities $p$ and $1 - p$ (in bits):
Fair coin ($p = 0.5, 1 - p = 0.5$):

$$H = -(0.5\log_2(0.5) + 0.5\log_2(0.5)) = -(0.5(-1) + 0.5(-1)) = 1.0\text{ bit}$$

- Biased coin ($p = 0.99, 1 - p = 0.01$):
$$H = -(0.99\log_2(0.99) + 0.01\log_2(0.01)) \approx -(0.99(-0.0145) + 0.01(-6.6439)) \approx 0.08\text{ bits}$$

# What Entropy Means in ML
Entropy measures uncertainty or unpredictability in a distribution.
- If all classes are equally likely (high uncertainty), entropy is high.
- If one class dominates (low uncertainty), entropy is low.
- In decision trees, algorithms like ID3/C4.5 use entropy reduction (information gain) to pick splits that make child groups purer.
# Cross-Entropy (The Classification Loss)
Cross-entropy $H(P, Q)$ measures the average surprise when events truly come from distribution $P$, but you measure surprise using your model's predicted distribution $Q$.

$$H(P, Q) = -\sum_{x} p(x)\log(q(x))$$

# Concrete ML Example
Suppose there are $3$ classes (Cat, Dog, Bird), and the true label is Dog ($c = \text{Dog}$).
- Model A predicts $Q = [0.10, 0.80, 0.10]$. Loss (in nats) is $-\ln(0.80) \approx 0.223$.
- Model B predicts $Q = [0.40, 0.20, 0.40]$. Loss (in nats) is $-\ln(0.20) \approx 1.609$.
Model A has lower cross-entropy loss because it assigned higher probability to the true class Dog. Minimizing $-\log q(c)$ pushes $q(c)$ toward $1$.
# KL Divergence (Mismatch Between $P$ and $Q$)
Kullback-Leibler (KL) divergence measures how much extra average surprise you experience by using model distribution $Q$ instead of the true distribution $P$.

$$D_{\text{KL}}(P \parallel Q) = \sum_{x} p(x)\log\left(\frac{p(x)}{q(x)}\right)$$#

Using the log quotient rule $\log(a/b) = \log a - \log b$, we can expand this:

$$D_{\text{KL}}(P \parallel Q) = \sum_{x} p(x)\log p(x) - \sum_{x} p(x)\log q(x) = -H(P) + H(P, Q)$$

Rearranging gives the exact identity in your note:
$$H(P, Q) = H(P) + D_{\text{KL}}(P \parallel Q)$$

# Two Critical Properties to Remember
1. Minimizing cross-entropy equals minimizing KL divergence during training: Because $P$ comes from the dataset, $H(P)$ is fixed with respect to model parameters. Changing model weights changes $Q$, which changes $H(P, Q)$ and $D_{\text{KL}}(P \parallel Q)$ by the exact same amount.2. Not symmetric (not a true distance): In general, $D_{\text{KL}}(P \parallel Q)$ is not equal to $D_{\text{KL}}(Q \parallel P)$.
- Forward KL, $D_{\text{KL}}(P \parallel Q)$: Penalizes putting low probability $q(x)$ where true probability $p(x)$ is high (used in standard supervised classification and maximum likelihood).
- Reverse KL, $D_{\text{KL}}(Q \parallel P)$: Penalizes putting high probability $q(x)$ where $p(x)$ is low (often mode-seeking, seen in variational inference).

# Joint Entropy, Conditional Entropy, and Mutual Information
Think of $H(X)$ as a circle and $H(Y)$ as an overlapping circle in the diagram above:
- Joint Entropy $H(X, Y)$: The total area covered by both circles together:
$$H(X, Y) = -\sum_x \sum_y p(x, y)\log(p(x, y))$$

Because overlap avoids double-counting, $H(X, Y) \le H(X) + H(Y)$. Equality holds only when $X$ and $Y$ are independent (zero overlap).
- Conditional Entropy $H(Y \mid X)$: The part of $Y$'s circle outside the overlap:
$$H(Y \mid X) = H(X, Y) - H(X)$$

It always satisfies $0 \le H(Y \mid X) \le H(Y)$. If $X$ completely determines $Y$ (like Celsius determining Fahrenheit), $H(Y \mid X) = 0$. If $X$ tells nothing about $Y$ (like a coin flip and tomorrow's weather), $H(Y \mid X) = H(Y)$.
- Mutual Information $I(X; Y)$: The overlapping lens in the middle:

$$I(X; Y) = H(X) - H(X \mid Y) = H(Y) - H(Y \mid X) = H(X) + H(Y) - H(X, Y) = \sum_x \sum_y p(x, y)\log\left(\frac{p(x, y)}{p(x)p(y)}\right)$$

# Numerical Example
Suppose $X$ is whether it rains today (0 = no, 1 = yes) and $Y$ is whether someone carries an umbrella (0 = no, 1 = yes), with joint probabilities in base $2$ (bits):
- $p(0, 0) = 0.45$, $p(0, 1) = 0.05$ $\implies p_X(0) = 0.50$
- $p(1, 0) = 0.10$, $p(1, 1) = 0.40$ $\implies p_X(1) = 0.50$
Marginal probabilities for $Y$: $p_Y(0) = 0.55$, $p_Y(1) = 0.45$.
1. Marginal entropies:
$$H(X) = -(0.5\log_2 0.5 + 0.5\log_2 0.5) = 1.000\text{ bit}$$
2. Joint entropy:
$$H(X, Y) = -(0.45\log_2 0.45 + 0.05\log_2 0.05 + 0.10\log_2 0.10 + 0.40\log_2 0.40) \approx 1.685\text{ bits}$$

3. Conditional entropy and mutual information:
$$H(Y \mid X) = H(X, Y) - H(X) \approx 1.685 - 1.000 = 0.685\text{ bits}$$
$$I(X; Y) = H(Y) - H(Y \mid X) \approx 0.994 - 0.685 = 0.309\text{ bits}$$
Knowing rain status $X$ drops uncertainty about carrying an umbrella $Y$ from $0.994$ bits down to $0.685$ bits—a reduction of $0.309$ bits.

# ML Role: Feature Selection and Decision Trees
- Decision trees split on the feature that minimizes conditional entropy $H(Y \mid X)$ (equivalently maximizing information gain $I(X; Y)$).
- Feature selection ranks features by $I(X_i; Y)$ and keeps the top $k$. Unlike Pearson correlation (linear only) or Spearman correlation (monotonic only), mutual information captures any statistical dependence—including non-monotonic curves—though finite samples need enough data and sensible discretization/binning.
# Label Smoothing, Cross-Entropy, Bits vs. Nats, and Perplexity
**Label Smoothing**
A hard one-hot target like [0, 0, 1, 0] has zero entropy and pushes logits toward extreme values. With $\epsilon = 0.1$ across $K = 4$ classes:
$$\text{soft\_target}_k = (1 - \epsilon)\cdot \text{hard\_target}_k + \frac{\epsilon}{K}$$
- True class (index 2): $(1 - 0.1)(1) + \frac{0.1}{4} = 0.9 + 0.025 = 0.925$
- Each other class: $(1 - 0.1)(0) + \frac{0.1}{4} = 0.025$
- Result: [0.025, 0.025, 0.925, 0.025]. Target entropy increases above $0$, preventing extreme logit growth and improving probability calibration.
# Why Cross-Entropy Is THE Classification Loss
- Information theory: Measures extra bits/nats wasted relative to true distribution $P$.
- Maximum likelihood: Over $N$ samples with true classes $y_i$, maximizing $\prod_i q(y_i)$ is equivalent to maximizing $\sum_i \log q(y_i)$ and minimizing $-\sum_i \log q(y_i)$ (negative log-likelihood).
- Gradients: Combined with softmax, the gradient of cross-entropy with respect to logits $z$ is simply $q - p$ (predicted probabilities minus target distribution), avoiding vanishing/exploding gradient headaches.
# Bits vs. Nats and Perplexity
Log base sets units: $\log_2 \to \text{bits}$, $\ln \to \text{nats}$ ($1\text{ nat} = \frac{1}{\ln 2}\text{ bits} \approx 1.4427\text{ bits}$). PyTorch and TensorFlow use natural log (nats) by default.
Perplexity exponentiates average cross-entropy:
$$\text{PPL} = 2^{H(P, Q)} \text{ (bits)} \quad \text{or} \quad \text{PPL} = e^{H(P, Q)} \text{ (nats)}$$

If average cross-entropy is $\ln(50) \approx 3.912\text{ nats}$, perplexity is $e^{3.912} \approx 50$—meaning the model's uncertainty equals choosing uniformly among $50$ equally likely next tokens. Lower is better.