---
layout: post
title: 02. Modelo PAC generalizado y predictores lineales
date: 2019-08-13 12:58:00
mathjax: true
comments: true
---


### Problemas
Problemas 4, 7 del capítulo 3, problema 1 del capítulo 4, problema 3 del capítulo 9.


### Trabajo numérico

Vamos a implementar en **python** el algoritmo del perceptrón. Recordamos que, dado un conjunto de entrenamiento $S_m = \\{(\mathbf{x}_1, y_1), \ldots, (\mathbf{x}_m, y_m) \\}$, con cada $\mathbf{x}_i\in\mathbb{R}^d$ y cada $y_i\in\\{+1,-1\\}$, formamos una secuencia de predictores $\mathbf{w}^{(t)}$ de la siguiente manera. Elegimos $\mathbf{w}^{(1)}$ como el vector $(0,\ldots,0)\in\mathbb{R}^{(d+1)}$, con el que formamos el predictor dado por el signo de $h\_{\mathbf{w}}(\mathbf{\tilde{x}}) = \langle\mathbf{w}, \mathbf{\tilde{x}}\rangle$, con $\mathbf{\tilde{x}} = (1, \mathbf{x})$. Si todos los elementos en $S_m$ son correctamente clasificados, entonces hemos terminado. Si existe algún dato $(\mathbf{x}_i, y_i)$ mal clasificado, entonces definimos $\mathbf{w}^{(2)} = \mathbf{w}^{(1)} + y_i\mathbf{\tilde{x}}_i$. Si este predictor clasifica bien a todos los elementos en el conjunto de entrenamiento, hemos terminado. Si no, entonces definimos otro predictor. En general, definimos $\mathbf{w}^{(t+1)} = \mathbf{w}^{(t)} + y_i\mathbf{\tilde{x}}_i$, donde $(\mathbf{x}_i, y_i)$ es un dato en el que el predictor $\mathbf{w}^{(t)}$ se equivoca. En clase demostramos que el número de iteraciones necesarias para encontrar el predictor correcto en el esquema de realizabilidad está acotado.

1. Implementa este algoritmo en **python**.

2. Consideremos ahora clasificación binaria en $\mathbb{R}^2$, bajo el supuesto de realizabilidad en la clase de predictores lineales. Supongamos que el predictor verdadero está dado por $\mathbf{w} = (-1,1,1)$. Grafica la frontera entre ambas clases de acuerdo a este clasificador.

3. Supón que la distribución sobre $\mathbb{R}^2$ es homogénea. ¿Cómo generas puntos aleatorios en $\mathbb{R}^2? $Para cada $m=1,\ldots,1000$, forma 100 conjuntos de entrenamiento $S_m$ y grafica el promedio de $R = \max_i \\{\|\|\mathbf{\tilde{x}}_i\|\|\\} $. Es decir, ¿cómo escala $R$ con el tamaño de la muestra?

4. Para cada $m=1,\ldots, 1000$, ejecuta el algoritmo de perceptrón y  grafica el número de pasos necesarios que le toma al algoritmo encontrar un vector $\mathbf{w}^*$ como función de $m$.

5. Para m = 100, grafica en $\mathbb{R}^2$ la secuencia de actualizaciones $\mathbf{w}^{(t)}$ de predictores hasta que clasifican correctamente a los datos de entrenamiento.