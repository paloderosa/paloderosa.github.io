---
layout: post
title: Cómo montar un blog de Jekyll con matemáticas y comentarios
date: 2019-07-10 10:49:00
mathjax: true
description: Describimos como montar un blog en Github Pages donde podamos publicar artículos matemáticos y tener comentarios
---

En esta entrada inicial vamos a montar un blog donde publicar nuestros hallazgos matemáticos. Para que satisfaga nuestras necesidades, vamos a implementar la posibilidad de escribir símbolos matemáticos con el menor sufrimiento posible, por un lado, y vamos a habilitar la escritura de comentarios por parte de otras personas. La manera en que vamos a implementar esto es relativamente estándar en la comunidad de programadores. Más formalmente, vamos a generar un blog usando **Jekyll** y lo vamos a publicar en **Github Pages**. A continuación explicamos todo esto.
{: style="text-align: justify"}

### 1. Cuenta de Github
El primer paso en nuestra tarea es crear una cuenta en [github.com](https://github.com). Github es un sitio donde se pueden alojar repositorios de **git**. git es una herramiento para gestionar versiones de código. Además de crear una cuenta en Github, es necesario también que [descarguen git](https://git-scm.com/downloads). Para saber más del flujo de trabajo con git, te recomendamos mucho [esta guía](https://guides.github.com/introduction/git-handbook/). 
{: style="text-align: justify"}

Una nueva funcionalidad de Github es que permite alojar páginas web personales o de organización o páginas web asociadas a repositorios o proyectos específicos. Nosotros vamos a crear una página personal. Como mi nombre de usuario es **paloderosa**, mi página alojada en Github Pages es [paloderosa.github.io](https://paloderosa.github.io). Esto no se produce automáticamente, sino que es resultado de un proceso. Cuando completemos este proceso, si el nombre de usuario en la cuenta que han creado es **usuario**, entonces su página quedará alojada en **usuario.github.io**.
{: style="text-align: justify"}


### 2. Elegir una tema de Jekyll
Como dijimos que queremos montar un blog con el menor sufrimiento posible, vamos a usar temas prediseñados que personas han hecho y puesto de manera abierta en internet. Si no quisiéramos elegir un tema, tendríamos entonces que correr con todo el diseño y escritura de una página web. El término para buscar en **google** es [Jekyll themes](https://www.google.com/search?q=jekyll+themes&oq=jekyll+themes). Algunos lugares donde pueden buscar son:

- [jekyllthemes.io](https://jekyllthemes.io/)
- [jekyllthemes.org](http://jekyllthemes.org/)
- [www.wowthemes.net/jekyll-themes-templates/](https://www.wowthemes.net/jekyll-themes-templates/)

Nosotros hemos elegido un tema muy minimalista, [-folio](http://bogoli.github.io/-folio/), como punto de partida de nuestro blog. Lo que haremos será tomar ese tema, borrar las entradas de ejemplo y añadir las nuestras. 

En mi caso, el tema se encuentra en [https://github.com/bogoli/-folio](https://github.com/bogoli/-folio). En esta página, damos *click* en **fork**, en el repositorio.

<img class="col three right" src="/img/fork-template.png">

Esto genera una copia de este repositorio dentro de nuestra propia cuenta, es decir, ahora uno de *nuestros* repositorios es una copia del repositorio que contiene el tema. Después de que haber dado *click* en *fork*, github nos redirige a la página de la copia del repositorio en nuestra cuenta. El repositorio en nuestra cuenta tiene el nombre del repositorio original. Es necesario que cambiemos el nombre el repositorio. Para esto, damos *click* en *Settings* y en el campo para renombrar al repositorio escribimos **usuario.github.io**, donde **usuario** es el usuario que elegimos.

<img class="col three right" src="/img/rename-repository.png">

Si visitamos la página **https://usuario.github.io**, podemos ver ahora la versión inicial de nuestro blog.

<img class="col three right" src="/img/initial-site.png">

¿Cómo modificamos ahora el código para publicar el contenido que queremos? Necesitar tener una copia en nuestra computadora que podamos modificar y después volver a poner en el repositorio de Github. Para descargar el repositorio a nuestra computadora, abrimos nuestro la línea de comandos. Elegimos una carpeta donde queramos albergar el repositorio y nos movemos en la línea de comandos a esa carpeta,

{% highlight bash %}
cd /ruta-a-carpeta/
{% endhighlight %}

Descargamos una copia local del repositorio y nos movemos al repositorio con

{% highlight bash %}
git clone https://github.com/usuario/usuario.github.io.git
cd usuario.github.io
{% endhighlight %}

Esto, además, inicia un repositorio local. Para ver en cualquier momento el estado de nuestro repositorio, escribimos
{% highlight bash %}
git status
{% endhighlight %}


### 3. Habilitar símbolos matemáticos
Existen distintas maneras de habilitar la escritura de símbolos matemáticos en una página web, cada una con distinto nivel de dificultad y con distintos resultados. Para una página generada con Jekyll, la recomendación es usar una librería de **Javascript** llamada **Mathjax**.

Para habilitar **Mathjax** en nuestro blog, hacemos lo siguiente. En los archivos del repositorio, existe una carpeta llamada <code>_includes</code>. Dentro de esta carpeta, creamos un archivo llamado <code>mathjax.html</code> con el siguiente contenido:

{% highlight javascript %}
{% raw %}
{% if page.mathjax %}
{% endraw %}
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath: [ ['$','$'], ["\\(","\\)"] ],
      processEscapes: true
    }
  });
</script>
<script
  type="text/javascript"
  charset="utf-8"
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"
>
</script>
{% raw %}
{% endif %}
{% endraw %}
{% endhighlight %}

Guardamos este archivo. Ahora tenemos que incluir esta sección de código en las páginas donde queremos poder escribir matemáticas. Normalmente, nos interesa poder escribir matemáticas en cualquiera de nuestras entradas. En otra carpeta de nuestro repositorio, en <code>_layout</code>, existe un archivo llamado <code>post.html</code>. El inicio del archivo es de la siguiente forma:
{% highlight markdown %}
---
layout: default
---
.
.
.
{% endhighlight %}

Incluimos el archivo actual en este inicio:
{% highlight markdown %}
---
layout: default
---
{% raw %}
{% include mathjax.html %}
{% endraw %}
.
.
.
{% endhighlight %}

Observemos ahora el encabezado de alguna entrada de ejemplo del tema que descargamos. El encabezado de este artículo, por ejemplo, es el siguiente.

{% highlight markdown %}
---
layout: post
title: Cómo montar un blog de Jekyll con matemáticas y comentarios
date: 2019-07-10 10:49:00
description: Describimos como montar un blog en Github Pages donde podamos publicar artículos matemáticos y tener comentarios
---
{% endhighlight %}

La primera línea con <code>layout: post</code> indica que el formato de la entrada es el que esté definido en el archivo <code>post.html</code> que acabamos de ver. En este momento, no está habilitada la inclusión de símbolos matemáticos. Para habilitar esta inclusión, tenemos que incluir <code>mathjax: true</code> al encabezado, de modo que resulte en:
{% highlight markdown %}
---
layout: post
title: Cómo montar un blog de Jekyll con matemáticas y comentarios
date: 2019-07-10 10:49:00
description: Describimos como montar un blog en Github Pages donde podamos publicar artículos matemáticos y tener comentarios
mathjax: true
---
{% endhighlight %}

En este momento, ya podemos incluir símbolos matemáticos. Por ejemplo, el texto

>En clase, iniciamos la definición del esquema de aprendizaje PAC (Probably Approximately Correct). Bajo ciertas simplificaciones, dado un parámetro de confianza $\delta$ y un error $\epsilon$, encontramos el número mínimo de datos de entrenamiento en $S$ tal que el error de generalización $L_{(D,f)}(h_S)$ para el predictor $h_S$ resultado de ERM$_H$ satisface $$L_{(D,f)}(h_S)<\epsilon$$ con probabilidad $1-\delta$.

resulta de escribir

{% highlight TeX %}
En clase, iniciamos la definición del esquema de aprendizaje PAC
(Probably Approximately Correct). Bajo ciertas simplificaciones,
dado un parámetro de confianza $\delta$ y un error $\epsilon$,
encontramos el número mínimo de datos de entrenamiento en $S$
tal que el error de generalización $L_{(D,f)}(h_S)$ para el
predictor $h_S$ resultado de ERM$_H$ satisface $L_{(D,f)}(h_S)<\epsilon$
con probabilidad $1-\delta$.
{% endhighlight %}

Puedes habilitar **mathjax** en algún post del tema original, modificando el encabezado, y agregar alguna ecuación.


### 4. Ejecutando los cambios en la página
Ahora que hemos realizado varias modificaciones, queremos poder observar esas modificaciones en nuestro blog. Todas las modificaciones fueron realizadas en la copia local de nuestro blog, de manera que cuando veamos <code>usuario.github.io</code> obviamente no se mostrará ningún cambio. Ubicando la línea de comandos en nuestro repositorio, escribimos
{% highlight bash %}
git status
{% endhighlight %}
que mostrará todos los archivos que creamos o modificamos. Escribimos
{% highlight bash %}
git add .
git commit -m "Primera modificación al blog"
git push origin master
{% endhighlight %}

Para observar las modificaciones que hagamos, tendremos que repetir estos pasos.