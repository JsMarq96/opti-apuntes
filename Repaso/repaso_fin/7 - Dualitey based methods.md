## Dualidad: el teorema de min-max

Partimos de la base de la inecualidad del min-max,  que es
$$\max_y \min_x L(x,y) \leq \min_x \max_y L(x,y)$$
Es decir que el orden del max y min importa, y pueden dar valores distintos

La diferenica de ambos se llama el Duality Gap, y es mayor o igual a 0 
$$ DG = \min \max L - \max \min L \geq 0$$
Y cuando el el DG es 0, a esas soluciones se les llama saddle point. Es decir si existe un saddlepoint, el DG es 0, es una condicion necesaria.

### COndicion suficiente para un saddle point
Usano el teorema del MinMAx the Von Neuman, asumiendo que X e Y sean sets cerrados y convexos, si 
$$x \in X \rightarrow L(x,y)\ is\ convexo\ para\ y \in Y$$
$$y \in Y \rightarrow L(x,y)\ es\ convexo\ para x \in X$$
Y tango X e Y estan bounded (limitados?), DG = 0, y L tiene un saddlepoint en la interseccion de ambos sets


## Dualidad Lagrangiana
A la hora de resolver problemas duales con el lagrangiano, vemos que se tiene que minimizar x, pero lambda y nu se tienen que maximizar! Y encima lambdas estan constrained.

A esto se le llama la dual funtion
$$ g_D(\lambda, \nu) = \min_x L(x,\lambda, \nu)$$
Y podemos usarla para escribir el problema original como
$$\max_{\lambda\geq 0, \nu} g_D(\lambda, \nu)$$
(asumiendo que el DG = 0, es decir que no hay preferenia por maximinizacion y minimizacion)
A este problema se la llama el problema dual, y f(x) es la funcion primal, con x siendo la variable primal


# Metodos primales duales y duales, para problemas no diferenciables

Podemos encontrarnos en problemas donde el gradiente no es diferenciable! Puede que Ax=0 no sea diferenciable.
pero usando una variable exta y formulando un problema equivalente, se podria aproximar

## Ejemplo: minimizar esta funcion
$$f(x) = ||Ax||_R + \frac{1}{2\lambda}||x-b||^2_R$$
Pero esta funcion cuando Ax = 0, no es diferenciable, por lo tanto no es continua
La idea es envolver en un dot product la parte no continua, por una neuva variable, y someter esa variable a un operador de maximizacion.
$$||y||_R = \max_{||\xi||_R \leq 1} <y, \xi>_R$$
Apl;icamos esto, lo cual nos da H
$$ H(x,\xi) = <Ax, \xi>_r + \frac{1}{2\lambda}||x-b||^2_R $$
Y
$$f(x) = \max_\xi H(x, \xi)$$
Por lo que, para minimizar f
$$ \min_x f(x) = \min_x \max_\xi H(x,\xi)$$
Esto es ahora un problema minmax

Ahora, para una x fija, H es una funcion concaba
Y para una xi fija, H es una funcion convexa

Asi que cambiamos la funcion min max, por una max min, podemos encontrar un saddlepoint, donde ambos gradientes se encuentran, tal que:
$$H(x_0, \xi) \leq H(x_0, \xi_0) \leq H(x, \xi_0)$$


# Resolver un problema max min
Estan 2 metodos:
- Dual: eliminando x, resolviendo primero la parte min como una funcion de xi, y luego resolver la funcion max que depende solo en xi
- Primal-dual: resolver ambos a la vez, para enconrtar un saddlepoint.



## Primal Dual
La idea es tener dos pasos de gradiente, uno ascendiente para xi, y otro descendiente para x

- $\triangledown_x H(x, \xi) = A^T \xi + \frac{1}{\lambda}(x-b)$
- $\triangledown_\xi H(x, \xi) = Ax$

Pero ojo, para xi, el paso es un projected gradien ascent, porque la maximizacion esta constrained, a que es mayor que 1
Se usan las derivadas direccionales


#### Dual update
Primeor empezamos maximizando xi, pero la cosa es que este paso tiene una constraint de proyeccion, para que la norma sea menor que 1
$$ \xi^{k+1} =  Pc(\xi^k + r\triangledown_\xi H(x^k,\xi^k))$$
Donde Pc es la funcion de proyeccion, que es
$$Pc(\xi) = \frac{\xi}{\max(||\xi||,1)}$$
#### Primal update
Ahora resolvemos el minimizador, con x, usando el resultado del maximizador:
$$ \min_x H(x, \xi^{k+1})$$
En este caso el paso es:
$$x^{k+1} = x^k - \theta \triangledown_x H(x^k, \xi^{k+1})$$

## Dual approach
EN este caso, primero abordamos el problema max min, resolviendo la parte min
Esto es porque esta parte es un porblema de minimizacion unconstrained, con una funcion de objetivo diferenciable.

El minimizador es la solucion de la ecuacion $\triangledown_x H(x, \xi) = 0$
Por lo que se puede escribir como:
$$x_0(\xi) = b - \lambda A^T \xi$$
por lo que podemos sustituir en la funcion original
$$g_D(\xi) = \min_x H(x,\xi) = H(x_o(\xi), \xi) = <Ab, \xi> - \frac{\lambda}{2}||A^T \xi||^"$$
Ahora lo que hay que hacer es maximizar g_D para xi

Esto es un problema cuadratico con constraints, asi que tenemos que resovlerlo con ascenso de gradiente projectado

$$\triangledown g_D(\xi) = A(b-\lambda A^T \xi)$$
Y el paso es
$$ \xi^{k+1} = Pc(\xi^k + r A(b-\lambda A^T \xi^k))$$
Esto nos permite encontrar el dual optimun (xi), que luego lo podemos aplicar para calcular el primal optimum x_0(xi) aplicando el valor conseguido de xi

Una cosa guay es que podemos usar el el duality gap para parar las iteraciones:
El DG se calcula como:
$$ \min_x \max_\xi H(x, \xi) - \max_\xi \min_x H(x, \xi) \geq 0$$
Y su lo aplicamos a estas formulas
$$ \min_x f(x) - \max_\xi g_D(\xi) \geq 0$$
$$ f(x^k) - g_D(\xi^k) > 0$$
Cuando esta desigualdad se cumple, podemos parar (o con un delta muy chiquito)


## Terminar las aplicaciones


# Proceso
1) Calcular el laplaciano L como si fuese normal
2) Establacemos g_D como una funcion de minimizacion x sobre el laplaciano
3) Calculamos x^gorrito, que dara X para un lmabda en concreto, el argmin de L
4) para calcular x gorrito, calculamos el gradiente de L, y lo igualamaos a 0, usando lambda como unica variable
5) Eso nos dara una ecuacion para minimizar cualquier x, para cualquier lambda
6) sustituimos x por x_gorrito en g_D
7) Ahora entramos en maximizacion de g_D