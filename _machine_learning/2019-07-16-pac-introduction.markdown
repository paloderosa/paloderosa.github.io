---
layout: post
title: Introduction to the Probably Approximately Correct model of machine learning
date: 2019-07-16 12:58:00
mathjax: true
comments: true
---


Vamos a hacer experimentos numéricos para ilustrar el contenido de los resultados en torno a que las clases de hipótesis finitas son PAC aprendibles.

Consideremos el problema que hemos estado discutiendo en clase. Tenemos un dominio $\mathcal{X}$ dado por el cuadrado $[0,2]\times[0,2]$ y un conjunto de categorías dado por $\mathcal{Y} = {0,1}$. Supongamos que la distribución definida sobre el dominio es una distribución homogénea y la función de clasificación $f$ es $f(x) = 1$ si $x\in\mathcal{X}_1$ y $f(x)=0$ si $x\in\mathcal{X}_0$, donde $\mathcal{X}_1 =  [1/2, 3/2]\times[1/2,3/2]$ y $\mathcal{X}_0 = \mathcal{X}-\mathcal{X}_1$.

Consideremos ahora una clase de hipótesis finita que satisfaga realizabilidad. Una clase de estas consiste en rectángulos alineados a los lados de $\mathcal{X}$. Para que la clase de hipótesis sea finita, discretizamos los lados del rectángulo en unidades de 0.1 y desplazamos la esquina inferior izquierda de los rectángulos de la esquina inferior izquierda de $\mathcal{X}$ en unidades de 0.1 en cada dirección.

1. Especifica una parametrización del espacio de hipótesis.
2. ¿Cuál es la dimensión del espacio de hipótesis?
