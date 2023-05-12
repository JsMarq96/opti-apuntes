When optimizing a problem throught a goal, the conditions can almos always be represetend as a (somatimes linear) system of equations.

$$ \min_{u \in W} E(u) $$
Being u a solution in the space W, need to be the maximun or minimun.
We can assume that if u is a etremum, u has to satisfy a differential equation, names the Euler-Lagrande equation.
	Usually we discrtize the differential operator, usually results in a ser of equation $Au = b$
	This can easily be solved, if the system is solvable, and if A is invertible.

A system can have multiple solutions, and not all of them are optimal.

## Data fitting
We have m samples, with a form of input t (with n dimensions), and output y a scalar
Find the relationship between input and output in a model $y = f(t)$ 

But in teh real world there is never a perfect relationship:
$$ y_i = f(t_i) + noise_i$$
And we can asume that the relationship f is a polynomial relationship, while looking at the data.
in order to aproximate f, we will solve this, as a regression problem.

#### Linear regression
Fit the data to a linear equation $f(t) = at + b$

Assuming a and b are know, or we have a first guess.
We can calculate the the error of a date point as
$$ d_i = f(t_i) - y_i $$
And the total error function is
$$ E(a,b) = \sum_{i=1}^m d_{i,j}^2 = \sum_{i=1}^m(f(t_i) - y_i)^2 $$
Usually, the error d is called residual, and it is not possible to be 0 for all the data points

This is called a least squares problem, and it has a colsed-form solution.
#### How do we solve it??
First, we can write it as a set of form of equations.
$$ a t_1 + b - y_1 = d_1$$
$$ a t_2 + b - y_2 = d_2$$
$$...$$
$$ a t_m + b - y_m = d_m$$
A set of m system of linear equations, and as so, we can write it as a matrix
$$\begin{bmatrix} t_1 & 1\\ t_2 & 1  \end{bmatrix} \times \begin{bmatrix}  a\\  b  \end{bmatrix} - \begin{bmatrix}  y_1\\  y_2
\end{bmatrix} = \begin{bmatrix}  d_1\\  d_2
\end{bmatrix}$$
And we want to minimize the sum of d_i
 This is a problem of linear regression of the form $Ax -b = 0$

$Ax-b = d$ can be solved with using the leas squares one shot solution, that is if $A^TA$ is invertible
$$ x = (A^T A)^{-1} A^Tb $$

This can be solved to sovle non-linear equations, but only if the coefficients are linear (aka the unkowns)


### General formulation
Given the data: $(t_1,y_1), ..., (t_m, y_m)$ where $t_i \in R^p$  $y_i \in R$
And functions: $\phi_1(t), .., \phi_n(t)$ we model
$$ f(t) = \sum_{j=1}x_j \phi_j(t) $$
Compute the values fo that $f(t_i) = y_i$
- $A = (\phi_j(t_i))^{m,n}_{i=1,j=1}$
- $x = (x_1,..., x_n)^T$
- $b = (y_1, .., yy_m)^T$

We need to solve $\min_x || Ax-b||^2_2$


## Linear algebra preliminaries
 Objetive:  solvinf the "normal" equationss", and that is solving $\min ||Ax-b||_2^2$
and that is like solving
$$ A^TAx = A^Tb $$
Only if the matrix $(A^TA)^{-1}$ existis, $x=(A^TA)^{-1}A^Tb$ 

### Basics
- Vectors
- Vector Spaces
- Transpose matrices
- IMPORTANT: $(AB)^T = B^T A^T$
- Dot or scalar product: $<x,y>$ also called inner product
- norm or length $||x||$
- Change a matrix side of an equation: $<Ax,y> = <x, A^Ty>$
- $\cos(angle(x,y)) = <x,y> / ||x||\ ||y||$
- vector are orthogonal if the dot is 0
- and are orthonormal if there ar all unit length, and orthogonal
- $P_xy = (<x,y>\ / \ <x,x>) * x$
- Image?? Kernel??
- Kernel: a set of vector that maps a matrix A to 0
- Iamge: the colum space of a matrix
hasta solving a linear system 32




# Repaso: Algebra lineal
Dado un porblema de optimizacion, usamos un enfoque variacional, que suele implicar un sistema algebraico de ecuaciones
Dado $$ \min_{u\in W} E(u)$$
- Necesitamos encontrar un extremum (maximo o minimo, en funcion del problema.). Ese extrenum u satisface una serie de ecuaciones diferenciales (llamads de Euler Lagrange)
- Generalemente, lo problemas se pasan a una forma $Au = b$

