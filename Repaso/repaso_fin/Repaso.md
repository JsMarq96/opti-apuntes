# Conjugado de gradiente
Minimizar una funcion cuadratica (donde A es una matriz simetrica de nxn)

### Direcciones ortonogales
El descenso potimo de n pasos, solo devera usar N direcciones ortogonales, e usar cada direccion solo 1 vez.

El problema es que para que esto funcione necesitamos saber el error exacto, que solo lo sabemos si sabemos el resultado, en el que alpha es el paso en una direccion i y e = x_i - x^*
$$\alpha_i = -\frac{<e_i,d_i>}{<d_i, d_i>}$$
### Metodo de direcciones conjugadas
La idea es que generar 2 direcciones que sean A-rtohonales (ortonoales a la matriz), o que sean conjugadas. Estos vectores son ortogonales si normalizamos A
$$<v,Aw>=0$$
Es decir que tomoms una serie de direcciones conjugadas  entre si en A
Aqui el paso se calcula el usando el resto = $r_i = Ax_i - b$ no necesitmaos los valores correctos de x
$$\alpha_i = -\frac{<r_i,d_i>}{<d_i, Ad_i>}$$
El problema ahora e que la ortgonalizaciond e gramms chmidpt para calcular las bases A-ortogonales es muy caro de calcular


# Optimizacion convexa
Si nuestro problema es convezo podemos garantizar la existencia de soluciones/
Si es extrictamente convexo,  podemos problar que la funcion tiene una solucion unica.

En caso de que no sepamos esto, podemos enclose las solucioens en sets convexos, y garantizar la existencia y unicidad de una solucion.

Y si el problema es convexo pero no diferenciable, lo podemos derivar usando principios de dualidad.

# Sets convexos
Un set convexo es un set el cual al unirno 2 ptos con un segmento, el segmento nunca sale fuera de la forma del set.

### Set affin
Un set que contiene no segmentos, si no lineas entereas. Todos los sets affines son sets convexos

### Tipos
- Hyperplano
- Medioespacio
- complex hull

### Preservar convexidad
- si f es una funcion affin, y acepta de entero un set convexo, el resutlado y la inversion de f (transformacion afin del set) son convexos

### Condiciones de convexidad en funciones
- Primer orden: si $f(y)>f(x)+<\triangledown f(x), y-x>$ (es decir si dados dos puntos, el valor de uno es mayor que el valor del anterior mas la distancia/ pendiente que hay hasta el otro punto)
- Si es doble diferenciacble y la Hessiana es positiva semi-definitiva (si es positiva defintinva f es estrictametne convexa)

Least squares es convexa para cualquier A


# Minimizacion de funcioens convexas en sets covnexos
La idea es poner unas limitaciones a la optimizacion a modo de constraints.
Constricciones de sets convexos conservan las propiedades del set original, de manera de que un minimo local tambien sera globnal, por lo que un set limimtad tambien tendra un minimo.
Es decir funciones convexas limitatres en locsed and bounded convex sets tiene minima.

Podemos mirar las funciones como que tienen +infinot si no estan dentro de las contraints, y f(x) si x esta dentro.


### Subgradiente
Si una funcion f no es diferenciable, defimos que p es un subgradiente de la funcion si se satisface la condicion $f(y)>f(x)+<p, y-x>$.

A el diferencial d se le llama a todos los psudogradietnes que hay en unputo de f


### Minimizacion de funcioens convexas en sets convexos
Dada f una funcion conveza y C un sets cerrado convexo de R^n
$$\min_{x \in C} f(x) = \min_{x\in R^N}f^{gorrito}_c(x)$$
Un pto x_0 es un minimo solo si y en ese punto, el uno de los pseudogradientes  del diferencial es 0
Eso equivala a si fuese diferenciable que le gradiente da 0 en eses punto


# Constrainded optimizacion
2 tipos de constraints:
- Inequality constraints >=
- Equality constraints =

para resolverlo, la idea es que lo pasamos a un porblema de optimizacion generico
### Multiplicador lagrangiago

La teoria del mutplicaod lagrangiano dice, que dado un extremo local en una funcion, el gradiente de la funcion en ese punto, puede ser expreesado como una convinacion lineal de gradientes de las constraints.

