Given a system of linear equations $Ax = b$, where A is a m x n matrix
There are 3 positiblities:
- More equations than unkowns (m >n)
- As many equations as unknows (m = n)
- More unkows that equations (m < n)

# More equations than unkowns (m >n)
- if $b \notin Im(A)$, so there is no solution 
- if $b \in Im(A) \ \ rank(A)=n$, there is only one solution
- if $b \in Im(A)\  \ rang(A) < n$ there is an infinite number of solutions

# AS many equations as unknows:
Since the rank is n, it means that A in invertible

# More unkownws than equations
-  if $b \notin Im(A)$, so there is no solution 
-  if $b \in Im(A)$, so the system has infinitely many solutions (rank(A) <= m < n)



# SVD
Similar to an eigendecomposition; but decomposes in singular vector & singular values
- Every real matrix has a simgular value decomposition, even if the matrix is not square.
Given a matrix A of size m x n it can be factores into
$$ A = U \sum V^T $$
- U an mxm ortohogonal basis matrix (the columns are an orthonormal basis of R^m) aka left-singular vectors
- V is a nxn octhogonal amtrix (its columsn are a orthonormal basis of R^n) aka right singular vectors
- $\sum$ is an m x n rectangular diagonal matrix that only has non-zero values in the diagonal aka singular values.

### SVD and the eigendecomposition of $AA^T$
The left singular vector of A (U) are the eigen vectors of $AA^T$
-  d
- d
- d
So:
- $A^TA = VDV^T$
- $AA^T =UD^~ U^T$ 


#### IMPORTANT: we ccan use to partially generalize matrix inversion in non-square matrices
- Dimensionality reduction (PCA)
- Data denoising
- Pseudo inverse

### Pseudo inverse calculation
If A is taller than its wide (m > n) it might not have a solution
If A is (n > m) more inkwones tha tequations it coul have muptiple possible solutions
But the pseudoinverse can help on both cases

$$ A^+ = V \sum^+U^T $$
And the pseudoinverse of $\sum$ is obteined by taking teh reciprocal of tis non-zero elemtns, and then the transpose of the resulting matrix.
$$ x^* = A^+ y $$
### Ax=b has no solutions
If Ax=b has no solutions, then $Ax*$ gives the clsoes approximation b; and it corresponds to the least-squares solution:
$$ x^* = \arg \min_x ||Ax-y||_2 $$

### Ax=b has multiple solutions
if then, the pseudoinverse selects the minimun-norm solution. Given a set X of solutions of Ax=b; the pseidoinverse satiefies:
$$ x^* = \arg \min_{x \in X} ||x||_2 $$

# Back to the problme
Even if tehre is no solutions, we want to find a good enought one.
Apxorimate a solution given a numerical process

pagina 50 leccion 3