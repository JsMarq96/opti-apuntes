Como garantizamos la existencia de una solucion dado un problema?

En algunos problemas convexos, podemos garantizar la existencia de solutiones.
Si el problema es ESTRICTAMETNE convexo, podemos grantizar que existe una solution unica
Si el problema es estricatmente convezo, y restringimos las soluciones en sets convexos podemos garantizar que exisitira una solucion unica y que existe!

Pero si el problema es convexo pero no diferenciable, tendremos que usar los principio de dualidad

Un ejemplo de optimizacion convexa limitada, es encontrar el minimo de una funcion decreciente, en el radio alrededor de un pto.

# Sets convexos
Un set de Rn es convexo si dados 2 ptos cualquieras dentro del set, generan un segmento que no se sale del set

### Set afin
Un set es afin si contiene no un segmento, si no una linea.
Por ejemplo, un set de las posible soluciones de un sistema lineal de equaciones

La interseccion de n sets convexos, da un set convexo; pero la union no tiene porque.

No enteindo estrictametne convezo

Una funcion doblemente diferencible es conveza si y solo si la hessiana de f es positiva semi-definitiva para todo los puntos dentro de su subsets convexo, pero si todos los eigenvalores son positivos f es estictamente convexa

Por ejemplo, suna funcion quadratica, si una matrix A es simetrica, es convexa si A es positivamene definitiva

Una funcion de least squares es convexa para cualqueir matriz A

## Condificion sufficeinte y neceastia para convexidad
TODO REVIEW ESTO


# Minimizacion de funcioens convexas en Sets convexos
COn constraints o limitaciones en la solucion.

Las funciones convexas en bounded and clsoed convex ses tiene minima
## Mirarse la clase online



## Constrained optimization

Limitar el espacio de soluciones en funcion de las necesidades del problema

Es limitaciones vienen a modod de funciones que son de inecualidad o de ecualidad, sobre una solution

Para resolvoerlo estableceremos una reglas que ha de cumplir nuestra solucion.

## Multiplicador Lagrangiano
Podemos ver el gradiente como una funcion que nos da un vector perpendicular a el controno de la funcion en un punto.

Y dos funciones se intersectan en su contorno en un pto cuando en ese punto los gradientes estan opuestos entre ellos
Se puede escribir como $\triangledown f(x) = \lambda \triangledown g(x)$ 
El lambda indica un cambio de signo o magnitud, pero la direccion es la misma y se le llama, el multiplicado de lagrange

Este es el teorema del multplicador lagrangiano, donde g se le llama restruccion

En base a esto construimos el Lagrangiano de nuestro problema:
$$ \mathcal{L}(x, \lambda, \nu) = f(x) - \lambda g(x)  - \nu d(x)$$

y para garantizar la optimalidad de la condicion estan las Condiciones Karush-Kuhn-Tucker (o KKT)

## Karush-Kuhn-Tucker
1) Estacionalidad primordial: $\triangledown_x \mathcal{L}(x,..) += 0$ 
2) Feasibilidad primal $c_i(x) \geq 0$
3) Feasiblidad primal (igualdad) $d_i(x) = 0$
4) Positividad dual $\lambda_i \geq 0$ por la orientacion de las constraint
5) Complementary slackness $\lambda_i c_i(x_0) = 0$

Estas condicioens son necesarias!!!

Para resolver el problema intenamos minimizar x, y maximar los multiplicadores de lagrange.
Esto hace que la solucion sea un saddlepoint que x y los multiplicadores tiene que cumplir

## Constraints
- Que es un interior point?
Es cuando un valor x esta dentro de la region de feasiblidad de una constraint
- Cuando esta una constraint activa?
Cuando tenemos solucion dentro de la region de feasibilidad de uns constraint decimos que la activa. una solucion solo puede ser optima si activa todas las constraints

