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
