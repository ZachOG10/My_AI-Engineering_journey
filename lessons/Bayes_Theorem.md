# From joint probability to Bayes
If you narrow your focus to only the outcomes where $B$ happens, what fraction of those also have $A$ happening? It is the overlap $P(A \text{ and } B)$ divided by the size of the $B$ group, $P(B)$:

$$P(A \mid B) = \frac{P(A \text{ and } B)}{P(B)}$$

Flip the roles of $A$ and $B$ and you get the symmetric rule:
$$P(B \mid A) = \frac{P(A \text{ and } B)}{P(A)}$$

# The Algebraic Bridge
Multiply both sides of each equation by its denominator to isolate the shared joint probability $P(A \text{ and } B)$:
1. From the first equation: $P(A \text{ and } B) = P(A \mid B) \cdot P(B)$
2. From the second equation: $P(A \text{ and } B) = P(B \mid A) \cdot P(A)$
Because both right-hand sides equal the exact same quantity—$P(A \text{ and } B)$—set them equal to each other:
$$P(A \mid B) \cdot P(B) = P(B \mid A) \cdot P(A)$$

Now divide both sides by $P(B)$ to solve for $P(A \mid B)$:
$$P(A \mid B) = \frac{P(B \mid A) \cdot P(A)}{P(B)}$$
# Expanding $P(B)$ with the Law of Total Probability
Event $B$ can happen when $A$ is true, or when $A$ is false ($\text{not } A$). Adding those two mutually exclusive ways together gives the total probability of $B$:
$$P(B) = P(B \mid A) \cdot P(A) + P(B \mid \text{not } A) \cdot P(\text{not } A)$$

# Tracing the Two Examples Step by Step
- Example A: Why Rare Diseases Fool Accurate Tests
Suppose $1$ in $10,000$ people has a disease, and a test catches $99\%$ of sick people while giving false positives to $1\%$ of healthy people.
- Prior: $P(\text{sick}) = \frac{1}{10,000} = 0.0001$, so $P(\text{healthy}) = 1 - 0.0001 = 0.9999$.
- Likelihoods: $P(\text{positive} \mid \text{sick}) = 0.99$, and $P(\text{positive} \mid \text{healthy}) = 0.01$.
Now trace the total chance of a positive test, $P(\text{positive})$:
1. True positives (sick and tests positive): $0.99 \times 0.0001 = 0.000099$
2. False positives (healthy and tests positive): $0.01 \times 0.9999 = 0.009999$
3. Add them: $P(\text{positive}) = 0.000099 + 0.009999 = 0.010098$
Finally, compute the posterior:
$$P(\text{sick} \mid \text{positive}) = \frac{0.000099}{0.010098} \approx 0.0098 \quad (0.98\%)$$

Why is it under $1\%$? Even though $99\%$ of sick people test positive, there are almost $10,000$ healthy people for every $1$ sick person. One percent of $9,999$ healthy people is about $100$ false positives, compared to only $\sim 0.99$ true positives per $10,000$ people. Most positives come from the huge healthy crowd.