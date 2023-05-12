## Funciones Cuadraticas
Muy usadas, por ejemplo en least squares.
Tambien casi todoas se pueden aproximar mediante Taylos.

En R tienen la forma de: $f(x) = \frac{1}{2}ax^2 - bx+c$ 
Y en funcion de a la funcion:
- a>0 es conveza con un unico minimo
- a<0: es concava sin minimo
- a=0 es una funcion afin, y no tiene minimo si b!=0

En Rn tiene la forma de  $f(x) = \frac{1}{2} <Ax,x> - <b,x> + c$, donde A es una matriz nxn simetrica, b un vector de n, y c un numero real
- A definitivamente positiva: es conveza con un unico minimo
- A definitivamente negativa: conveza sin minmo
- A eigenvalues mixtos, f es concava y convexa en distintas partes, sin minimi
- A = 0, f es afin, y no tiene minimo si b != 0
- A es semidefinitiva (eigenvalores icnluyen 0): f es conveza, peropuede no tener un minimo finito.

## Minimo de una funcion quadratica convexa
Si es conveza, todos sus eigenvalues son positivos.
Si es cierta, significa que el gradiente tiene una posicion que es 0
$$ \triangledown f(x^*) = Ax^*+b = 0 $$
$$ x^* = A^{-1} b $$
pero si A  tiene zero eigenvalues, A no es invertible, y la ecuacion de grad = 0, solo tiene solucion si b esta en la imagen de A, si no, es conveza y pero no tiene minimo!

Pero... Problema! Inverta A es muy caro!!
- Gauss jorgan es O(n^3)
- Los nuevos metodos guays son $O(n^{2.37})$ 

Se necesitan soluciones baratas, y/o aproximaciones

## Descenso de gradiente para funciones Quadraticas
Dada una funcion f quadrativa y general, A es una matriz simetrica y positiva definitivamente, el descenso de gradiente se formula igual
$$ \triangledown f(x) = Ax-b $$
$$x_{k+1} = x_k - \alpha_k \triangledown f(x_k)$$
$$ x_{k+1} = x_k - \alpha_k (Ax-b) = (I-\alpha_k A)x_k + \alpha_k b $$
#### Con paso constante
pag 11


# Mid repaso
### Funciones cuadraticas
Muy comunes en los problemas de optimizacion, como en least squares y las define la matriz que usan.
A es una matriz simetria nxn y:
- Es positiva definitiva: es convexa con minimo
- Es negativa def: es concava sin minimo :(
- A tiene eigenvalores mixtos: no tiene minimio, en algunos lados es concava y en otros es conveza PRINGLES
- A = 0: es una funcion afin, pero si b no es igual que 0 tiene minimo
- Si es positiva semidefinitiva: eigenvalores positivos o 0, es convexa pero puede que no tenga un minimo finito!

### Minimos
Si es positiva definititva tenemos suerte! Tiene un positivo y es facil encontrarlo.
El gradiente se puede escribir como $\triangledown f(x) = Ax+b$ y el minimo es $x=A^{-1}b$
(si no es invertible es que tiene 0 eigenvalores, y  es positiva semidefinitiva)

Y esto esta guay, pero invertir A puede ser suuuper caro! O(n^3) y un mejor caso de O(n^2.37)!

una solucion es usar metodos basados en gradiente o aproximaciones para tener soluciones validas bien rapido

### Descenso de gradiente cuadratico
Aplicar el viejo descenso de dradiente a las funcioens quadraticas
$$ x_{k+1} = x_k - \alpha_k (Ax+b)$$
$$ x_{k+1} = (I - \alpha_kA)x_k + \alpha_k b$$
Y si el paso es constante, podemos escribir toda la iteracion como:
$$ x_{k+1} = (I - \alpha A)^k x_0 + \sum^k_{i=0}(I - \alpha A)^i b$$
Y esto acab convergenendo a $\alpha (\alpha A)^{-1}b$

Y como de rapido converge? Pues si decimos que L es el eigenvalor maximo de A, y mu el menor; sabiendo asi su k (el numero de condicion).
El rate de congencia mas alto es cuando alpha = 1/L; pero si mu> 0 la convergenia es lineal.
Aunque si mu = 0, la convergenia esta garantizada!!

Pero esto es todo con paso fijo!

#### y con paso exacto...?
La direccion es ostogonal entre la slope )??? mirar manana
Pero el paso... El paso es una funcion que tenbemos que minimizar tambien! la definimos como $g_p(\alpha) = f(x+\alpha p)$ y dadon esto, necestiamos encontrar $g_p'(alpha^*) = 0$
Es decir un pto estacionario de esta funcion! Y si tenemos r= como el residuo=Ax-b
Entonces el paso ideal seria $$ \alpha^* = \frac{<r,r>}{<r,Ar>} $$
Y p = -gradiente de f, que es -(Ax-b) = -r
los angulos de cada paso son de 90 grados, yq eue los gradientes son perpendiculares a la linea de nivel; y iteramos usando el gradiente como direccion.