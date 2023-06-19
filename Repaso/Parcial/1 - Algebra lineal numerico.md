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
Es decir, el mejor resultado que podemos tener es el de la diferencia entre Pb y b; y ahora mismo los objetivos seran intercambiables.

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



# Mid Repaso
(AB)^T=B^TA^T

## Resolviendo sistemas lineales
Dado un sistema lineal Ax=b y A tioene un tamano de mxn (m es el numero de equaciones, y n el numero de incognitas)
- mas ecuaciones que incognitas m > n:
	- Si b no esta en la imagen, no tiene solucion!
	- Si b esta en la image
		- rank(A) = numero de incognitas m, hay 1 solucion!
		- rank(A)< # de incognitas hay infinitas soluciones
- Si m=n se aplican los mismos casos, pero A es invertible!
- si hay mas incognitas que ecuaciones:
	- si b no esta en la imagen, no hay solucion
	- si b esta, hay infinitas soluciones


### SVD
Descompone una matriz en valores singulares y vectores singulares. Una version generica y mas aplicable que el eigendescomposicion, ya que no necesita que la matriz sea cuadrada.
$$ A = U\Sigma V^T $$
U: mxm V: nxn \Sigma: mxn
Hay tantos valores singulares como rango tiene una matriz

El mejor uso que tiene es que se puede usar para casi casi generalizar la inversion de matrices a matricers no cuadradas.

Supongamos que tenemos Ax=b y C es la inversa de A, podemos x = Cb.
Esto esta guay, pero depende de la esctructura y planteamiento del problema!

### pseudoinversa
Lo que es guay es que incluso si no tiene una solucion el sistema, o si tiene multiples soluciones, la pseudoinversa nos ayuda a encontrar una solucion sensible!
La pseudoinversa se puede ver como la aproximacion mas cercana a b en terminos de la norma euclidiana, asi que se correspondria con la solucion de un problema de least squares!

OJO: si no hay solucion, esto dara la solucion de least squares, pero si el sistema tiene soluciones, entonces el resultado es la solucion de norma mas chiquita.


### Pero.. como? Y porque?
Imagia que tenemos un problema de least squares como Ax=b, pero el problema es que b no esta en la imagen de A, asi que no tiene solucion!
Entonces, intentaremos aproximarla, dejarla lo mejor que podemos, minimizando la diferencia de least squares.

Como podemos solucionar esto? Pues si proyectamos b a la imagen de A, nos podemos acercar, de manera de que el nuevo problema sea Ax = Pb, siendo P la matriz de proyeccion a la Im(A). Este vector Pb lo llamaremos x*, que es el vector mas proximo de Im(A) a b.

para esto, calcularemos la proyeccion ortogonal de b en la Imagen de A.

esto implica que b = Pb + Qp, siendo Qp el error o distancia con b de la proyeccion d b
min||Ax-b||^2 = ||Ax*-Pb||^2 + ||Qb||^2 = ||Qb||^2 (porque Pb y Ax* es lo mismo, si alzanzamos la solucion)

Y si desarrollamos Ax* = n = Ax*-Pb-Qb = -Qb  = KernA^T
Y acabamos con las ecuaciones normales del least squares problem.
Si las resolvemos, encontraremos la solucion del sleast squares.

Y si el rank(A) = n (y la matriz A^TA es nxn), podemos resolverlo en 1 one shot con x* = (A^TA)^-1 A^Tb.

Y ojo, si miramos esto Pb = Ax* = A(A^TA)^-1 A^Tb, el cual es la proyeccion ortogonal de b en Im(A)

Pero... Y si el rango es menor que n?? Eso significaria que AtA no es invertible, entonces no podriamos resovlerlo one shot.

Podemos hacerlo con SVD!
1) Aplicamos SVD a A
2) calculamos b^ = U^T b
3) Luego calculamos y, que esl la divicion de b^ por cada valor singurar de su posicion
4) calculamos x*^ = V y
