# Linear Algebra

## Why linear algebra

* Translation and manipulation of space and data
* We usually understand 3D objects such as a primitive cube as a single mass but the reality is that they are made of points. A cube has at least 4 points. Each point has it whole XYZ coordinates. How can we perform transformations across all these points. The answer is using matrices/linear transformation. A matrix, in a way, is like a rule, that can be apply to each point.

| Item                                   | Cheat                                                                                                                                                                   |                                      |
| -------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------ |
| **Linear Transformation**              | <p><strong>Conditions:</strong><br>1. Origin remains fixed</p><p>2. All lines remain straight </p>                                                                      |                                      |
| Linear Combination                     | <ul><li>Sum of two vectors </li><li>Tip-to-tail method</li></ul>                                                                                                        |                                      |
| Span                                   | <ul><li>Span of 2 vectors is set of all their linear combination</li></ul>                                                                                              |                                      |
| Linearly dependent                     | Remove one point and there is no change                                                                                                                                 |                                      |
| Scalars                                | numbers                                                                                                                                                                 |                                      |
| Composition                            | Product of two matrices in a single action                                                                                                                              |                                      |
| Determinant                            | <p>Scaling factor </p><ul><li>if negative, orientation is flipped</li><li>det(m₁m₂) = det(m₁)det(m₂)</li></ul>                                                          |                                      |
| **Dot product**                        | if dot product of 2 vector = 0, then vectors are perpendicular                                                                                                          |                                      |
| **Cross product**                      |                                                                                                                                                                         |                                      |
| Basic vectors                          | <p>i-hat - unit vector of x<br>j-hat - unit vector of y</p><ul><li>The basis of vector spaces is set of linearly independent vectors that span the full span.</li></ul> |                                      |
| Eigenvalue                             |                                                                                                                                                                         |                                      |
| Eigenvector                            |                                                                                                                                                                         |                                      |
| Rank                                   | <p>Rank 1: Single line</p><p>Rank : 2D Plane</p><p>Rank 3: 3D plane</p>                                                                                                 |                                      |
| Duality                                | Natural but surprising correspondence                                                                                                                                   |                                      |
| Cramer's rule                          |                                                                                                                                                                         |                                      |
| Gaussian Elimination                   |                                                                                                                                                                         |                                      |
| Translating between coordinate systems | <ol><li>Translate to your own basic vectors</li><li>Perform linear transformation</li><li>Inverse translate basis vectors back to original</li></ol><p>A⁻¹MA</p>        |                                      |
| Identity matrix                        | Multiplying any matrix by the _identity matrix_ results in the same matrix.                                                                                             | <p>1 0 0</p><p>0 1 0</p><p>0 0 1</p> |
| Kernel                                 |                                                                                                                                                                         |                                      |
|                                        |                                                                                                                                                                         |                                      |

#### Unit Vector — a vector whose length =1

$$
u = v/||v||
$$

**Tips**

* Do one transformation at a time from right to left
*
