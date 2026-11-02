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

# The Catch: When Can You Invert a Matrix?
- Just like you can't divide a regular number by zero, not every matrix can be inverted. For a matrix to have an inverse, it must meet strict rules:
* It must be a square matrix: It must have the exact same number of rows and columns (e.g., $2 \times 2$, $3 \times 3$). Non-square matrices cannot be inverted.
* It must be "non-singular": Its determinant (a special scalar value calculated from the matrix elements) cannot be zero. If the determinant is $0$, the matrix is "singular," meaning it has collapsed dimensions, and its inverse simply does not exist.

# What is a Dot Product?
- A dot product takes two vectors of the exact same length, multiplies their corresponding elements together, and then adds all those products up into a single number (scalar).
* For example, the dot product of two vectors $v = \begin{bmatrix} 1 & 2 \end{bmatrix}$ and $u = \begin{bmatrix} 5 \\ 7 \end{bmatrix}$ looks like this:

$$(1 \times 5) + (2 \times 7) = 5 + 14 = 19$$

# How Dot Products Build Matrix Multiplication
- When you multiply two matrices together, every single number (element) in your final resulting matrix is born from a dot product:
* You take a row from the first matrix.
* You take a column from the second matrix.
* You calculate their dot product. That single number becomes one entry in your new matrix.

If you multiply a $2 \times 2$ matrix by a $2 \times 2$ matrix, you are essentially doing four separate dot products to fill in the four spots of the new grid:

$$\begin{bmatrix} \text{Row 1} \\ \text{Row 2} \end{bmatrix} \times \begin{bmatrix} \text{Col 1} & \text{Col 2} \end{bmatrix} = \begin{bmatrix} (\text{Row 1} \cdot \text{Col 1}) & (\text{Row 1} \cdot \text{Col 2}) \\ (\text{Row 2} \cdot \text{Col 1}) & (\text{Row 2} \cdot \text{Col 2}) \end{bmatrix}$$

