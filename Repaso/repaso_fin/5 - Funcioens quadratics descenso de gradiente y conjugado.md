### Repaso
### Funciones Quadraticas
La variable es al cuadrado
La forma generica en R tiene:
$$ f(x) = \frac{1}{2}ax^2-bx+c $$
En $R^n$ :
$$ f(x) = \frac{1}{2}<Ax,x> - <b,x>+c $$
A es una matriz simetrica
- A es positiva definitiva: f es convexa con un minimo unico
- A es negativa: f es convava sin minimo
- A tiene eigenvalores positivos y negativos: f es concava y convexa, es un saddle point, sin maximo y nimo.
- A = 0: f es afin y sion minimo, si b!=0
- A es positiva demidefinitiva: es convexa, pero puede no tener un minimo infinito.

## Minima de positive definitive
$$ \triangledown f(x) = \triangledown(\frac{1}{2}<Ax,x> - <b,x>+c) = Ax + b = 0 $$
Si A es postiive defintiva, A es invertible y entonces
$$ x = A^{-1}b $$
Pero si algun eigenvalor es zero, A no es invertible, y el minimo solo existe si b esta en la imagen de A.

Peero inverti A es carisimo, sobretod mientras n crece, entonces se intena de otras manera, usando algoretimos de busqueda en linea

# Descenso de gradiente
$$x_{k+1} = x_k - \alpha_k \triangledown f(x_k) = x_k - \alpha_k (Ax_k - b) = (I - \alpha_k A)x_k + \alpha_k b$$
### Convergencia
Siendo L el eigenvalor maximo de A, $\alpha < \frac{1}{L}$ y conforme mas se hacercque el valor de alpha, mayor sea l convergenica

L es el mayor eigenvalor, y mu es el minimo

Es decir la convergencia dependera del planteamisnedo del problema. 


## Exact line search
Thought experiment
Escogeja la longitud y direccion perfecta para cada paso, porque tenemos los valores perfectos de referencia en el residuo: $r = Ax-b$

Observamos que las direcciones de busqueda son ortonogonales!

# Conjugate gradient
Tiene 3 pasos hasta llegar al metodo de gradiente conjugado. Mnimizar una funcion cuadratica:
$$ f(x) = \frac{1}{2}<x, Ax> - <b,x> + c $$
#### Metodo de direcciones ortogonales
La idea es solamente usar n direccioiens ortogonales, una detras de otra (lo cual suele dar lugar a un zigzag). La cosa es que cada direccion solo se puede usar 1 vez

El problema de este sistemas es que para tomar las decieioens correctas necsitamos el valor optimo de x, para que funcione, porque lo usamos para cualcular el error e
$$ e_i = x_i -x^*$$
$$\alpha_i = -\frac{<e_i,d_i>}{<d_i, d_i>}$$
Entonces elegimos d_i tal que el error sea el menor

#### Metodo de las direcciones conjugadas
Partiendo de que A es una metriz simetrica y definitavmente positiva de tamana n x n.
Se dice que dos vectores son conjugados si
$$<v,Aw> = 0$$
Estos vectores conjugados o A-orthoganles, represetan que son angulos rectos en el espacio local de la matriz A.

Tomamos n direcciones conjugadas, y la idea es eocntrar la solucion optima en n pasos, y el paso es
$$x_{i+1} = x_i + \alpha_i d_i $$
Eso significa que todos los pasos son direccioens conjugadas a ale primero
Eso significa que el paso es:
$$ \alpha_i = -\frac{Ae_i, d_i}{<d_i, Ad_i>} = -\frac{<r_i, d_i>}{<d_i,Ad_i>}$$
Lo cual signicia que para calcular el paso necesitamos el resto, no el error! Por lo que es usable
El resto se calcula:
$$ r_i = Ax_i - b = Ae_i = A(x_i - x^*) $$

Esto es guay, pero como se calculan las bases conjugadas??
La idea es que usamos el Proceso de Gramm-Schmidt en la base u, para conseguir la base d (por cada iteracion!)

El problema es que es muy caro computacionalmente y de memoria, asi que conjugamos una bases que esta formada a partir de los gradientes de f
$$ u_i = -\triangledown f(x_i) = -r_i $$
Usando eso como parte, podemos hacer una parcializacion del metodo de gram shcmidt, de esa manera, es mucho mas barato de calcular.

A RELLENAR

Esto singincia que el coste de cada iteracion es solo un producot matrix-vector Ad_i

Pero a costo de exactitud y estabilidad numerica, esto hace que cuantas mas iteraciones, el error se acumula y dejan de ser conjugadas y se pierde la convergencia exacta.

iugalmente, la convergencia es mas rapida en ill posed problems, y no se suele usar todoas la n direcciones.

