# Procesos_Gaussianos
Este repositorio contiene una simulación de trayectorias de un Proceso Gaussiano (GP) junto con su análisis teórico y visualización mediante Python.

Un Proceso Gaussiano es un proceso estocástico definido en un conjunto de índices $T$ (usualmente el tiempo o el espacio), tal que cualquier subconjunto finito de variables aleatorias tiene una distribución normal multivariante. Un GP está completamente definido por su función de media $\mu(t)$ y su función de covarianza (kernel) $k(t_1,t_2)$.

Para cada conjunto de puntos ${ t_1​, t_2​,...,t_n } \subset T$, el proceso se define como:
$$(X_{t_1}, \dots, X_{t_n}) \sim N(\mu, K)$$

## Simulación de Procesos Gaussianos en Python

El objetivo principal del proyecto es explorar cómo diferentes funciones de kernel afectan la forma y suavidad de las trayectorias simuladas.
Se asume una función de media nula $\mu(t) = 0$. 
Los kernels implementados son los siguientes:

### Kernel RBF

Su expresión viene dada por: 

$$k(t_1, t_2) = \sigma^2 \exp\left( -\frac{(t_1 - t_2)^2}{2\ell^2} \right)$$

Donde:
 * $\sigma^2$  es la **varianza** y controla la amplitud vertical de las trayectorias.
 * $\ell$ es **longitud de escala** y controla la suavidad de las oscilaciones.

### Kernel periódico

Se utiliza para modelar funciones que repiten su estructura de manera cíclica. Su fórmula es:

$$k(t_1, t_2) = \sigma^2 \exp\left( -\frac{2\sin^2(\pi |t_1 - t_2| / p)}{\ell^2} \right)$$

Donde:
* $\sigma^2$  es la **varianza** y controla la amplitud vertical de las trayectorias.
* $p$ es el **periodo** y define la distancia entre las repeticiones del proceso.
* $\ell$ es la **longitud de escala**: y determina qué tan "suaves" son las oscilaciones dentro de cada periodo.

### Kernel DPK polinómico

Este kernel permite simular un GP que se comporta como una combinación lineal de funciones base (monomios). Dados $t_1, \dots, t_n \in T$ se define mediante una matriz $F$ 

$$F = \begin{pmatrix}
f_1(t_1) & \cdots & f_m(t_1) \\
\vdots & \ddots & \vdots \\
f_1(t_n) & \cdots & f_m(t_n)
\end{pmatrix}_{n \times m}$$

A partir de esta estructura, la matriz de covarianza $K$ se calcula mediante el producto matricial:

$$K = F F^\top$$

Donde cada entrada de la matriz resultante corresponde a la sumatoria:

$$k(t_1, t_2) = \sum_{i=1}^{m} f_i(t_1) \cdot f_i(t_2)$$

En este caso, las trayectorias resultantes no son curvas genéricas, sino **polinomios de grado $m$** con coeficientes aleatorios distribuidos según $N(0, 1)$.

## Tecnologías empleadas

Se ha hecho uso del lenguaje de programación python en el entorno de Google Colab, y las siguientes librerías
* numpy
* matplotlib
