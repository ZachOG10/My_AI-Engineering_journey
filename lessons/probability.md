# Events, Sample Spaces, and the Three Axioms
Probability is the mathematical language of uncertainty—and AI and machine learning run on uncertainty. Training data is a noisy sample from a larger world, model predictions are often probability distributions over possible outputs, and optimization algorithms rely on averages and variances across batches.
- The sample space $S$ captures every possible outcome. An event $A$ is any subset of $S$.
# The Three Kolmogorov Axioms
1. Non-negativity: $P(A) \ge 0$ for any event $A$. Probabilities cannot be negative.
2. Normalization: $P(S) = 1$. Something in the sample space is guaranteed to happen.
3. Additivity for mutually exclusive events: If $A$ and $B$ cannot happen at the same time (disjoint/mutually exclusive), then $P(A \text{ or } B) = P(A) + P(B)$.
# Why This Matters in AI and Machine Learning:
- Valid model outputs: When a classifier outputs class probabilities, every probability must be at least $0$, and all class probabilities must sum to $1$.
- Mutually exclusive classes: In standard single-label classification (e.g., classifying an image as cat, dog, or bird), the classes are treated as mutually exclusive—so $P(\text{cat or dog}) = P(\text{cat}) + P(\text{dog})$. (By contrast, multi-label tagging like outdoor and sunny can co-occur, so they are not mutually exclusive.)
# Conditional Probability and Independence
- Conditional probability updates your belief about event $A$ once you know event $B$ happened:
$$P(A \mid B) = \frac{P(A \text{ and } B)}{P(B)}$$
In a standard 52-card deck, there are $12$ face cards (Jack, Queen, King across 4 suits) and $4$ Kings. Given that you drew a face card ($B$), the probability it is a King ($A$) is:
$$P(\text{King} \mid \text{Face card}) = \frac{4/52}{12/52} = \frac{4}{12} = \frac{1}{3}$$
- Two events $A$ and $B$ are independent when observing $B$ does not change the probability of $A$:
$$P(A \mid B) = P(A) \iff P(A \text{ and } B) = P(A) \cdot P(B)$$
- Independent: Consecutive fair coin flips—knowing the first flip was Heads does not change the second flip's $0.5$ chance.
- Dependent: Drawing cards without replacement—removing a card changes the remaining deck composition and alters later probabilities.
# Why This Matters in AI and Machine Learning:
- Bayesian inference & generative models: Language models and vision models compute conditional probabilities like $P(\text{next token} \mid \text{previous tokens})$ or $P(\text{label} \mid \text{image})$.
- Conditional independence assumptions: Models like Naive Bayes assume features are conditionally independent given the class label to make high-dimensional calculations tractable—even when real-world features have some correlation.
- Data leakage: If training and test splits are not independent (for example, consecutive frames from the same video split across train and test), test accuracy becomes artificially inflated.
# Discrete vs. Continuous: PMFs vs. PDFs
**Probability Mass Function (PMF) — Discrete Variables**
- A discrete random variable takes countable values (integers or categories). Its PMF gives the exact probability at each value:
$$P(X = k), \quad \sum_{k} P(X = k) = 1$$
For a fair 6-sided die, $P(X = k) = \frac{1}{6}$ for each $k \in \{1, 2, 3, 4, 5, 6\}$
# Probability Density Function (PDF) — Continuous Variables
- A continuous random variable can take any real value in an interval (like height, latency, or a latent embedding coordinate). For a continuous variable, the probability of hitting any exact single point is $0$. Instead, probability is the area under the PDF $f(x)$ over an interval $[a, b]$:
$$P(a \le X \le b) = \int_a^b f(x)\,dx, \quad \int_{-\infty}^{\infty} f(x)\,dx = 1$$
Note that $f(x)$ is a density, not a probability—it can be greater than $1$ on a narrow interval, as long as the total area under the curve equals $1$.
# Why This Matters in AI and Machine Learning:
- Classification uses PMFs: A softmax layer outputs a discrete probability distribution over classes (e.g., $[0.70, 0.20, 0.10]$).
- Continuous latents & diffusion use PDFs: Variational Autoencoders (VAEs) and diffusion models work with continuous probability densities over vector spaces, optimizing likelihoods or score functions rather than discrete point masses.
# Common Probability Distributions in AI and Machine Learning:
DistributionTypeKey Formula / PMF or PDFMean & VarianceCore AI / ML Use CasesBernoulliDiscrete ($0$ or $1$)$P(X=1)=p$, $P(X=0)=1-p$$\text{Mean} = p$$\text{Var} = p(1-p)$Binary classification (sigmoid output), coin/click/fraud indicatorsCategoricalDiscrete ($1$ to $k$)$P(X=i)=p_i$, $\sum_i p_i = 1$$\text{Mean vector } \mathbf{p}$Multi-class classification (softmax output), token sampling in LLMsUniformDiscrete or ContinuousDiscrete: $P(X=k)=\frac{1}{n}$Continuous: $f(x)=\frac{1}{b-a}$ on $[a,b]$Continuous:$\text{Mean} = \frac{a+b}{2}$$\text{Var} = \frac{(b-a)^2}{12}$Random weight/parameter initialization, random sampling, baseline priorsNormal (Gaussian)Continuous$f(x) = \frac{1}{\sqrt{2\pi\sigma^2}}\exp\!\left(-\frac{(x-\mu)^2}{2\sigma^2}\right)$$\text{Mean} = \mu$$\text{Var} = \sigma^2$Weight initialization, Gaussian noise, VAEs/diffusion priors, Central Limit TheoremPoissonDiscrete ($k = 0, 1, 2, \dots$)$P(X=k) = \frac{\lambda^k e^{-\lambda}}{k!}$$\text{Mean} = \lambda$$\text{Var} = \lambda$Modeling count rates in fixed intervals (API requests/sec, rare events)

