# Matrices
# A Matrix:
- This is a rectangular grid of numbers, consisting of rows and colums.

# Elements:
- The individual numbers inside the matrix is called an element or item.

## Common types of metrices:
- Row matrix: This is a matrix with just one row.
- column matrix: This is a matrix with only one column.
- square matrix: This is a matrix where the number of rows and columns are esqual.
- identity matrix: This is a special matrix with zeros on the main diagonal and ones on everywhereelse.
- Zero matrix: This is a matrix where all the elements are zero.
## Basic matrix operations

# Matrix addition and subtraction
- You can only add and subtract a matrix only if they are of the same dimension. You can do this by adding or subtracting each coresponding element.
# scalar multiplication
- Multiplying a matrix is straightforward: you multiply each element in the matrix by the number.
# Matrix Multiplication (The Dot Product)
- Multiplying two matrices together is a bit more involved than addition.
# The Golden Rule:
- You can only multiply Matrix $A$ by Matrix $B$ if the number of columns in $A$ equals the number of rows in $B$. If $A$ is $2 \times \mathbf{3}$ and $B$ is $\mathbf{3} \times 2$, you can multiply them because the inner numbers match. The resulting matrix will have the dimensions of the outer numbers ($2 \times 2$).
- How it works: You take the rows of the first matrix and multiply them element-by-element against the columns of the second matrix, adding the results together (this is called the dot product).
# Example:
$$\begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix} \times \begin{bmatrix} 5 & 6 \\ 7 & 8 \end{bmatrix} = \begin{bmatrix} (1 \times 5 + 2 \times 7) & (1 \times 6 + 2 \times 8) \\ (3 \times 5 + 4 \times 7) & (3 \times 6 + 4 \times 8) \end{bmatrix} = \begin{bmatrix} 19 & 22 \\ 43 & 50 \end{bmatrix}$$
* (Note: Matrix multiplication is not commutative, meaning $A \times B$ is usually not equal to $B \times A$.)

# The Inverse Matrix ($A^{-1}$)
- If you have a square matrix $A$, its inverse is denoted as $A^{-1}$.
- When you multiply a matrix by its own inverse, you don't get the number $1$. Instead, you get the Identity Matrix ($I$)—which is the matrix equivalent of the number $1$:

$$A \times A^{-1} = I$$

So, if you ever need to "divide" by a matrix $A$ to solve an equation like $AX = B$, you don't divide. Instead, you multiply both sides by the inverse ($A^{-1}$):

$$A^{-1} \times (A \times X) = A^{-1} \times B$$

$$X = A^{-1}B$$

