#Twig

Twig es un motor de plantillas construido en PHP. ¿Y qué es eso de un motor de plantillas? Pues es una herramienta para eliminar la duplicación en HTML mediante la reutilización de plantillas.


A la hora de construir una página web solemos tener en cuenta evitar la duplicación de código en los controladores. ¿Pero qué pasa con los ficheros HTML? Si lo piensas, tienen toneladas de código duplicado, como pueden ser los menús inferior y superior, el sidebar lateral, la etiqueta <head> y todo su contenido, los ficheros js que incluimos al final de la plantilla… Cada página de nuestra web debe incluir todos esos elementos, y si no usamos un gestor de plantillas nos veremos obligados a copiarlos y pegarlos en cada una de nuestras páginas.

Pues bien, Twig soluciona este problema permitiéndonos usar herencia en nuestras plantillas, de forma muy similar a cómo se hace en la programación orientada a objetos. Lo único que tenemos que hacer es identificar aquellos elementos de nuestra web que sean comunes a todas las páginas, para de esa forma separarlos en una plantilla propia, y luego diseñar el resto de plantillas simplemente heredando de la “plantilla padre”.

##¿Cómo puedo eliminar la duplicación en HTML con Twig?

Vamos a verlo en código. Lo primero que haremos será diseñar la plantilla que tendrá todos los elementos inmutables de nuestra web, a la que llamaré base.html.twig:

<html>
    <head>
        <title>Mi web</title>
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta http-equiv="Content-Type" content="text/html;charset=UTF-8">
        <link href="css/styles.css" type="text/css" rel="stylesheet">
        <link rel="icon" type="image/x-icon" href="img/favicon.ico" />
    </head>
 
    <body>
        <nav class="navbar">
            <ul>
                <li><a href="http://miweb.com/quienes-somos">Quiénes somos</a></li>
                <li><a href="http://miweb.com/calendario">Calendario</a></li>
                <li><a href="http://miweb.com/contacto">Contacto</a></li>
            </ul>
        </nav>
 
        <div class="cuerpo">
            {% block body_content %}
            {% endblock %}
        </div>
 
        <footer class="footer">
            <ul>
                <li><a href="http://miweb.com/aviso-legal">Aviso legal</a></li>
                <li><a href="http://miweb.com/politica-privacidad">Política de privacidad</a></li>
            </ul>
        </footer>
 
        <script src="js/jquery-2.1.0.min.js"></script>
    </body>
</html>

Ok, ¿qué hemos hecho? Nada especial, realmente. Sólo hemos creado el diseño base, a partir del cual construiremos el resto de plantillas de nuestra web. Hemos creado menús superiores e inferiores, hemos puesto todo el contenido de la etiqueta "head" y hemos puesto también, al final del fichero, los scripts que necesitamos. Hay varias etiquetas HTML5, como "nav" y "footer", pero seguro que te resultan familiares.

La novedad está en el bloque body_content, delimitado por llaves y porcentajes. El contenido de este bloque será especificado en las plantillas que hereden de ésta. Por ejemplo, fíjate cómo quedaría el código de la plantilla de la página de inicio de nuestra web, a la que llamaremos index.html.twig:

<pre>
{% extends 'base.html.twig' %}
 
{% block body_content %}
    <!-- Contenido del index -->
{% endblock %}
</pre>
Facilísimo, ¿verdad? La primera línea indica que estamos extendiendo la plantilla base.html.twig, que definimos anteriormente. Después sólo tenemos que escribir el código que queremos que se muestre dentro del bloque body_content.

El procedimiento sería exactamente el mismo para el resto de páginas de nuestra web: quiénes somos, calendario, contacto, etc.

¿Qué pasa si sólo quiero sustituir el contenido de una sección en unas pocas páginas, y no en todas?

No habría ningún problema. Imagina que por ejemplo queremos cambiar el valor de la etiqueta <title> para cada página en la que estemos, para así darle un pequeño impulso al SEO de nuestra web. En nuestra plantilla base, sólo tendríamos que añadir el siguiente código a la etiqueta title:

<pre>
<title>{% block title %}Mi web{% endblock %}</title>
</pre>
En la plantilla index no tendríamos que hacer nada, ya que el valor por defecto nos parece correcto. Sin embargo, en la página de contacto queremos hacer algo como esto:

<pre>
{% extends 'base.html.twig' %}
 
{% block title %}
    Mi web - Contacto
{% endblock %}
 
{% block body_content %}
    <!-- Formulario de contacto de la web -->
{% endblock %}
</pre>
Como ves, esta plantilla es similar a la del index: extendemos la plantilla base y definimos el bloque body_content, pero además definimos el bloque title para mostrar un título específico para esta página.

La moraleja es que la sustitución del contenido de un bloque es opcional, no tenemos por qué hacerlo si no nos interesa.

¿Y qué pasa si no quiero sustituir el bloque, sino añadir contenido adicional?

También se puede hacer. Un problema típico suele ser cuando queremos usar una librería Javascript en una, y sólo una, página de nuestra web. Por ejemplo, un calendario.

La solución es similar a la del ejemplo de la etiqueta title. Lo primero sería modificar nuestra plantilla base para incluir nuestros scripts dentro de su propio bloque:

<pre>
{% block javascript %}
    <script src="js/jquery-2.1.0.min.js"></script>
{% endblock %}
</pre>
Una vez hecho esto, veamos cómo quedaría la plantilla de nuestro calendario:

<pre>
{% extends 'base.html.twig' %}
 
{% block title %}
    Mi web - Calendario
{% endblock %}
 
{% block body_content %}
    <!-- Calendario de la web -->
{% endblock %}
 
{% block javascript %}
    {{ parent() }}
 
    <script src="js/jquery.pickmeup.min.js”></script>
{% endblock %}
</pre>
La novedad está en la función parent, que lo único que hace es devolver el contenido del bloque Javascript tal cual está definido en la plantilla padre, que en este caso es base.html.twig. De esta forma tan sencilla, podemos añadir nuevo código a los bloques que ya fueron definidos en otras plantillas.