$$L(x,\lambda, \nu) = f(x) - \lambda g(x) - \nu r(x)$$
en el que g es una constrian de inqcualidad y nu una constrain de equalidad

- Una cosntraint esta activa si lambda es mayor que 0, y por lo tanto la condicion impuestq se esta respetando. Si no, esta inactiva.
- Si un pto no activa la constraint, se dice que el punto es un  pto interior
- Es decir constraint activa si = 0
- Un pto es interior point si c(x) >0 la cumple, pero pasivamente (lo cual hace que lambda se a 0)
NO ENTIENDO ESTO AAAAAA


### Karush Kuhn Tucker conditiones
La idea es que para que una solucion contrained sea dad como valida, tiene que cumplir todas las condicioens KKT pertientes
1) Primal stationaribility: $\triangledown L(x, \lambda, \mu) = 0$
2) Primal fesability $c_i(x)\leq 0$ 
3) Primal fesiablity: $d_i(x) = 0$
4) Dual positivity: $\lambda_i \leq 0$
5) Complementary slackness: $\lambda_i c_i(x_0) = 0$



# Problemas Duales
Son los porbelmas que intentan maximizar una cosa y minimizar otra variable.

### Inecualidad de Max-min
$$\max_y \min_x L(x,y) \leq \min_x \max_y L(x,y)$$
Esto intorudice el duality gap o DG, que es $\min_x \max_y L(x,y) - \max_y \min_x L(x,y) \geq 0$
Pero lo que esto nos dice es que si el DG llega a 0, estamos ante el maximo y el minimo posibles.
Esta solucion se le llama saddle point; y no podra exisitir un saddle point si el DG no es 0 en ese punto (condicion necesaria).

### Dualidad de langrangiano
Dado
$$ L(x,\lambda, \nu) = f(x) - \lambda_i c_i(x) - \nu_j d_j(x)$$
Esto se mantiene
$$\min_{x\in C} f(x) = \min_{x\in R^n} \max_{\lambda\leq 0, \nu \in R^n}f(x) - \lambda_i c_i(x) - \nu_j d_j(x)$$
Es decir la minimizacion del problema basico se aplica a la aresolucion del problema min-max
 Aqui tambien se aplica el dualitu Gap


### Problema Dual
Calculamos la funcion dual langrangiana, que es
$$ g_D(\lambda, \nu) = \min_{x\in R^n} L(x,\lambda,\nu)$$
Y la idea es maximizar la funcion dual, dando lugar a la funcion orignal. Esto es el Dual problema:
$$  \max_{\lambda\leq 0, \nu \in R^n} g_D(\lambda, \nu)$$
Se el llama a f la funcion primal y x la variable primal, sienod el problema primal el min de f(x)

En este caso el Dual Gap se calcula con la resta del problema primal - problema dual.

A esto se le llama el problema primal dual: encontrar un saddelpoint del laplaciano.


# Primal-dual y Dual para problemas no diferenciables
Puede haber problemas que no sean difereniables en algunos puntos del dominio, por lo que hace que no sea continua, lo cual hace que no podamos usar gradientes

### Variable auxiliar
Una manera de hacer diferenciables es anadir una variable auxiliar, reformulando el problema por uno equivalente.

En nuestro caso, veremos como sustituir una norma por un dot prod maximizado. La norma no siempre es diferenciable
$$||y||_R = \max_{||\xi||_R \leq 1} <y, \xi>_R$$
Reformulamos el problema como H(x,\xi), de tal manera que f(x) ahora es
$$f(x) = \max_{\xi \in C} H(x,\xi)$$
Por lo que el problema de minimizacion es
$$\min_x f(x) = \min_x \max_{\xi \in C} H(x, \xi)$$
Ahora en vez de un problema no difereiable tenemos un problema minmax

### Problema Min max
La cosa es que si partimos de un probelma
$$\min_x \max_{\xi \in C} H(x, \xi)$$
la cosa es que para cada x fijo H(x,\xi) es una funcion convaba para xi.
Asi que si le damos la vuelta de manera que 
$$\max_{\xi \in C} \min_x H(x, \xi)$$
Hacemos que H sea convexa para cada xi fijo. (esto ayuda a resolverlo, la solucion a bos es esl saddlepoint)


# Resolver problemas max min
### Metodo primal-dual
La idea es resolver x e xi a ala vez, encontrado un saddlepoint de H