# Expected Value and Variance
Expected value $\mathbb{E}[X]$ is the probability-weighted average of a random variable:
- Discrete: $\mathbb{E}[X] = \sum_i x_i P(X = x_i)$
- Continuous: $\mathbb{E}[X] = \int_{-\infty}^{\infty} x f(x)\,dx$
Variance $\text{Var}(X)$ measures how spread out values are around $\mathbb{E}[X]$:
$$\text{Var}(X) = \mathbb{E}\!\left[(X - \mathbb{E}[X])^2\right] = \mathbb{E}[X^2] - (\mathbb{E}[X])^2$$
Standard deviation is $\sigma = \sqrt{\text{Var}(X)}$.
# Why This Matters in AI and Machine Learning:
- Loss functions as expectations: Minimizing empirical risk (average loss over a dataset) approximates minimizing expected loss $\mathbb{E}_{(x, y) \sim P_{\text{data}}}[\mathcal{L}(f_\theta(x), y)]$ over the true data distribution.
- Gradient variance & training stability: Stochastic Gradient Descent (SGD) estimates gradients from mini-batches. Small batches or noisy labels increase gradient variance, causing loss curves to jitter or oscillate; larger batches or momentum/Adam help stabilize updates.
- Bias–variance tradeoff: High-variance models overfit training noise and generalize poorly to unseen data.

# Bayes' Theorem: Updating Beliefs with Evidence
Bayes' theorem shows how to update the probability of a hypothesis after observing new evidence. Cross-entropy loss measures how poorly a predicted probability distribution matches the true outcome—making it the go-to training loss for classification and language models.

