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
