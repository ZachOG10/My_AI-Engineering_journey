## Linear transformations are the foundational mechanics behind how computers manipulate space, data, and models.

# Linear Transformations & The Role of Basis Vectors
# Detailed Mathematical Foundations
# Linear Transformations & The Role of Basis Vectors:
- A linear transformation is a function $T: \mathbb{R}^n \to \mathbb{R}^m$ that
preserves vector addition and scalar multiplication:
$$T(\mathbf{u} + \mathbf{v}) = T(\mathbf{u}) + T(\mathbf{v})$$$$T(c\mathbf{v}) = cT(\mathbf{v})$$

- In linear algebra and AI engineering, the notation $T: \mathbb{R}^n \to \mathbb{R}^m$ is a concise way of describing a function, mapping, or transformation that takes an input from one dimensional space and converts it into an output in another dimensional space.

In 2D space, any linear transformation is entirely defined by where it sends the standard basis vectors:
$\mathbf{e}_1 = \begin{bmatrix} 1 \\ 0 \end{bmatrix}$ (along the x-axis)$\mathbf{e}_2 = \begin{bmatrix} 0 \\ 1 \end{bmatrix}$ (along the y-axis)
If a transformation moves $\mathbf{e}_1$ to $\mathbf{e}_1'$ and $\mathbf{e}_2$ to $\mathbf{e}_2'$, the transformation matrix $M$ is formed by placing these new vectors as its columns:
$$M = \begin{bmatrix} \mathbf{e}_1' & \mathbf{e}_2' \end{bmatrix} = \begin{bmatrix} a & c \\ b & d \end{bmatrix}$$
To transform any arbitrary vector $\mathbf{v} = \begin{bmatrix} x \\ y \end{bmatrix}$, you perform matrix-vector multiplication:
$$M\mathbf{v} = \begin{bmatrix} a & c \\ b & d \end{bmatrix} \begin{bmatrix} x \\ y \end{bmatrix} = x\begin{bmatrix} a \\ b \end{bmatrix} + y\begin{bmatrix} c \\ d \end{bmatrix} = \begin{bmatrix} ax + cy \\ bx + dy \end{bmatrix}$$

# Breaking Down the Notation

$$\underbrace{T}_{\text{The Transformation}}: \underbrace{\mathbb{R}^n}_{\text{Input Space (Domain)}} \longrightarrow \underbrace{\mathbb{R}^m}_{\text{Output Space (Codomain)}}$$

$T$ (The Transformation):
- This is the name of the rule, function, or operation being applied. In our previous discussion, $T$ could be a rotation, scaling, shearing, or a neural network layer. When you feed a vector into $T$, it transforms it.
- $\mathbb{R}^n$ (The Input Space / Domain):
$\mathbb{R}$ stands for the set of real numbers (meaning the coordinates can be any real number like $2$, $-5.3$, $\pi$, etc.).
$n$ represents the number of dimensions (or features) of the input vector.

Example: If an input vector $\mathbf{x}$ has 2 elements $\begin{bmatrix} x_1 \\ x_2 \end{bmatrix}$, then it lives in $\mathbb{R}^2$ (a 2D plane). If it has 768 elements (like an embedding vector from an LLM), it lives in $\mathbb{R}^{768}$.- $\to$ (Maps to):
This arrow means "transforms into" or "maps inputs from the left side to outputs on the right side.
- "$\mathbb{R}^m$ (The Output Space / Codomain):
$m$ represents the number of dimensions of the resulting output vector after the transformation has been applied.
Example: The output vector might have 3 elements $\begin{bmatrix} y_1 \\ y_2 \\ y_3 \end{bmatrix}$, meaning it lives in $\mathbb{R}^3$ (3D space).

## Core Geometric Transformations
# Rotation
- Rotating a 2D plane counterclockwise by an angle $\theta$ moves the basis vectors 
$\mathbf{e}_1 = \begin{bmatrix} 1 \\ 0 \end{bmatrix}$ to $\begin{bmatrix} \cos\theta \\ \sin\theta \end{bmatrix}$ and $\mathbf{e}_2 = \begin{bmatrix} 0 \\ 1 \end{bmatrix}$ to $\begin{bmatrix} -\sin\theta \\ \cos\theta \end{bmatrix}$. Thus, the rotation matrix is:
$$R(\theta) = \begin{bmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{bmatrix}$$
In 3D, rotations happen around principal axes:
- Around Z-axis: $$R_z(\theta) = \begin{bmatrix} \cos\theta & -\sin\theta & 0 \\ \sin\theta & \cos\theta & 0 \\ 0 & 0 & 1 \end{bmatrix}$$
- Around X-axis: $$R_x(\theta) = \begin{bmatrix} 1 & 0 & 0 \\ 0 & \cos\theta & -\sin\theta \\ 0 & \sin\theta & \cos\theta \end{bmatrix}$$
- Around Y-axis: $$R_y(\theta) = \begin{bmatrix} \cos\theta & 0 & \sin\theta \\ 0 & 1 & 0 \\ -\sin\theta & 0 & \cos\theta \end{bmatrix}$$

# Scaling

Stretches or compresses coordinates independently along each axis by factors $s_x$ and $s_y$:
$$S = \begin{bmatrix} s_x & 0 \\ 0 & s_y \end{bmatrix}$$

# Shearing
- Tilts space while keeping one axis fixed.
- Shear along x-axis (shifts $x$ by $k \cdot y$):
$$Sh_x = \begin{bmatrix} 1 & k \\ 0 & 1 \end{bmatrix}$$
- Shear along y-axis (shifts $y$ by $k \cdot x$):
$$Sh_y = \begin{bmatrix} 1 & 0 \\ k & 1 \end{bmatrix}$$

# Reflection
- Mirrors coordinates across an axis:
Across y-axis: 

$\begin{bmatrix} -1 & 0 \\ 0 & 1 \end{bmatrix}$

Across x-axis:

$\begin{bmatrix} 1 & 0 \\ 0 & -1 \end{bmatrix}$

# Composition of Transformations
- Applying transformation $A$ followed by transformation $B$ to a point $\mathbf{v}$ is written as:
$$\text{Result} = B(A(\mathbf{v})) = (B \cdot A)\mathbf{v}$$
Note: Matrix multiplication is not commutative ($BA \neq AB$). Order matters deeply—rotating then scaling yields a different geometric state than scaling then rotating.

## Eigenvalues, Eigenvectors, and Eigendecomposition
- The Mathematics
Most vectors change direction when multiplied by a matrix. An eigenvector $\mathbf{v}$ is a non-zero vector that only changes by a scalar factor when multiplied by a matrix $A$
$$A\mathbf{v} = \lambda\mathbf{v}$$$\mathbf{v}$ = eigenvector (direction that survives unchanged in orientation)

$\lambda$ = eigenvalue (the scaling factor by which $\mathbf{v}$ is stretched or shrunk)

To find eigenvalues, we solve the characteristic equation:

$$\det(A - \lambda I) = 0$$

where $I$ is the identity matrix.

