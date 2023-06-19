# Condiciones de optimalidad
- Condicion NECESARIA para extremos locales: un pto x0 es un minimo o maximo local si es continuamente diferenciable alrededor, y si el gradientes es 0 en x0
- Condiciones suffiecnetes para un minimo local: Si el gradiente es 0 en un pto x0, y D^2 f es positivo definitivo, entonces x0 es un minimo local

NOTAS: la suma de dos amtrices defintiivamente positivas, da un matriz positiva, y la transpuesta de una amtriz positivametne definitiva es positiviamente definitiva
# Descenso de gradient & metodo de Newton

$$ D_v f({x}) = \lim_{h \rightarrow 0+} \frac{f({x} + v h) - f({x})}{h} = <\triangledown f(x),v> $$
La direccion de maximo crecimiento de f en un pto x_o:
$$ p = \frac{\triangledown f(x_0)}{||\triangledown f(x_0)||}$$
Y la direccion de maximo decrecimiento:
$$ p = -\frac{\triangledown f(x_0)}{||\triangledown f(x_0)||}$$
# Sistemas de busqueda lineal
Se basan en calcular puntos estacionadios de una funcion diferencial. Son metodos iterativos con un pto incial, y una sucesion de iterados.

la idea es encontrar un una sucesion de ptos hasta que convergan a $\triangledown f(x^*)=0$
Se calculan los pasos con:
- $p_k$ es ima direccion de busqueda
- $\alpha_k$ es la longitud del paso
$$ x_{k+1} = x_k + \alpha_k p_k $$
Las diferencias dependen de como se calclan

## Condiciones para converger
#### Direcciones de Descendimiento
Dada una direccion de descendimeinto, $<p, \triangledown f(x)>\  < 0$ 
$$ f(x) > f(x+\alpha p) $$
Es bastante sencillo y directo

### Elegir una longitud del paso
La opcion mas facil es usar un paso igual para cada iteracion. Pero esto influye mucho en la convergencia de la funcion, y la velocidad de su convergencia! Por lo que aunque sea facil de implementar, limita mucho la practica y los resultados.

Pero esto lo podemos presentar como un problema de optimizacion! Elegir la distancia adecuada para minimizar la funcion.
$$ g_p(\alpha) = f(x + \alpha p) $$
$$ \alpha_p ^* = arg \min_{\alpha >0} g_p(\alpha) = arg \min_{\alpha >0} f(x + \alpha p)$$

Sin embargo, el calcular el optimal step, puede ser demasiado caro! 
Pero hay un truco!
$$ g'_p(\alpha^*_p) = 0 \leftrightarrow <\triangledown f(x + \alpha^*_p p), p> = 0 $$
Esto significa que el paso optimo esta en los ptos en los  que el gradiente es ortogonal a ldireccion de p. Es decir, cuando la direccion de busqueda sea tangente a la linea de nivel.

#### La condiciones de Wolfe
Queremos un paso que:
- haga decrecer la funcion
- No se muy pequeno (demasiadas iteraciones para converger)
Las condicioens de Wolde determina el rango de $\alpha$ valores que satisfacedn las 2 condiciones; y sirven de bases para construir un algortimo de busqueda en linea con menos coste computacional de el optimal line seach.

Dado un stepsize $\alpha$ que satisface las condiciones de Wolfe en la direccion de p si:
- Sufficient decrease: dado $c_1 \in (0,1)$
$$ g_p(\alpha) \leq g_(0) + c_1 \alpha g_p'(0) \ \ \leftrightarrow \ \ \ f(x+\alpha p) \leq f(x) + c_1\alpha <\triangledown f(x),p>$$
Significa que eel valor de la funcion deveria decrecer significativamente en el nuevo punto, si la normal del gradiente es grande. C_1 es para tener en ceunta el error de la aproximacion de talylor (en practica c1 es chiquito)
Esto hace que el alpha es proporcional a el gradiente del punto, y que por lo menos siempre es mejor (es decir, es menos llano el pto) (ojo, como esto esta basado en Taylor, necesito tener en cuenta el error de taylor, en sistemas del mundo real)

- Curvature condition: dado $c_2 \in (c_1,1)$
$$ g_p'(\alpha) \geq c_2 q_p'(0) \ \ \leftrightarrow \ \ <\triangledown f(x + \alpha p),p> \geq c_2<\triangledown f(x), p>$$
signnifica que la pendiente del pto deve decrecer significativametne en un nuevo punto. Esta condicion nos hace estar mas cerca de cunplir que el dot del gradiente y la direccion p sea 0, por lo que es un paso optimo. c2 en este caso deveria ser grande


## Pero cuando converge?
Se usa el Teorema de Zoutendijk: Dada una sucesion de iteraciones x, y una seria de direcciones p, y longitudes de paso $\alpha$ que satisfacen las condiciones de wolfe:
$$ \sum^\infty_{k=1}\cos^2(\theta_k) ||\triangledown f(x_k)||^2 < \infty$$
Donde
$$ \cos \theta_k = \frac{<\triangledown f(x_k), p_k>}{||\triangledown f(x_k)||\ ||p_k||} $$
Esto implica que la funcion tiende a 0

