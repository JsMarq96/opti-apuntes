Rank(A) = # de columnas independitnes

### Sistema leastSquares tiene solucion?
if rank(A) < n (incognitas)
	Se puede resolver usando la pseudoinversa y esa sera la funcion minima
	Ya que se basa en la proyeccion de b en la imagen de A (A^T b)
	Si exiasten varias soluciones, este proceso elegria la funcion de norma (distancia) mas pequena
If rank(A) = n # incognitas:
	x = (A^TA)^-1 A^T b
If m = n
	Si b no esta en la imagen, no hay anda que hacer



# 1 Psoinlidades de resolver un sisitema LE






