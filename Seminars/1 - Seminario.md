# 1

Primero $A^TA$ y luego $A^TA - \lambda$ 
$\det(A^TA - \lambda) = 0$

## Compute SVD
$$ A = U \Sigma V^T $$
1) $A^TA$
2) $P_{A^TA} = \det(A^TA-\lambda Id)$
3) Singular values $\lambda$ -> $\sqrt{\lambda_1} = \delta_1$
4) Find V: 
	1) For each $\lambda$ $E_i  = N(A^TA - \lambda_i Id)$ (N is null space) -> $v_i$ 
	2) Normalizamos cada $v_i$
	3) Construimos V, orenador por columnas con v, empezando con la que tiene el $\lambda$ mas alto, y acabando con la que menos
5) Find U:
	1) $u_i = \frac{Av_i}{\delta_i}$
	2) $u_i = A \frac{v_i}{\delta_i}$
	3) Rellenar U usando u, empezando por el mayor $\lambda$ en la derecha (igual que V)
Caso $AA^t$
Calculamos primero U, y ordenamos  de la misma manera
Y encontramos V de la misma manera

#### Cuando elegir entre $A^TA$ o $AA^T$
La que tenga menos dimensiones!

### Normal equations of Ax=b
- $A^TAx = A^Tb$
### Pseudo inverse of A
$A^+ = V \Sigma^+ U^T$
$\Sigma ^+= \Sigma^T$


# 2
$$ \min_x ||Ax - b||^2 $$
a) $A^TAx = A^Tb$ 
$$ \overline{x} \in \arg \max_x || Ax-b||^2 \rightarrow A^TA\overline{x} = A^Tb $$
b) Depends on the rank of A, the number of solutions, but $\overline{x} = A^Tb$ is always a solution
And it corresponds to the smallest vector in the solution (the lowest eigenvalue??)

c) Compute the SVD
Orthogonal projection en Im(A) ($E = Im(A) \oplus ^\perp Ker*A^T)$

$$\begin{pmatrix}  
-1 & 1 & ll 0\\  
0 & -1 & 1 \\
0 & 0 & 0
\end{pmatrix}$$
## 3
$$ \min_x ||Ax-b||^2 $$
a) $E(a,b,c) = \sum^{500}_{i=1} (t_ia + b + c \cos(t_i))^2$
b) $\overline{x} \in \arg \min((Ax-b))^2$ -> $A^TA \overline{x} = A^Tb$
c) $\overline{x} = A^+ b$ <- $A^+ = V \Sigma^+ U^T$

## 4
#### 1)
$$   A = \begin{pmatrix}  
-1 & 1 & 0\\  
0 & -1 & 1 \\
0 & 0 & 0
\end{pmatrix}   $$

#### 2)
There are more unkowns thatn equations & the image can not contain the soultion, since the thir equation is empty, and it cannot return 1
#### 3)
$$ E(x) = \sum^3_{i=1} (A_i x-b_i)^2 = ||Ax-b||^2_2$$
##### 4)
Using least squares with SVD
How many solutions for a general matrix A?
- Rank(A) = n -> $A^TA$ invertible -> 1 solution
- rank(A) < n -> $A^TA$ not invertible -> infinte numebr of solutions


##### 5) Rank??
Rank 2 -> inifite solutions
Como lo allanos? pseudoinverse


# Notes
### 1)
$\lambda \geq 0$ eigenvalues of $A^TA$
$\exists x \ \ AA^Tx = \lambda x$
$A^TA(A^T x) = \lambda (A^Tx))$ -> $A^Tx$ eigenvector from $A^TA$
