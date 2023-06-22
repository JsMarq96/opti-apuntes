La idea del supervised learning es generar un modelo que estrapole conclusiones de una serie de datos clasificoas, y que lo aplique a datos no conocidos

- Tenemos un dataset S de n cantidad, donde $S_n = (Z_1,Z_2, .., Z_n )$ donde $Z_i = (X_i, Y_i)$ que es un Input X y un label Y, y asumimos que no son aleatorios, ahi una distribucion D que desconocemos.
- Tenemos una classe H, que es una seria de funciones que mapea de X a Y. Suele estar parametrizadopor una serie de pesos
- Una funcion de error, o loss function, que mide lo eficaz que es una hipotesis en un pto de datos z

La idea es minimzar el error de pruebas $R(h) = E[l(h,Z')]$

Pero esto presenta un problema! Solo tenemos una parte de las pruebas de error, y no podemos aber como va a genralizar mas haya de esto!
Es decir, podemos subir la eficacia en los test de pruebas, pero puede no generalizar con datos no vistos.

Es decir, reigo empirico, o training error, la idea es reducirlo lo maximo posible, y rezar para que eso generalice despues!

### ERM
El empirical risk minimzaer es la funcion de optimizacion para reducir el training error, y es
$$w_{ERM} = \arg \min_w \frac{1}{N} \sum^N_i l(w,Z_i) + \lambda E(w)$$
El erm generalmente generaliza bien si la distribucion de datos es benigna, y la clase de hyptoesis no es muy compleja.

Una manera de ayudar a la generalizacion es añadir una funcion de regularizacion (acanade un coste extra, en funcion de como son los pesos). Penalizarian las hiptesis con "large complexity??" es decir con pesos muy desiguales?, o no normalizados.

# ERM como una optimizacion convexa
la funcion de optimizacion no siempre tiene que se convexa! Lo es en  una regresion lineal, peero en un clasificador binario, tiene miuchas discontinuidades! El gradiente es o 0 o no existe

### Areglando la no-convexidad
la idea es sutituir la funcion de loss por una que sea tractable upper bound.
Esto significa que en vez de dar 0 o 1, da vlores de distancia entre ellos

Para ello primero definimos una funcion de margen $\mu(w,z)= y <w,x>$ 
Luego cambiamos la funcion de step no diferenciable por una funcion surogada convexa.

Esta funcion a de ser convexa y surrogada, y ser el upper bound de la funncion step (es decir deve ser igual o mayor en los valores de cada punto), y ser similar a la step funcion (sobretodo en que da 1 en 0, y cuando tienda el infinto da 0)

Se suelen usar la logistic loss, la hinge loss, la squares hinge loss


# Descenso de gradiente estocastico
Intenta resolver problemas con los gradientes:
- Puede ser caro calcular el gradiente de los pesos
- Puede haber error en el gradiente o los datos
- puede que haya punto en los que el gradiente no exista!

Para solucionar el problema de los gradientes, la idea es sustituirlo por un estimador unbiased del gradiente.

En este caso, sampeamos las muestras de entrenamiento, elegemimos aleatoriamente unas muestras para aproximar el gradiente.

Es decir por cada iteracion sampleamos la muestras y elegimos lt
Calculamos el subgradiente g_t
Actualizamos los parametros w
Y luego proyectamos los parametros a C

(solo 1 muestra)

Peerro el problema que esto muestra es que la aleatoriedad puede dañar la convergencia!
Entonces esto va por minibatching!
Aproximamos el gradiente en vez de elegir 1 indice, elegimos unas minibatched de tamano b, y calculamos el sibgradiente con ellos
Si b es grande, el resultado es crcano a el gradiente autentico, y sigue siendo unbiased.


Esto mola y tal, pero no podemos estar 100% seguro de que el subgradiente sea la direccion de descenso!

## Que mola?
- Mucho ams optimo y rapdiod ecalcullar
- Funcionara incluso sin un numero de condicion finita, sin coste por la alta dimensionalidad
### Que no mola?
- La conversion es mucho mas lenta que linear, cuando se compara con desceso de graidente con un buen numero de condicion.
- Los learning rates o el paso es bastnate mas chiquito apra compensar por el ruido.