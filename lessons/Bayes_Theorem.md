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
# Naive Bayes, MLE, and Laplace Smoothing
Extending to Multiple Features (Naive Bayes)
A real email has many words (features $f_1, f_2, \dots, f_n$). Computing exact joint probabilities across dozens of words at once requires huge amounts of data. Naive Bayes makes a simplifying shortcut: it assumes that given the class (say, spam), each feature occurs independently of the others:
$$P(\text{class} \mid f_1, f_2, \dots, f_n) = \frac{P(\text{class}) \cdot \prod_{i=1}^{n} P(f_i \mid \text{class})}{P(f_1, f_2, \dots, f_n)}$$

- Why "naive"? In real language, words aren't independent—"New" and "York" often appear together, or "free" and "money".
- Why does it still work? When classifying an email into spam or not spam, the denominator $P(f_1, \dots, f_n)$ is identical for every class you compare. If you only care which class wins, you can drop the denominator and compare unnormalized scores:
$$\text{score}(\text{class}) = P(\text{class}) \cdot \prod_{i=1}^{n} P(f_i \mid \text{class})$$

# Maximum Likelihood Estimation (MLE)
How do you estimate $P(\text{word} \mid \text{class})$ from labeled training emails? Maximum Likelihood Estimation (MLE) picks the probability value that makes the observed training counts most probable. For word counts, that simplifies to a straightforward ratio:
$$P(\text{"free"} \mid \text{spam}) = \frac{\text{number of spam items with "free"}}{\text{total spam items}}$$
(In a multinomial word-token model, the denominator is the total number of word occurrences across all messages in that class.)
# The Zero-Probability Trap and Laplace Smoothing
Suppose the word "crypto" never appeared in any training spam email, so its count in spam is $0$. Under pure MLE, $P(\text{"crypto"} \mid \text{spam}) = 0$. When you multiply all feature probabilities together in $\text{score}(\text{spam})$, multiplying by $0$ wipes out the entire product—even if ten other words strongly scream "spam".
- Laplace smoothing (add-one smoothing) prevents any seen vocabulary word from getting a zero probability by adding $1$ to the numerator and adding the total vocabulary size $V$ (number of unique known words) to the denominator:
$$P(\text{word} \mid \text{class}) = \frac{\text{count}(\text{word}, \text{class}) + 1}{\text{total\_words\_in\_class} + V}$$

Adding $V$ to the denominator ensures the probabilities of all $V$ vocabulary words for a given class still sum to $1$. Finally, if a brand-new word at prediction time never appeared anywhere in the training vocabulary, it isn't in $V$ and is simply skipped because the training data offers zero evidence about how it behaves in either class.
