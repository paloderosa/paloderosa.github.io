---
layout: post
title: 01. Introducción al modelo de aprendizaje PAC
date: 2019-07-16 12:58:00
mathjax: true
comments: true
---


### Problemas
Ejercicio 3 del capítulo 2 de *Understanding machine learning*


### Trabajo numérico
Vamos a hacer experimentos numéricos para ilustrar el contenido de los resultados en torno a que las clases de hipótesis finitas son PAC aprendibles.

Consideremos el problema que hemos estado discutiendo en clase. Tenemos un dominio $\mathcal{X}$ dado por el cuadrado $[0,2]\times[0,2]$ y un conjunto de categorías dado por $\mathcal{Y} = \\{ 0,1 \\}$. Supongamos que la distribución definida sobre el dominio es una distribución homogénea y la función de clasificación $f$ es $f(x) = 1$ si $x\in\mathcal{X}_1$ y $f(x)=0$ si $x\in\mathcal{X}_0$, donde $\mathcal{X}_1 =  [1/2, 3/2]\times[1/2,3/2]$ y $\mathcal{X}_0 = \mathcal{X}-\mathcal{X}_1$.

Consideremos ahora una clase de hipótesis finita que satisfaga realizabilidad. Una clase de estas consiste en rectángulos alineados a los lados de $\mathcal{X}$. Para que la clase de hipótesis sea finita, discretizamos los lados del rectángulo en unidades de 0.01 y desplazamos la esquina inferior izquierda de los rectángulos de la esquina inferior izquierda de $\mathcal{X}$ en unidades de 0.01 en cada dirección.

1. Especifica una parametrización del espacio de hipótesis.
2. ¿Cuál es el tamaño del espacio de hipótesis?

Formemos ahora conjuntos de entrenamiento *independiente e idénticamente distribuidos*, con una distribución, como dijimos, homogénea en $\mathcal{X}$ para un solo punto.

{:start="3"}
3. En **python**, define un conjunto de métodos que realicen las siguientes tareas: a) formen conjuntos de entrenamiento $S$ con $m$ elementos, b)implementen una hipótesis $h:\mathcal{X}\rightarrow\{0,1\}$ para cada $h$ en $\mathcal{X}$, c) calculen errores empíricos y de generalización y d) seleccionen al rectángulo $\text{ERM}_{\mathcal{H}}$.

4. Simplifiquemos la clase de hipótesis finitas a rectángulos con lados paralelos a los lados de $\mathcal{X}$, *centrados* en $\mathcal{X}$. ¿Cuál es el tamaño de $\mathcal{H}$? Forma un conjunto de entrenamiento con $m$ elementos, para $m = \text{e}^0, \text{e}^{1/2},\text{e}^1, \ldots,m_{\mathcal{H}}$, donde $m_{\mathcal{H}}$ es la complejidad de $S$ para un parámetro de confianza y un error de 0.01. Grafica los puntos de cada conjunto de entrenamiento. Grafica los errores de generalización $L_{(D,f)}$ y empírico $L_S$ para cada hipótesis en $\mathcal{H}$. Obtén algún rectángulo $h_S$ que minimice $L_S$ y grafícalo en $\mathcal{X}$.

5. Para cada valor de $m$, forma 1000 conjuntos de entrenamiento, selecciona $h_S$ en cada caso y haz un histograma del error $L_{(D,f)}$.

6. Si seleccionas un valor $\epsilon$ del error de generalización $L_{(D,f)}$, ¿cuántos puntos del histograma tienen error de generalización menor a $\epsilon$?

7. ¿Qué dice en este caso el resultado de que las clases de hipótesis finitas son PAC aprendibles con complejidad de muestra $\text{log}(\|\mathcal{H}\|/\delta)/\epsilon$?

8. Haz cualquier otra cosa que te resulte interesante.
