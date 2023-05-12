Diapo 5
# Line search methods
Algoritmos que implican moverse en una linea, consiguiendo una direccion y una longitud del paso; para llegar a una meta.

Son metodos iterativos, que a cada paso, genera un nuevo resultado x
$$ x_{k+1} = x_k + \alpha_k p_k $$
- X_k es la posicion inicial
- Alpha_k es el step size
- p_k es un vector unitario con la direccion del desplazamiento

Lo que diferencia a los distintos metodos es como se calculal alpha_k y p_k; ademas de que condiciones tienen.

# Descent directions
Dado un pto en una funcion diferenciable, es lo opuesto a la direccion del gradiente (la pendiente) (es decir, el dot entre los dos es negativo)
$$ p \bullet \triangledown f(x) < 0 $$
Si usamos el descent direction para mover x en la funcion, mejoraremos en algo el resutlado d ela funcion
$$ f(x) > f(x+\alpha p) $$
Esto es tambien uno de los princpios de los primeros terminps de Taylor


### Choosing a step length
- La opcion mas facil: un fixed step. Pero eso no siempre va a funcionar bien: puede ser o una perdida de recursos (converge lentamente), o no converger y quedarse atascado
- Podemos calcularo perfectamente, usnado el exact line search. Para ello comprueba todas las posiblidadades y elige la mejor distancia y direccion (calcula el optimal step length): $\alpha^*_p = \arg \min_{\alpha>0} g_p(\alpha) = \arg \min_{\alpha > 0} f(x + \alpha p)$ pero esto es demasiado caro! Pero si lo ree-escribimos, vemos que la unica manera economica de conseguir el optimal step lenght es cuando el gradiente de f es ortogonal a la direccion de p


### Choosing a step, wolfe's conditions
Clausulas generales a para un good step size:
- Hacer decrecer la funcion
- No son muy pequenos (si no, muchisimas iteraciones)

Las condiciones de Wolfe determinana un rango de alpha que satisface ambas condiciones.
Presetnan las bases para construit un algoritmo lde busqueda  lineal aproximada; con un coste mucho menos que el del optimal line search algo

Tomando una direccion p, y un setpsize alpha que satisface las siguients condiciones:
- Sufficient decrease:  $c_1 \in (0,1): \ \ \ g_p(\alpha) \leq g_p(0) + c_i \alpha g'_p(0)$ <-> $f(x + \alpha p) \leq f(x) + c_i \alpha (\triangledown f(x) \bullet p)$  Esto hace que el alpha es proporcional a el gradiente del punto, y que por lo menos siempre es mejor (es decir, es menos llano el pto) (ojo, como esto esta basado en Taylor, necesito tener en cuenta el error de taylor, en sistemas del mundo real)
- Corvature condition: $c_2 \in (c1, 1): \ \ \ \ g'_p(\alpha) \geq c_1 g'_p(0$  <-> $\triangledown f(x + \alpha p) \bullet p \geq c_2 (\triangledown f(x) \bullet p)$  indica que el slope decremetnara un poco en el punto nuevo.


## Convergencia de los sistemas de busqueda en linea
EL usar las condiciones de Wolfe nos asegura una convergencia
El temorema de Zoutendijk



# Gradient Descente & Newton's method
## Gradiend descent
El algoritmo de busqueda en linea mas sencillo posible.
$$ p_k = -\triangledown f(x_k) $$
$$ x_{k+1} = x_k - \alpha_k \triangledown f(x_k) $$
it can be used with fixed, optimal and approximated step sizes.
Muy usado en achine learning

## Metodo de Newton
Se basa en aproximar f usando su polinomio de Taylor de segunda orden
$$ f(x) \approx m(x) = (expansion\ de\ Taylor\ grado\ 2)$$
Luego, calculamos el punto en el que el gradiente de m(x) es 0, y lo usamos como punto $x_{i+1}$ 
Entonces:
$$ x_{k+1} = x_k - D^2 f(x_k)^{-1} \triangledown f(x_k) $$
Esto intenta raplicar la senal y hacerla mas smooth, mas facil de iterar, usando el polynomio de taylor de grado 2 (una parabola).
El problema que tiene es que dependiendo del punto donde empieza, puede converger en un maximo, no en un minimo!
Ih a hessian is positive, then it is a line search method
$$ p_k = -D^2 f(x_k)^{-1} \triangledown f(x_k) $$
$$ \alpha_k  = 1$$
pag 19



# LAB 2
Image denoising


## Ratio de convergencia en metodos iterativos
OJO: no es lo unico importatne, puede pasar que un metodo sea muhco mas caro de usar

Dada una secuaicna generada por una sucesion iterativa x, con x0, x1, x2... hasta converger a x* (que es el minimizicador de la funcion), este es la convergencia linear
$$ \lim_{k \rightarrow \infty} \frac{||x_{k+1} - x^*||}{|| x_k - x^* ||} = r $$
r es el ratio de convergencia
Tambien se puede expresar como
$$ || x_{k+1} - x^* || > || x_k - x^* || $$
Si r = 0: TODO

Luego tambien esta la convergencia quadratica:
$$ \lim_{k \rightarrow \infty} \frac{||x_{k+1} - x^*||}{|| x_k - x^* ||^2} = M $$

Si r es un numero Real mayor que 0, siginifica que hay un numero de pasos FINITO para llegar al minimo.


### Orden de convergencia
definimos el error de convergencia como $e_k = || x_k - x^* ||$



## Ratio de convergencia para el descenso de gradiente
$$ \kappa = \frac{\lambda_{max}}{\lambda_{min}} \geq 1 $$
Cuanto mas se aporima kappa a 1, la convergencia es mas grande (y las lambdas son los eigenvalues de $D^2 f(x^*)$ (es la hessiana??)

## Ratio de covnergancia de metodo de Newton
Si el emtodo de newton esta cerca del minimo, la convergencia esta asegurda y es muy rapida (entre en super convergencia (que es convergencia cuadratica))
