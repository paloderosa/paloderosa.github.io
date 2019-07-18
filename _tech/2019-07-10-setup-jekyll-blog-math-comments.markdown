---
layout: post
title: Cómo montar un blog de Jekyll con matemáticas y comentarios
date: 2019-07-10 10:49:00
mathjax: true
comments: true
description: Describimos como montar un blog en Github Pages donde podamos publicar artículos matemáticos y tener comentarios
---

En esta entrada inicial vamos a montar un blog donde podamos publicar nuestros hallazgos matemáticos o simplemente cualquier cosa que queramos compartir. Para que satisfaga nuestras necesidades, vamos a implementar la posibilidad de escribir símbolos matemáticos con el menor sufrimiento posible, por un lado, y vamos a habilitar la escritura de comentarios por parte de otras personas. La manera en que vamos a implementar esto es relativamente estándar en la comunidad de programadores. Más formalmente, vamos a generar un blog usando **Jekyll** y lo vamos a publicar en **Github Pages**. A continuación explicamos todo esto. Como referencia, el código de mi blog se encuentra en [github.com/paloderosa/paloderosa.github.io](https://github.com/paloderosa/paloderosa.github.io).

### 1. Cuenta de Github
El primer paso en nuestra tarea es crear una cuenta en [github.com](https://github.com). Github es un sitio donde se pueden alojar repositorios de **git**. git es una herramiento para gestionar versiones de código. Además de crear una cuenta en Github, es necesario también que [descarguen git](https://git-scm.com/downloads). Para saber más del flujo de trabajo con git, te recomiendo mucho [esta guía](https://guides.github.com/introduction/git-handbook/). 

Una nueva funcionalidad de Github es que permite alojar páginas web personales o de organización o páginas web asociadas a repositorios o proyectos específicos. Nosotros vamos a crear una página personal. Como mi nombre de usuario es **paloderosa**, mi página alojada en Github Pages es [paloderosa.github.io](https://paloderosa.github.io). Esto no se produce automáticamente, sino que es resultado de un proceso. Cuando completemos este proceso, si el nombre de usuario en la cuenta que han creado es **usuario**, entonces su página quedará alojada en **usuario.github.io**.


### 2. Elegir una tema de Jekyll
Como dijimos que queremos montar un blog con el menor sufrimiento posible, vamos a usar temas prediseñados que personas han hecho y puesto de manera abierta en internet. Si no quisiéramos elegir un tema, tendríamos entonces que correr con todo el diseño y escritura de una página web. El término para buscar en **google** es [Jekyll themes](https://www.google.com/search?q=jekyll+themes&oq=jekyll+themes). Algunos lugares donde pueden buscar son:

- [jekyllthemes.io](https://jekyllthemes.io/)
- [jekyllthemes.org](http://jekyllthemes.org/)
- [www.wowthemes.net/jekyll-themes-templates/](https://www.wowthemes.net/jekyll-themes-templates/)

Nosotros hemos elegido un tema muy minimalista, [-folio](http://bogoli.github.io/-folio/), como punto de partida de nuestro blog. Lo que haremos será tomar ese tema, borrar las entradas de ejemplo y añadir las nuestras.

En mi caso, el código del tema se encuentra en [https://github.com/bogoli/-folio](https://github.com/bogoli/-folio). En la parte superior de esta página, damos *click* en **fork**.

<img class="col three right" src="/img/fork-template.png">

Esto genera una copia de este repositorio dentro de nuestra propia cuenta, es decir, ahora uno de *nuestros* repositorios es una copia del repositorio que contiene el tema. Después de haber dado *click* en *fork*, github nos redirige a la página de la copia del repositorio en nuestra cuenta. El repositorio en nuestra cuenta tiene el nombre del repositorio original. Es necesario que cambiemos el nombre el repositorio. Para esto, damos *click* en *Settings* y en el campo para renombrar al repositorio escribimos **usuario.github.io**, donde **usuario** es el usuario que elegimos.

<img class="col three right" src="/img/rename-repository.png">

Si visitamos la página **https://usuario.github.io**, podemos ver ahora la versión inicial de nuestro blog.

<img class="col three right" src="/img/initial-site.png">

¿Cómo modificamos ahora el código para publicar el contenido que queremos? Necesitar tener una copia en nuestra computadora que podamos modificar y después volver a poner en el repositorio de Github. Para descargar el repositorio a nuestra computadora, abrimos nuestra terminal. Elegimos una carpeta donde queramos albergar el repositorio y nos movemos en la terminal a esa carpeta,

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
Existen distintas maneras de habilitar la escritura de símbolos matemáticos en una página web, cada una con distinto nivel de dificultad y con distintos resultados. Para una página generada con Jekyll, la recomendación es usar una librería de **javascript** llamada **mathjax**.

Para habilitar **mathjax** en nuestro blog, hacemos lo siguiente. En los archivos del repositorio, existe una carpeta llamada <code>_includes</code>. Dentro de esta carpeta, creamos un archivo llamado <code>mathjax.html</code> con el siguiente contenido:

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

que es muy parecido a LaTeX. Puedes habilitar **mathjax** en algún post del tema original, modificando el encabezado, y agregar alguna ecuación.


### 4. Ejecutar los cambios en la página
Ahora que hemos realizado varias modificaciones, queremos poder observar esas modificaciones en nuestro blog. Todas las modificaciones fueron realizadas en la copia local de nuestro blog, de manera que cuando veamos <code>usuario.github.io</code> obviamente no se mostrará ningún cambio. Ubicando la terminal en nuestro repositorio, escribimos
{% highlight bash %}
git status
{% endhighlight %}
que mostrará todos los archivos que creamos o modificamos. Escribimos
{% highlight bash %}
git add .
git commit -m "Primera modificación al blog"
git push origin master
{% endhighlight %}

Si modificaste alguna entrada de ejemplo o agregaste alguna ecuación, debieras poder observar los resultados en **usuario.github.io**. Cada vez que hagas una modificación, tienes que repetir estos pasos.


### 5. Habilitar comentarios
Como queremos poder criticar nuestro trabajo, necesitamos habilitar comentarios. Igualmente aquí existen muchas opciones, cada una con distinto nivel de sufrimiento. Lo más sencillo y estándar es habilitar el sistema de comentarios de [disqus](https://disqus.com/).

Lo primero que se requiere es abrir una cuenta de [disqus](https://disqus.com/profile/signup/). Después de crear una cuenta, tenemos que registrar nuestra página en **disqus** en [https://disqus.com/admin/create/](https://disqus.com/admin/create/). Una vez que elijamos un nombre de página, **disqus** generará un nombre corto para la página, **usuario-github-io** en este caso. Seleccionamos una categoría y creamos el sitio.

<img class="col three right" src="/img/disqus-register.png">

Ahora, en el archivo <code>_config.yml</code> de nuestro repositorio local, debemos agregar las líneas
{% highlight yml %}
comments:
  provider: "disqus"
  disqus:
    shortname: "usuario-github-io"
{% endhighlight %}

En <code>shortname</code> sustituimos el nombre que haya generado **disqus**.

Ahora, en la carpeta <code>_includes</code>, creamos un archivo llamado <code>disqus.html</code> con el siguiente contenido:

{% highlight javascript %}
{% raw %}
{% if page.comments %}
{% endraw %}
	<div id="disqus_thread"></div>
    	<script>
    
    	/**
    	*  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
    	*  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables*/
    	
    	var disqus_config = function () {
    
    		this.page.url = {% raw %} "{{ page.url | absolute_url }}" {% endraw %};  // Replace PAGE_URL with your page's canonical URL variable
    		this.page.identifier = {% raw %} "{{ page.url }}" {% endraw %}; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
    	};
    	
    	(function() { // DON'T EDIT BELOW THIS LINE
    	var d = document, s = d.createElement('script');
    	s.src = {% raw %}'https://{{ site.comments.disqus.shortname }}.disqus.com/embed.js'{% endraw %};
    	s.setAttribute('data-timestamp', +new Date());
    	(d.head || d.body).appendChild(s);
    	})();
    	</script>
    	<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
                            
{% raw %}
{% endif %}
{% endraw %}
{% endhighlight %}

Abrimos el archivo <code>post.html</code> que se encuentra en la carpeta <code>_layouts</code> e incluimos la sección de comentarios en el lugar apropiado, al final del *tag* <code>article</code>, de la siguiente forma:

{% highlight html %}
<article class="post-content">
    .
    .
    .
    {% raw %}{% include disqus.html %} {% endraw %}
</article>
{% endhighlight %}

Para habilitar ahora comentarios en una entrada del blog, miramos de nuevo al encabezado de alguna de las entradas. El encabezado hasta el momento para esta entrada es

{% highlight markdown %}
---
layout: post
title: Cómo montar un blog de Jekyll con matemáticas y comentarios
date: 2019-07-10 10:49:00
mathjax: true
description: Describimos como montar un blog en Github Pages donde podamos publicar artículos matemáticos y tener comentarios
---
{% endhighlight %}

Si agregamos <code>comments: true</code>, de modo que el encabezado queda como

{% highlight markdown %}
---
layout: post
title: Cómo montar un blog de Jekyll con matemáticas y comentarios
date: 2019-07-10 10:49:00
description: Describimos como montar un blog en Github Pages donde podamos publicar artículos matemáticos y tener comentarios
mathjax: true
comments: true
---
{% endhighlight %}

debe de cargar al final de la página. Para ver los resultados, hacemos de nuevo
{% highlight bash %}
git add .
git commit -m "Comentarios de disqus habilitados"
git push origin master
{% endhighlight %}


### 6. Generar el blog localmente
Como habrás visto, es un poco tedioso el proceso de agregar o modificar contenido a nuestro blog, hacer todo el proceso en git y ver los resultados en la página. Sólo hasta que completamos todo este procedimiento podemos saber si el resultado coincide con lo que pretendíamos.

Cuando alojamos nuestra página en el repositorio remoto de Github, Github procesa el contenido y genera los archivos de la página. Lo que nosotros escribimos localmente no coincide con el código de lo que termina publicado en el blog; esto último es el resultado de la compilación de nuestro código.

Nosotros podemos hacer la compilación localmente y ver en tiempo real las modificaciones que hagamos, en lugar de hacer todo el proceso anterior. A continuación nos guiamos por las instrucciones que [Github nos indica](https://help.github.com/en/articles/setting-up-your-github-pages-site-locally-with-jekyll). Sin embargo, algunos de los pasos que ahí se indican ya los hemos realizado, así que sólo es necesario realizar los pasos que se indican en los Requisitos, Paso 2 y Paso 4.

Lo primero es abrir la terminal y verificar que tenemos un programa que se llama **ruby**. Escribimos
{% highlight bash %}
ruby --version
{% endhighlight %}
Si aparece algo, ya lo tenemos. En macOS y Linux, **ruby** suele estar instalado como parte del sistema operativo. En Windows esto no es así. Entonces hay que instalar **ruby** [aquí](https://www.ruby-lang.org/en/downloads/). Debemos de tener la versión 2.1.0 o más reciente.

Una vez que tengamos **ruby**, instalamos **bundler** con
{% highlight bash %}
gem install bundler
{% endhighlight %}

Ahora, buscamos en el repositorio local el archivo <code>Gemfile</code>. Si no existe, creamos un archivo llamado <code>Gemfile</code> (sin extensión) con el siguiente contenido:
{% highlight bash %}
source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
{% endhighlight %}
 Si el archivo <code>Gemfile</code> ya existe, sólo agregamos las líneas anteriores al contenido del archivo.
 
Instalamos ahora Jekyll. Ubicamos la terminal en el repositorio local y escribimos
{% highlight bash %}
bundle install
{% endhighlight %}
Esto instala Jekyll y lee el contenido de <code>Gemfile</code> para decidir qué dependencias adicionales instalar.

Finalmente, escribimos en la terminal
{% highlight bash %}
bundle exec jekyll serve
{% endhighlight %}
y abrimos la dirección [http://127.0.0.1:4000/](http://127.0.0.1:4000/), donde podemos ver el resultado de nuestro código. Cuando hagamos una modificación, recargamos la página y debiéramos ver las modificaciones. El generador de Jekyll se mantendrá corriendo en la terminal hasta que lo interrumpamos con <code>Ctrl+C</code>.

Cuando tengamos una versión de nuestro blog que queramos publicar a la página, repetimos el proceso
{% highlight bash %}
git add .
git commit -m "Comentarios de disqus habilitados"
git push origin master
{% endhighlight %}

### 7. Siguientes pasos
Casi todo de lo que mencionamos probablemente sea nuevo para todos. A continuación menciono algunas referencias o ideas para empezar a generar nuestras propias entradas y experimentar con la estructura del blog.

1. Prueba a modificar la estructura del archivo <code>_config.yml</code>. Aquí puedes modificar la estructura del blog, añadir o quitar secciones, personalizar datos del blog.

2. Revisar la [documentación de Jekyll](https://jekyllrb.com/docs/).

3. El contenido del blog se escribe en un lenguaje llamado **markdown**, que es una simplificación de **html**. Puedes consultar [esta guía rápida](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) de **markdown**.