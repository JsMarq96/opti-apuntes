# Funciones quadraticas: descenso de graidente & conjugaod graident

# Recap funciones quadraticas
Nota: no tiene minimo??
En la forma de R^n
$$ f(x) = \frac{1}{2} <Ax,x> - <b,x> + c $$
El comportamtiento depende de la funcion en R depdend e A
- A es positive definiit: f es conveza con un unico minim
- A es negative definiteL es concaba sin un minimo
- A tiene eigenvalues mixtos positivos y negativos: f es concava en unalguas sdirecciones y convexas en otras. No tiene minimo
- A = 0: f es una funcion affine y no tiene minimo si b = 0
- A es positivo semidefinitiva: f es convexa, pero puede que no tenga un minimo finito (A=0 es un positivo semidefinido)

Nos centraremos en las positivas definitivas: convexas!
A partir de ahroa suponemos que A es positiva semidefinitiva (sin eigenvalues negativos)

## Minima de una forma deifnitiva positiva de formas quadraticas
Empezamos provando la condicion de primer orden para la optimilidad, que es que $\triangledown f(x^*) = 0$
 Entonces:
 $$ \triangledown f(x^*) = \triangledown(\frac{1}{2} <Ax,x> - <b,x> + c) = Ax^* + b = 0 $$
 Es decir: $x^* = A^{-1} b$ pero eso significa que solo se puede resovler si A es invertible!
 Si A tiene zero eigenvalues, A no es invertible, y la ecuacion solo tiene una solucion b en su iamgen.

Problema: Invertir matrices es caro!
Gauss jordan tarda $O(n^3)$
Nuevos metodos mas aelegantes como Coppersmith-winograd tarda $O(n^{2.37})$ 
Eso es prohibitivo si N es grande! Hoy vamos a ver metodos apra resolver un sistema lineal

# Gradient descent for Quadratic functions
Asi es el graident desncet step
$$ x_{k+1} = x_k - \alpha_k \triangledown f(x_k) $$
Y el gradiente es $\triangledown f(x) = Ax-b$, entonces es:
$$ x_{k+1} = x_k - \alpha_k (Ax-b) = (I - \alpha_k A) x_k + \alpha_k b $$
Y si, el paso es contante
$$ x_{k+1} = (I-\alpha A)x_k + \alpha b  = (I - \alpha A) ((I-a\alpha)x_{k-1} + \alpha b) + ab$$
$$ = (I - \alpha A)^2 x_{k-1} + \alpha (I -\alpha A)b + \alpha b = ... = (I - \alpha A)^k x_0 + a \sum^k_{i=0}(I-\alpha A)^i b$$
Y cuando $\alpha < 1/\lambda_{max}(A)$ enteonces $\lambda_{max}(I - \alpha A) < 1$ que implica que $(I-\alpha A)^k x_0$ -> 0 (tiende a 0) la suma geometrica de matrix converge a
$$ \alpha \sum^\infty_{i=0} (I - \alpha A)^i b = \alpha(\alpha A)^{-1} b $$
Esto se lla ala expansion de la serie de newman parala matrix $(\alpha A)^{-1}$

Esto implica que si el paseo del gradiente es menor que el mayor eigenvalue de A, el dencenso de graidente converge!

Pero... como de rapido?

### Convergence speed
Siendo $L = \lambda_\max(A)$ y $\mu = \lambda_\min(A)$ y $\kappa = \frac{L}{\mu}$ el numero condicional de A. Suponiendo que $\alpha \leq \frac{1}{L}$ lasiteraciones del descneso de graidiente satisffacen las condiciones de limites (en el pdf pag 12)

Es decir, el faster rate se consigue si $\alpha = \frac{1}{L}$ in the case we have $\alpha \mu = \frac{1}{k}$

La convergencia lineal se consugue si $\mu > 0$ y la velocidad depende en el numeor de condicion $\kappa$ y puede ser muy lento si kappa es grande.

Si esto se sabe porque se fine tunea manualmente en ML el paso? evitar overfitting?? 

hasta pag 18