Para eso contamos con un descenso de gradiente para x; y un ascenso de gradiente projectado para xi(porque esta constrained).

La proyeccion viene dada por
$$P_C(\xi) = \frac{\xi}{\max(||\xi||, 1.0)}$$

1) Se actualiza el dual: $\xi^{i+1} = Pc(\xi^i + r \triangledown_\xi H(x^i,\xi^i))$ 
2) Se actualiza el primal: $x^{i+1} = x^i - \theta \triangledown_x H(x^i, \xi^{i+1})$

### Metodo Dual
Intentamos resolver ambos a al vez

Primero minimzamos de cara x, usando $\triangledown_x H(x,\xi) = 0$ y reescribimos esto como una funcion que dependa de xi: $x_0(\xi)$ 

Luego lo sustituimos dentro de H, dando lugar a 
$$g_D(\xi) = \min_x H(x,\xi) = H(x_0(\xi), \xi)$$
Ahora maximizamos g_D llegando a el problema dual.
Esto es ahora un problema quadratico con constraints
esto lo podemos resolver como
$$\xi^{k+1} = Pc(\xi^k + r\triangledown_\xi g_D(\xi))$$
En este caso, podemos usar el Duality gap para elegir si terminamos antes las operaciones o no! (como es un saddlepoint)

$$\min_x \max_\xi H(x,\xi) - \max_\xi \min_x H(x,\xi) \geq 0$$
$$f(x^k) - g_D(\xi^k) \geq 0 $$


# Supervised learning
La idea es, a partir de una seria de datos categorizados, como unpiuts y respuestas, conseguir aun funcion de hipotesis h que funcione y clasificque en datos no vistos.

### Partes
- Dataset: compuesto por pares de (Xi, Yi), input y label
- Hipotesis: una fucion hipotesis que mapea input a labels
- Loss function: una funcion que dado un label y un input evaluaa la calidad de una hipotesis l(h(x,y), x, y). Esto da el test error

### La meta
Reudicr la loss funcion en el test data, y esperar que extrapole anuevos datos
$$ \min_\omega R(\omega)$$
### Modos
En funcion de lso labes puede ser
- Regresion: generar un valos
- clasificacion: decir con un parcentage que es mas posible que sea

### Empirical risk vs error
El probelma es que no podemos porblar todos los casos del mundo real, entonces solo tenemos controlsobre el traninig error (o riesgo empirico), que es la media de todos las pruebas del traninig error.

Al final tenemos que intentar rebajar el training error, y esperar qu generalice 9asi que no se tiene que especializar tanto)

### Empirical risk minimizator
Una amtrica de error que intenta que se generaliza mas o menos si los datos no son muy complejos

$$w_{ERM} = \arg \min_w \frac{1}{n}\sum_{i=1}l(w,Z_i) + \lambda E(w)$$
Tamtien se puede anadir un termino regulador que penaliza pesos no normalizados o muy grandes.

### ERM como una optimizacion convexa
El problema es que no tiene porque ser voncexa, depnde del problema y  los datos, como por ejemplo si es un calsificado binatio, que el gradiente no existe.

Entonces primero tenemos que susttuir la la step function, por una funcion surrgada, que sea covnexa y diferenciable, que sea upper boiund (siempre mayor que la step), y que deve satisfacer que en 0, da 1; y que en el finiito da 0. Hasy varias como la hinge loss o la logistic loss


### Descenso de gradiente estocastico
Problema: con todo y con eso el gradiente no termina de molar.
Calcularlo par aun pto puede ser muy caro (el RM es muy caro si n es grande!), puede haber ruido en los datos, o puede que haya puntos en los que no existe igualemnte (como la hinge loss).

Entonces usamos tocastic gradient descnet!
La idea es reemplazar el gradiente por un subgradiente estimado sin ningun biase, elegido altoriamente.

Entonces en cada paso calculals un subgradiente g_t mediante tomando una muestra unbiased de una de los ptos de nuestro dataset, y calculando el gradiente SOLO con esa.

Luego hacemos el update
Y luego proyectamos los parametros a C

pero eso podria danar la convergencia, asi que vamos por minibatches: calcualmos no 1 muestra, si no varias, elegirdas alateoriamente.