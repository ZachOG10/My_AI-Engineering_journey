## Every AI model is just matrix math wearing a fancy hat.

## Vectors
- A vector is an ordered list of numbers. The numbers mean something: coordinates, features, or a description of a thing.
- Normalized vectors are called unit vectors. 
- Normalize means shrink a vector to length 1 while keeping its direction: divide every item by the length.
## The Dot product:
- multiply matching items, add. No square root.
- Length of each vector: square, add, square root (only here).
- Divide the dot product by the two lengths multiplied.
## Semantic search and RAG:
- RAG means Retrieval-Augmented Generation: before an LLM answers, you fetch relevant documents and give them to it. The fetching is dot products.

## Matrices:

- A Matrix is a rectangular grid of numbers. The shape is (rows,columns).

# Three rules to memorize:
1. Shape rule: (m×n) @ (n×p) gives (m×p). The inner numbers must match. Most 'shape mismatch' errors in AI code are this rule being broken.
2. Order matters: B @ A = [[23, 34], [31, 46]], which is not A @ B. Matrix multiplication is not commutative.
3. Meaning: A @ B applied to a vector means 'do B first, then A'. Stacking neural network layers is chaining matrices.