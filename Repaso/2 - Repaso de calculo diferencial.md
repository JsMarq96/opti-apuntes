Repaso de calculo diferencia bajo la lupa de optimizacion unconstrainded (sin limitaciones)
Es decir:
$$ \min_x f(x)$$
x es un vector real de N, y f es una muncion continua y diferenciable; y al ser sin limitacioens, no ponemos restricciones en los valroes de x

La idea es encontrar un minimo global, es decir un point para el que
$$ f(x^*) \leq f(x)\ \ \ \forall x \in R^n $$
pero, hay muchos algortimos que solo pueden encotnrar un minimo local de f, para el cual
$$ f(x^*) \leq f(x)\ \ \ \forall x \in Nieghbordhood(x^*) $$

## Gradients y Hessianas
Un gradiente esta compuesto por n derivadas direccionales, evaluadas en un pto, que calcula el cambio en cada una de las n direccioens de la funcion. Es un vector que apunta en la direccion en la que la funcion esta incrementando mas rapidamente (steepest ascent). Y de la misma manera, el gradiente negado es la direccion de steepest descent.

La hessiana estudia el cambio en los gradientes. (se escribe con $D^2$)

## Taylor
La aproximacion de taylor es una aproximacion local a una funcion, que se basa en hacer que sus primeras n derivadas coincidan para un punto.

Usando nuestra notacion, podemos escribir la expansion de taylor en grado 2, en un pto x_0
$$ f(x) = f(x_0) + <\triangledown f(x_0), x-x_0> + \frac{1}{2}<D^2 f(x_0)(x-x_0), x-x_0> + o(||x-x_o||^2_2) $$

## Deribadas direccionales
El gradiente esta compuesto por derivadas direccionales en cada direccion $v \in R^N$, y se evalua en un pto $\overline{x}$
$$ D_v f(\overline{x}) = \lim_{h \rightarrow 0+} \frac{f(\overline{x} + v h) - f(\overline{x})}{h} $$
## Ptos estacionarios:
- Un pto estacionario es cuando el gradiente da 0, es decir que no hay cambio en su pendiente
- Puede ser un maximo o un minimo, si y solo si es continuametne diferenciable alrededor del pto que el grad da 0
- Si la hessiana evaluada en el pto x_0 es definitivamente positiva, se trata de un minimo; y si es definitivamente negativa, es un maximo. Pero si sus eigenvalues son negativos y pos, es un saddle point (centro de una pringles vamos). Y si no tiene igenvalores, no hay claisificacion posible.

### Cosas interesantes:
$$ D_v f(x) = <\triangledown f(x), v>$$
Y si aplicacmos esa propieda a todas las direcciones, obtenemos que
$$ \triangledown f(x) = 2A^T(Ax-b) $$
Y si lo evaluamos en un minimo:
$$\triangledown f(x) = 0 \ \rightarrow \ 2A^T(Ax-b) = 0 \ \rightarrow \ A^TAx = A^Tb$$
Acabamos con las normal equations!


## Funciones Quadraticas
Porque son interesantes? 
- Aparecen mucho en porblemas de optimizacion.
- Casi todas las funciones se puede aproximar a funciones cuadraticas con Taylor
- Algunas son convexas:
	- Si lo son, tiene un minimo!
	- Y podemos lelgar al minimo con arg min
- Las conidiciones para saber que son minimos y maximos son bien faicles

Funcion cuadratica en R^n de 1 dim
$$ f(x) = \frac{1}{2} a x^2 + bx + c$$
Formula cuadratica genercia:
$$ f(x) = \frac{1}{2}x^TAx+b^T +c =\frac{1}{2} <Ax,x> + <b,x>+c  $$
Donde A es una matrix simetrica de nxn