Both connect directly to how AI models represent uncertainty, update beliefs, and learn from data.
Starting from conditional probability $P(A \mid B) = \frac{P(A \text{ and } B)}{P(B)}$ and the fact that $P(A \text{ and } B) = P(B \mid A)P(A)$, we get Bayes' theorem (often written with hypothesis $H$ and evidence $E$):
$$P(H \mid E) = \frac{P(E \mid H)\,P(H)}{P(E)}$$
# What Each Term Means
- $P(H)$ (Prior): Your initial probability of hypothesis $H$ before seeing evidence $E$.
- $P(E \mid H)$ (Likelihood): How probable evidence $E$ is assuming hypothesis $H$ is true.
- $P(E)$ (Evidence / Marginal Likelihood): The total probability of observing $E$ across all possibilities. For mutually exclusive events $H$ and $\neg H$ ("not $H$"), $P(E) = P(E \mid H)P(H) + P(E \mid \neg H)P(\neg H)$.
- $P(H \mid E)$ (Posterior): Your updated probability of $H$ after observing $E$.
# Worked Example: Fraud Detection and Base Rates
Suppose only $1\%$ of transactions are fraudulent ($P(\text{Fraud}) = 0.01$, so $P(\text{Legit}) = 0.99$). A fraud model triggers an alert with:
- True positive rate: $P(\text{Alert} \mid \text{Fraud}) = 0.90$
- False positive rate: $P(\text{Alert} \mid \text{Legit}) = 0.05$
First, calculate the overall probability of an alert:
$$P(\text{Alert}) = (0.90)(0.01) + (0.05)(0.99) = 0.009 + 0.0495 = 0.0585$$

Now apply Bayes' theorem to find the chance an alerted transaction is actually fraud:
$$P(\text{Fraud} \mid \text{Alert}) = \frac{0.90 \times 0.01}{0.0585} = \frac{0.009}{0.0585} \approx 0.1538 \text{ (about } 15.4\%\text{)}$$

Even with a $90\%$ true positive rate, roughly $84.6\%$ of alerts are false alarms because true fraud is rare. Ignoring base rates ($P(\text{Fraud}) = 0.01$) is a classic pitfall when interpreting model predictions or alerts.
# AI and Machine Learning Connections
- Generative models: Models that learn class-conditional likelihoods $P(X \mid Y)$ and class priors $P(Y)$ use Bayes' theorem to infer $P(Y \mid X)$.
- MAP (Maximum A Posteriori) estimation: Regularization techniques like L2 weight decay correspond to placing a prior (such as a zero-mean Gaussian) over model weights and maximizing the posterior $P(\theta \mid \text{data})$.
# Cross-Entropy Loss: Scoring Predicted Probabilities
Suppose a true outcome has probability distribution $p$ (often one-hot, such as $[1, 0, 0]$ for class $0$), and a model outputs predicted probabilities $q$ (such as from a softmax or sigmoid layer).
- Multi-class cross-entropy over $K$ classes:
$$H(p, q) = -\sum_{i=1}^{K} p_i \log(q_i)$$

- Binary cross-entropy for binary targets $y \in \{0, 1\}$ and predicted probability $\hat{y} \in (0, 1)$:
$$\mathcal{L}_{\text{BCE}}(y, \hat{y}) = -\Big[ y \log(\hat{y}) + (1 - y)\log(1 - \hat{y}) \Big]$$
(In ML, $\log$ typically denotes the natural logarithm $\ln$, base $e$.)
# Why $-\log(q_i)$ Penalizes Mistakes Strongly
When $p$ is one-hot with true class $c$ ($p_c = 1$, others $0$), cross-entropy simplifies to $-\log(q_c)$:
- High confidence on the right class ($q_c = 0.95$) $\implies -\ln(0.95) \approx 0.051$ (small loss).
- Low confidence on the right class ($q_c = 0.20$) $\implies -\ln(0.20) \approx 1.609$ (larger loss).
- High confidence on the wrong class ($q_c = 0.01$) $\implies -\ln(0.01) \approx 4.605$ (steep penalty).

Minimizing cross-entropy is equivalent to maximizing likelihood (minimizing negative log-likelihood), and equals $H(p) + D_{\text{KL}}(p \parallel q)$, where $H(p)$ is entropy of the target and $D_{\text{KL}}(p \parallel q)$ is KL divergence measuring how much $q$ diverges from $p$.

# Worked Example: Multi-Class Classifier
For a sample whose true class is index $0$ ($p = [1.0, 0.0, 0.0]$):
- Model A predicts $q_A = [0.80, 0.15, 0.05] \implies -\ln(0.80) \approx 0.223$
- Model B predicts $q_B = [0.20, 0.70, 0.10] \implies -\ln(0.20) \approx 1.609$
Model A has much lower cross-entropy because it puts more probability mass on the true class.