## Descenso de gradiente
Es un algoritmos de busqueda en linea en el que
$$ p_k = -\triangledown f(x_k)$$
$$x_{k+1} = x_k - \alpha_k \triangledown f(x_k)$$
El paso puede ser fijo, optimo o aproximado. Es bien sencillo de usar, pero es bastante lento, aunque con algun punto guay.


## Metodo de Newton
Se basa aproximar una funcion doblemente diferenciable, usando su expansion de taylor de grado 2; y usarlo para configurar el paso y direccioni cuando el gradiente de este sea 0.
Gracias a usar el taylor de grado 2, la optimizacion es mas sencilla, ya que tiene forma de parabola (o paraboloide?).
$$  f(x) \approx m(x) = f(x_k) + <\triangledown f(x_k), x-x_k> + \frac{1}{2}<D^2 f(x_k)(x-x_k), x-x_k> $$
Luego calculamos el pto estacionario de m(x) usando el gradiente igual a 0, y eso lo usamos ara generar el paso
$$ x_{k+1} = x_k -D^2 f(x_k)^{-1} \triangledown f(x_k) $$
Problema: solo si D^2 es defintivamente positivo, x_k+1 sera el minimizador y p_k sea la direccion de descendimento. Si no ira al maximizador
Es decir, si la hessiana es positiva, es un line seach method.

Otro problema que tiene es que la covnergencia no esta garantizada, depende de las condiciones iniciales.
$$ p_k = -D^2 f(x_k)^{-1} \triangledown f(x_k)$$
$$ \alpha_k = 1$$

Y aunque este metodo PUEDE ser muy rapido, las itraciones pueden ser muy caras, ya que implica calcular la hessiana. Hay metodos basados en este que intentan aproximarla, se llaman los metods quasi-Newton

# Ritmo de convergencia de metodos iterativos
Siendo un metodo iterativo con pasos x, y un valor al que tiene que converger x*,

se dice que un metodo tiene convergencia linear si:
$$ \lim_{k\rightarrow \infty} \frac{||x_{k+1}-x^*||}{||x_k-x^*||} = r\ \ \ r \in (0,1)$$
Donde r es el ritmo de convergencia (o ratio??)
si r=0 la convergencia es super linear (to rapida!)
Si r=1 tiene convergencia sublinear

Luego esta la convergencia Quadratica
$$ \lim_{k\rightarrow \infty} \frac{||x_{k+1}-x^*||}{||x_k-x^*||^2} = M\ \ \ M \in 0$$


# 3 Minimizacion de metodos diferenciales
Esta la derivada direccional, que estudia el cambio en una direccion

La direccion de maximo crecimiendo en un pto es la normalizacion del gradiente en ese pto
	OJO: en partes de crecimiento 0, la direccion es ortogonal a la superficie

Y la direccion de maximo decrecimiento, es el gradiente normalizado, pero negativo!

### Como sabemos si un pto es un extremo y un minimo?
Esta la condicion Necesaria, que es cuando no hay cambio en una funcion en un pto, que sera el cual en el que el gradiente de 0. Todos los extremos deven de cumplir esta condicion

Y si queremos saber si es un minimo, evaluamos la hessiana en ese punto y (si se cumple la primera condicion), y la matriz producida por la hessiana es definitivamente positiva, se trata de un minimo local!

Pero, como encontramos los minimos?

### Busqueda lineal!
Estos son metodos iterativos, que calculan una sucesion de ptos estacionarios, de funciones diferenciables, hasta llegar un pto estacionario de la funcion!
Las iteraciones se calculan usando $x_{k+1} = x_k + \alpha_k p_k$,en el que x son las muestras, alpha el paso y p la direccion en la que actualizamos la x anterior.

Los distintos tipos de busqueda lineal se dan a la hora de cauclar p y alpha para una nueva iteracion; pero tenemos un problema, como elegimos estos valores para asegurarnos una buena convergencia?

##### Direccion de descenso
Una buena metrica para asegurarnos que tenemos la direccion correcta, es que tiene que ser en una direccion opuesta a el gradiente (ya que nos interesa el minimo). Es decir dada una direccion cualquiera p, el dot entre la direccion y el gradiente tiene que ser menor que 0.
Otra condicion interesante es que al evaluar f en el pto nuevo, el resultado tiene que ser menor que el actual, incluso si el paso es pequenito.
Pero.. cuanto avanzar?

##### Longitud del paso
La manera mas facil, es elegir un paso fijo e tirar para alante. Sin embargo, es muy facil perder la granuralidad y perder la convergencia, o tardar demasiados pasos en llegar a ella.

