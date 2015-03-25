
#HAML
HAML (HTML abstraction markup language) se basa en que el código sea bonito, simple y que acelere y simplifique la creación de código.
Haml es un markup lenguage que se utiliza para escribir el código HTML de cualquier documento web sin el uso de código en línea. Haml funciona como un reemplazo para sistemas de plantillas de página en línea tales como PHP, ASP y ERB, el lenguaje de plantillas utilizado en mayoría Ruby on Rails. Sin embargo, Haml evita la necesidad de forma explícita la codificación HTML en la plantilla, porque él es sí mismo una descripción del HTML, con un código para generar contenido dinámico.


Principios 
Haml se basa en varios principios fundamentales para lograr lo que quieren.  Estos son:

-El markup 
No debe utilizarse como una herramienta simple para navegadores para representar una página cómo el desarrollador quiere que se vea. La representación no es lo único que la gente tiene que ver; tienen que ver, modificar y comprender como es el markup.


-El markup debe quedar bien
Haml automáticamente cierra y pone las etiquetas como se debe

-El HTML debe ser claro
XML y HTML son formatos basados en la idea de un documento estructurado. Esa estructura se refleja en su markup y asimismo debe ser reflejada en meta-marcado como lógica de Haml porque Haml se basa en la de elementos secundarios (child elements), esta estructura se conserva naturalmente, haciendo el documento mucho más fácil, más lógico y más simples de leer para el usuario.


Características:

* Whitespace activo
* Markup bien formateado
* Sigue las convenciones CSS
* Integra código Ruby
* Implementa Rails templates con la extención .haml


Usar Haml:

1. Como una herramienta de lineas de comando
2. Como un plugin de Ruby on Rails
3. Como un módulo independiente Rubí.


Texto sin formato
Una parte importante de cualquier documento HTML es su contenido, que es texto sin formato. Cualquier línea de Haml que es interpretado como algo más, es tomado como texto sin formato, y pasan sin modificarse. Por ejemplo:
<pre>
%gee   %whiz     Wow this is cool!
</pre>
Es completado como:
<pre>
<gee>   <whiz>     Wow this is cool!   </whiz> </gee>
</pre>


Atributos de estilo de HTML: ()
Haml también apoya una sintaxis de atributo más concisa, menos la syntaxis de Ruby que esta basada en los atributos de HTML. Éstos son usados con paréntesis en vez de corchetes, como se muestra a continuación:
<pre>
%html(xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en")
</pre>
Las variables de Ruby pueden utilizarse omitiendo las comillas. Pueden utilizar variables locales o las variables de instancia. Por ejemplo:
<pre>
%a(title=@title href=href) Stuff
</pre>
Esto es igual a:
<pre>
%a{:title => @title, :href => href} Stuff
</pre>
Porque no hay comas separando los atributos, sin embargo, las expresiones más complicadas no están permitidas. Para los que tendrás que utilizar la sintaxis {}. Sin embargo, puede utilizar juntos dos sintaxis:
<pre>
%a(title=@title){:href => @link.href} Stuff
</pre>
Tambien se puede usar #{} para insertar expresiones complicadas en un atributo de estilo HTML:
<pre>
%span(class="widget_#{@widget.number}")
</pre>
Atributos de estilo HTML se pueden poner a través de varias líneas como atributos de hash-estilo:
<pre>
%script(type="text/javascript"         src="javascripts/script_#{2 + 7}")
</pre>

Class and ID: . and #
El signo de punto y el numeral son representativos de CSS. Se utilizan como métodos abreviados para especificar los atributos class e id de un elemento, respectivamente. Varios nombres de clases pueden especificarse en forma similar al CSS, encadenando los nombres de clase con puntos. Se colocan inmediatamente después de la etiqueta y antes un hash de atributos. Por ejemplo:
%div#things   %span#rice Chicken Fried   %p.beans{ :food => 'true' } The magical fruit   %h1.class.otherclass#id La La La
se compila:
<pre>
<div id='things'>   <span id='rice'>Chicken Fried</span>  
 <p class='beans' food='true'>The magical fruit</p>   
 <h1 class='class otherclass' id='id'>La La La</h1> </div>
 </pre>

Estos métodos abreviados pueden combinarse como una larga cadena de atributos; los dos valores serán fusionados como si todos se colocaron en un array. Por ejemplo:
%div#Article.article.entry{:id => @article.number, :class => @article.visibility}
Esto es igual a:
%div{:id => ['Article', @article.number], :class => ['article', 'entry', @article.visibility]} Gabba Hey
Se podría compilar como:
<div class="article entry visible" id="Article_27">Gabba Hey</div>


HTML Comments: /
El carácter de barra inclinada, cuando se coloca al principio de la línea, envuelve todo el texto en un comentario de HTML. Por ejemplo:
%peanutbutterjelly   / This is the peanutbutterjelly element   I like sandwiches!
se compila como:
<pre>
	<peanutbutterjelly>   <!-- This is the peanutbutterjelly element -->   I like sandwiches! </peanutbutterjelly>
</pre>

La barra inclinada también pueden envolver con sangría secciones de código. Por ejemplo:
/   %p This doesn't render...   %div     %h1 Because it's commented out!
se compila como:
<!--   <p>This doesn't render...</p>   <div>     <h1>Because it's commented out!</h1>   </div> -->


Haml Comments: -#
El guión seguido inmediatamente por el signo de número, significa un comentario silencioso. Cualquier texto que sigue a esto no es tomado en el documento resultante en absoluto. Por ejemplo:
%p foo -# This is a comment %p bar
is compiled to:
<pre>
<p>foo</p> <p>bar</p>
También puede unir texto debajo de una observación silenciosa. Por ejemplo:
%p foo -#   This won't be displayed     Nor will this                    Nor will this. %p bar
is compiled to:
<p>foo</p> <p>bar</p>
</pre>


##Filters

Los dos puntos indican un filtro. Esto permite pasar un bloque de texto con sangría como entrada a otro programa de filtrado y añadir el resultado a la salida de Haml. La sintaxis es simplemente con dos puntos seguidos por el nombre del filtro. Por ejemplo:
<pre>
%p   :markdown     # Greetings      Hello, *World*
se compila como:
<p>   <h1>Greetings</h1>    <p>Hello, <em>World</em></p> </p>
</pre>

Los filtros podrían tener código de Ruby incorporado con #{}. 
Por ejemplo:
- flavor = "raspberry" #content   :textile     I *really* prefer _#{flavor}_ jam.
se compila como:
<pre>
<div id='content'>   <p>I <strong>really</strong> prefer <em>raspberry</em> jam.</p> </div>
</pre>
Estos son algunos de los filtros de Haml:

:cdata 
rodea el texto filtrado con etiquetas CDATA.

:coffee
compila el texto filtrado a Javascript usando Cofeescript. También puede hacer referencia a este filtro como  :coffeescript. Este filtro se implementa con Tilt.

:css 
rodea el texto con un filtro de <style></style> y opcionalmente con etiquetas CDATA . Se usa mucho para las líneas de CSS

:javascript
rodea el texto con un filtro de <script> y opcionalmente con etiquetas CDATA . Se usa mucho para las líneas de JS
:less
Analiza el texto filtrado con menos para producir la salida CSS. Este filtro se implementa con Tilt.


Referencias:

http://haml.info
http://haml.info/docs.html
http://haml.info/docs/yardoc/file.REFERENCE.html