## Data fitting
Dados m muestras $(t_i, y_i),\ i = 1,..., m$ donde t_i es un vector de R^n e y_i es un numero Real

Tenemos que averiguar una funcion que relaciones y e t de tal manera que: $y = f(t)$, pero estas observaciones pueden tener ruido $y = f(t) + noise$

Podemos suponer ciertas cosas, como que f es polinomial

Para resulverlo lo trataremos como un problema de regresion, como por ejemplo, una regresion lineal: $f(t) = at + b$

Si tenemos una idea inicial (o una aleatoria), y medimos la distancia entre las muestras y la linea
Podemos usar eso como residual, o error, para optimizar; aunque si hay ruido, sera imposible llegar a la solucion perfecta! r = 0

Lo podemos plantear como un problema de least squares 9que tiene una solucion cerrada!
$$ E(a,b) = ||Ax-b||^2$$
La solucion de forma cerrada (que solo existe si $A^TA$ es invertible) es $x = (A^TA)^{-1} A^T b$
(ojo, para una regresion lineal, la matriz tiene la forma de 2x2, asi que se puede ahcer a mano)


### Regresion linear
Un dato importante, es la aunque la funcion no sea linear, los coeficientes si que lo son. (tenemos la entrada, y el resultado, asi que da igual si son polinmois). En este caso las incognitas son los coeficientes.

A son las entradas

La idea es usar least squares para encontrar la mejor solucion posible
$$ \min_x \sum^m_{i=1} (y_i - \sum^n_{j=1} k_j \phi_j(t_j))^2$$


## Notaciones de Algebra lineal
- Transponer es rotar una matriz por la diagonal:
$$ (AB)^T = B^T A^T $$
$$ <Ax,y> = <x, A^Ty>$$
$$ <Ax, y> = (Ax)^t y = x^TA^Ty = <x,A^Ty>$$
- 2 vectores son orthogonales si $<x,y> = 0$
- Y son orthonormales entre si encima $||x||=1$
- La proyeccion de y en la direccion de x es: $P_x y= \frac{<y,x>}{<x,x>}x$
	- Si x es normal, el dot de y y x da la longitud de la projeccion
- La imagen de una matriz son todos los vectores que puede producir una matriz como un sistema lineal
- El kernel son los vectores que al transformarlos por una matriz dan 0
- Un complemento orthogonal son todos los vectores que son orgonoales a otro vector
- rank(A) te devuelve el numero de columans que son linealmente independientes.



# metodos director para resolver un sistema lineal
Dado un sistema lineal de ecuaciones: $Ax=b$ en la que A es mxn matrix
3 posiblidades:
- Mas ecuaciones que incognitas (m >n)
	Si b no esta en la Im(A) no hay solucion
	Si b esta en Im(A) y el rank(A) = n hay una solucion
	Si b esta en Im(A) y el rank(A) < n hay infinitas soluciones
- Tantas ecuaciones como incognitas (m=n)
	Si rank(A) = n, A es invertible, pero igual que el otro caso
- mas incognitas que ecuaciones (m<n)
	si b no esta en la imagen, no tiene solucion
	si b esta en la Im(A) el sistema tiene infintas soluciones



# SVD
Singular value Decomposition, descompone una matriz en sus componentes mas importantes, similar a una eigendecomposition; pero mas facil de aplicar.
Todas las matrices reales tiene una SVD, que lo descompone en vectores singualres y valores singulares.

Se puede aplicar a matrices no cuadradas (la igendecomp no)
Dada una Matrix A mxn
$$ A = U \Sigma V^T$$
- U es una base ortogonal de mxm (left singular vects)
- V es una base ortogonal de nxn (right singular vects)
- $\Sigma$ es una matriz diagonal que tiene los valores sigunlares en la diagonal de tamano mxn

El nuemro de valores singulares que no son zero es = rank(A)

Si descomponemos A:
- Los Left signualr vectors de A (U) son los eigenvectors de $AA^T$
- V son los eigenvecotres de $A^TA$
- Los valores singulares son las raices cuadradas de los eigenvalores de $A^TA$

### Calcular la pseudoinversa
Se usa para calcular la inversa de matricez que no son cuadradas, asi que lo usamos para calcular la pseudoinversa. 
la meta de la matriz pseudo-inversa C es dado $Ax=b$ conseguir que $x=Cb$ pero en funcion de A, puede que esta matriz no exista:
- m > n: puede no tener solucion
- m < n: puede tener multiples soluciones posibles.
$$ A^+ = V \Sigma^+ U^T$$
la pseudo inversad e Sigma,se calcula invirtiendo los valores no zero, y luego transponiendola

