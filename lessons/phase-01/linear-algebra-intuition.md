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

## Row Matrix:
- A matrix with only one row.
- Column Matrix: A matrix with only one column.
- Square Matrix: A matrix where the number of rows equals the number of columns.
- Identity Matrix: A special square matrix with ones on the main diagonal (top-left to bottom-right) and zeros everywhere else. It acts like the number "1" in regular multiplication.
- Zero Matrix: A matrix where every single element is zero.

## Basic Matrix Operations
1. Matrix Addition and Subtraction
You can only add or subtract two matrices if they have the exact same dimensions. To do this, you simply add or subtract the corresponding elements in each position.
2. Scalar Multiplication
Multiplying a matrix by a single number (called a scalar) is straightforward: you multiply every single element in the matrix by that number.
3. Matrix Multiplication (The Dot Product)
- Multiplying two matrices together is a bit more involved than addition.
- The Golden Rule: You can only multiply Matrix if the number of columns in equals the number of rows in. The resulting matrix will have the dimensions of the outer numbers.
- How it works: You take the rows of the first matrix and multiply them element-by-element against the columns of the second matrix, adding the results together (this is called the dot product).
