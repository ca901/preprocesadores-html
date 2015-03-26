#Handlebars 

Handlebars es una extensión de Mustache.js que tiene más prestaciones y mejor rendimiento. Si alguna vez hiciste algún template en Mustache.js no hay problema peusto que es compatible con Handlebars. Mustache tiene muchas implementaciones en muchos lenguajes de programación y es usado en multitud de sitios. Si queréis, podéis descubrir un poco más sobre Mustache en su web en Github.

####¿Por qué un sistema de plantillas?

Un sistema de plantillas permite definir de manera muy sencilla una “plantilla” para datos que vas a mostrar en el navegador para ser más limpio y legible que el común método de concatenar cadenas de caracteres dentro de una matriz mientras recorres un objeto que acabas de recibir (o crear) del servidor.

¿Y qué es una plantilla en sí? Bueno, las plantillas son código del lado del cliente que tienen expresiones para que la plantilla pueda recibir un objeto o una colección de ellos para renderizarlos fácilmente en código HTML.

Además, si trabajamos con diseñador, le resultará más sencillo modificar estas plantillas sin tener que enredar con el propio código.

####Instalando Handlebars

La forma más sencilla de instalar Handlebars.js es descargar la última versión del proyecto en Github, que actualmente va por la beta 6 de la versión 1.0. La inclusión es similar a la que haríamos con cualquier script:

####Ejemplos

Handlebars es realmente sencillo de usar y en los ejemplos que usaré para acompañar la explicación, veréis que la propia plantilla queda encapsulada en una etiqueta script con un tipo que el navegador no puede reconocer x-handlebars-template. Las variables y expresiones en Handlebars van encapsuladas entre dos llaves {{ y }}.


Ejemplo 1 – Hola mundo Función 13

Esta es nuestra plantilla:

<html>

    <script id="nuestra-plantilla" type="text/x-handlebars-template">
        <p>Hola {{usuario}}</p>
    </script>

</html>

####Ahora tenemos que compilar la plantilla:

<html>

    <script>
        var fuente = $('#nuestra-plantilla').html();
        var plantilla = Handlebars.compile(fuente);
    </script>
    
</html>


Ahora tenemos que pasar los datos, para ello voy a incluirlo en una variable, pero esta puede venir de cualquier sitio. Posteriormente vamos convertirla en HTML y adjuntarla al DOM.

<html>

    <script>
        var datos = {usuario : 'Función 13'};
        var html = plantilla(datos);
        $('#contenido').html(html);
    </script>
    
</html>

Lo cual resulta en:

<html>

    <p>Hola Función 13</p>

</html>

  ejemplo 2 Una lista : 

En el siguiente ejemplo vamos a ir un poco más lejos y vamos a iterar sobre un objeto JavaScript creando una lista de usuarios. Quizá este sea el uso más común:

<html>

<ul>
{{#each this}}
    <li><strong>Usuario</strong>: {{nombre}}
        <ul>
            <li><strong>Edad</strong>: {{edad}}</li>
        </ul>     
    </li>
{{/each}}
</ul>
</html>

Y los datos:

<html>

    <script>
    
        var datos = [
            {
                nombre: 'Matusalén',
                edad: 'Desconocida'
            },
            {
                nombre: 'Madonna',
                edad: 60
            }
        ];
    
    </script>
    
</html>


var datos = [
    {
        nombre: 'Matusalén',
        edad: 'Desconocida'
    },
    {
        nombre: 'Madonna',
        edad: 60
    }
];

Tendremos lo que buscábamos:
<html>

    <ul>
     
        <li><strong>Usuario</strong>: Matusalén
            <ul>
                <li><strong>Edad</strong>: Desconocida</li>
            </ul>        
        </li>
     
        <li><strong>Usuario</strong>: Madonna
            <ul>
                <li><strong>Edad</strong>: 60</li>
            </ul>        
        </li>
     
    </ul>
</html>

El bloque each, lo que hace es iterar sobre cada objeto (en este caso le pasamos como contexto el objeto completo this) y usar los datos que le estamos facilitando.