Para remediarlo, porponemos la idea de una busqueda de linea EXACTA, la cual se basa en usar un step perfecto. 
Esto se puede tratar como un problema de optimizacion por si mismo, intentando minimizar f en x0, y siendo alpha la variable.
Pero esto se puede volver muy caro computacionalmente, asi que intentaremos una estrategia.
Hemos observado que el paso optimo lo podemos conseguir directametne de la magnitud del gradiente, si la direccion en la que nos desplazamos p es tangente a la linea de nivel de la funcion (es decir si es orthogonal a el gradiente, es decir si su dot es 0, y puedes tirar para abajo y para arriba)

Para elegir un paso adecuado, usamos las condiciones de Wolfe, que nos marcan que rango de alphas funciona bien dado un pto. Esto cuidara que todos los alphas hagan que la funcion decrezca, y no sean muy chiquitos.
- Condicion de sufficient decreare: dado un parametro c1 (0,1), se adegura que el crecimineto corresponda con la norma del gradiente (norma muy grande, el alpha tendra que corresponder): $f(x+\alpha) \leq f(x) + c_1\alpha <\triangledown f(x), p>$ es decir, el paso tiene que reportar un beneficio lineal de la derivada en la direccion de movimiento. c1 existe porque esto esta inspirado en taylor asi que hay cierto margen de error. c1 suele ser chiquito 10^-4
- Condicion de curvatura: asegura que en un punto, la pendiente desciende significativametne en el nuevo punto, dado un parametro c2 (c1, 1): $<\triangledown f(x+\alpha p),p> \geq c_2 <\triangledown f(x), p>$. c2 suele ser grande, rollo 0.9

Estas condiciones y lo que sabemos de la direccion nos aseguran unas iteraciones eficaces, pero no nos garantizan si podemos converger!
#### Teorema de Zoutendjik
Asumismos una seria de iterantes, de un algoritmo de busquerda en linea, cuyos pasos y distancias de paso cumplen las distancias de wolfe:
$$ \sum^\infty_{k=1} \cos^2 \theta_k ||\triangledown f(x_k)||^2 < \infty$$
Siendo tetha el angulo de diferencia entre la direccion p  y el gradiente negado (pendiente o direccion idonea).
Esto implica que el coseno por la norma tienen a 0. Y si theta esta en el rango de 0 a pi/2, eso significa que la norma del gradiente tiende a 0, por que el algortimo converge a un pto estacionario. (?)

### Ratio de convergencia
Una cosa es llegar a la solucion, pero la otra, cuanto de rapido llegas!
Dada una serie de iterandos, y un punto x*, que es el pto de convergencia, podemos decir como converge un metodo dada su velocidad, y un rate de convergencia r:
- Linear: tiene convergencia linear si $\lim_{x \rightarrow \infty} \frac{||x_{k+1}-x^*||}{|| x_k - x^* ||} = r$ siendo r un numero de 0 a 1
- Sublinear si r=1
- Cuadratica: $\lim_{x \rightarrow \infty} \frac{||x_{k+1}-x^*||}{|| x_k - x^* ||^2} = M$ si M > 0
- O tiene una orden de convergencia p si: $\lim_{x \rightarrow \infty} \frac{||x_{k+1}-x^*||}{|| x_k - x^* ||^p} = M$ si M > 0

#### Descenso de gradiente:
Es un metodo de busqueda en linea, cuya pendiente es el gradiente negado; y de longitud del step se puede hacer lo que queramos.
Es bien sencillo, y muy usado, pero es a la vez uno de los mas lentos.
Como converge? En el peor de los casos, es lineal.
Su rate de convergencia depende de k, el condition number. Esta formado por la division del eigenvalor mayor por el menor, de la hessiana evaluada en el pto de convergencia.
Cuando k se acerca a 1, significa que los valores de la hessiana estan en un mismo rango, y se dice que el problema esta bien posado (?)

#### Metodo de Newton
El metodo de Newton se basa en el polinio de Taylor de segundo grado.  Esto es porque tiene una forma de parabola, y tomando la aproximacion local de Taylor, podemos aprovecharnos de eso para encontrar el siguiente pto estacionario de la funcion aproximada:
Tenemos m, que aproxima f en un pto k+1, entonces calculamos el gradiente de m y vemos cuando da 0; y usamos eso para construir el paso nuevo:
$$ x_{k+1} = x_k -D^2 f(x)^{-1} \triangledown f(x_k) $$
Ojo, estp solo funcionara si la hessiana es positiva definitivamente, de ser asi descendera a el minimo, pero si no se puede ir a un maximo. Por lo que el pto de comienzo influye mucho en la convergencia final, lo cual lo hace muy sensible; y encima es muy caro de calcular.
El paso se pone a 1 al prinpio, pero se va disminiyendo si la funcion no decrementa lo suficientemetne rapido.
Esto lo vemos reflejado en su convergencia:
Es quadratica, si esta cerca! Si no esta cerca, puede quedarse atascado en un pto estacionario intermedio, o dar vueltas indefinidamente.
Pero SI hay convergencia (esta cerquita) entonces es quadratico, muy rapido!
Los metodos de Quasi Newton, que usan aproximaciones para la hessiana, empeizan igual que el descenso de gradiente, pero cuando se empiezan a acercar a la convergencia pasan a moto Newton y aceleran