### Como se usa la pseudoinversa
Dada una $A^+$ y $x^* = A^+b$ una solucion,
$A^+b$ es una aproximacion a b en terminos de norma euclidiana; es decir se correponde con una least squares solution; solo si el sistema no tiene solucion!
$$ x* = arg\min_{x \in X} ||Ax-b||_2 $$
Y si tiene solucion, selecciona la minima de menor normal (la solucion mas chiquita):
$$ x* = arg\min_{x \in X} ||x||_2 $$

# Least squares
Incluso cuando el sistema no tiene solucion (b no esta en la imagen de A), podemos encontrar una solucion lo suficientemente buena!
Elegiermos la solucion mejor de las posibles:
$$ \min_{x \in R^n} ||Ax-b||^2_2$$
Intentara encontrar un vector v que este dentro de la imagen de A, pero que sea lo mas cercano posible a b.

Para ello la solucion es projectar b en la imagen de A; y con ello resolver luego $Ax = Pb$

#### Proceso
1) elejimos un vector $\overline{x}$ el cual es el mas cercano a b, en la imagen de A
2) Luego calculamos la proyeccion ortogonal de b en Im A (que es$A\overline{x}$).

Siendo $b \notin Im(A)$, projectamos b en Im(A), usando una proyeccion P
Pb = projeccion de b en Im(A) y Qb un vector ortogonal a Im(A), y la diferencia ente b y Pb

Esto implica (?) que para todas las x de la imagen, como no podemos aproximarnos a b, la lo maximo que nos podemos hacercar es la distancia de Qb, $||Ax-b||^2_2 \geq ||Qb||^2_2$ 
Incluso el minimo respetara esta igualdad.

Dado $Pb \in Im(A)$, $\overline{x}$ es la solucion tal que: $A\overline{x} = Pb$:
$$ ||Ax-b||^2_2 = ||A\overline{x}-Pb||^2_2 + ||Qb||^2_2 = ||Qb||^2_2$$
$$ \min_{x\in R^n} ||Ax-b||^2_2 = ||Qb||^2_2 \ \ \ \ \& \ arg\min_{x\in R^n}||Ax-b||^2_2 = arg \min_{x\in R^n}||Ax-Pb||^2_2$$
Es decir, el mejor resultado que podemos tener es el de la diferencia entre Pb y b; y el problema se puede sustituir por minimizar Ax-Pb

$$ A \overline{x} - b - A \overline{x} -Pb - Qd = -Qb \in (Im(A))^\perp = Ker(A)^T$$
Entonces
$$ A^T(A\overline{x}-b) = 0 \ \ \rightarrow\ \ A^TA\overline{x} = A^Tb $$
A $A^TA\overline{x} = A^Tb$ se le llama las ecuaciones normales del Least squares problem, y si lo resolvemos conseguiremos overline x

La gran ventaja de resovler esto vs Ax=b es que $A^TA$ es una matriz cuadrada, y si es invertible (su rango es igual que el numero de filas) podemos resovler el sistema!
$$OJO:\ rank(A^TA) = rank(A)$$
Entonces si $A^TA$ de tamano nxn, tiene rango n, la solucion es:
$$ \overline{x} = (A^TA)^{-1}A^Tb $$


Pero... y si no tiene rango n?? La ecuacion normal tiene solucion? Si, pero no es unica. Podemos sacarla con SVD!
1) Descomponemos A $A = U \Sigma V^T$
2) $\overline{b} = U^T b$
3) Formamos el vector y, tal que cada elementos sea $y_i = \frac{ \overline{b}_i }{\sigma_i}$ siento $\sigma_i$ el valor singular del vector i (si elvalor sigular es 0, y_i se deja a 0)
4) Entonces la solucion puede escribirse como $\overline{x} = Vy$

### Resumen de Least squares
- Minimiza un problema consiguiendo un vector para que la norma sea la minima posible
- La solucion se correponde con poryectar el vector de solucion b en Im A; como si calculamos la proyeccion P y encontrar un x tal que Ax = Pb
- Pero en la practica resolvemos $A^TA\overline{x} = A^Tb$
- Si el rango de A es n tenemos una solucion cerrad $\overline{x} = (A^TA)^{-1}A^Tb$
- Nota: miramos que $Pb = A\overline{x} =  A(A^TA)^{-1}A^Tb$ por lo que $P = A(A^TA)^{-1}A^T$
- Si el rango es menor, podemos usar la SVD y conseguir una solucion


