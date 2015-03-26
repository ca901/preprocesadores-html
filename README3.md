#Slim
Slim es un lenguaje de plantillas, cuyo objetivo es reducir la sintaxis de las partes esenciales sin llegar a ser críptico.

El diseño inicial de Slim es lo que se ve en la página principal. Comenzó como un ejercicio para ver cuánto podría ser eliminada de una plantilla estándar HTML (<,>, etiquetas de cierre, etc ...). A medida que más personas se interesaron por Slim, la funcionalidad creció y también lo hizo la flexibilidad de la sintaxis.

Slim se esfuerzan por mantener la simplicidad, pero la definición no todo el mundo de una sintaxis legible es la misma. La documentación le mostrará las opciones.

Slim utiliza Temple y Tilt. 

####¿Por qué utilizar Slim?

Slim le permite escribir plantillas muy mínimos que son fáciles de mantener y prácticamente garantiza que usted escribe HTML bien formado y XML.
También pensamos que la sintaxis Slim también es estético y lo hace mucho más divertido de escribir plantillas. Ya que se puede utilizar slim como un gota en el reemplazo de todo el marco principal se puede empezar fácilmente.
La arquitectura Slim es muy flexible y permite escribir extensiones y plugins de sintaxis.

Sí, Slim es rápido! slim fue desarrollado desde el principio con el rendimiento en mente. Los puntos de referencia se realizan para cada confirmación en http://travis-ci.org/slim-template/slim. No te fíes de los números? Eso es como debe ser. Por favor, intente la tarea rake referencia a ti mismo!

Sin embargo, en nuestra opinión debería usar delgado debido a sus características y sintaxis. Acabamos de garantizar que Slim no tiene un impacto negativo en el rendimiento de la aplicación.



Ejemplo de sintaxis

Aquí está un ejemplo rápido para demostrar lo que una plantilla slim se ve así:

<html>

    <head>
        title Slim Examples
        meta name="keywords" content="template language"
        meta name="author" content=author
        link rel="icon" type="image/png" href=file_path("favicon.png")
        javascript:
          alert('Slim supports embedded javascript!')
    </head>
      
    <body>
  
        h1 Markup examples
    
        #content
          p This example shows you how a basic Slim file looks.
    
        == yield
    
        - if items.any?
          table#items
            - for item in items
              tr
                td.name = item.name
                td.price = item.price
        - else
          p No items found. Please add some inventory.
            Thank you!
    
        div id="footer"
          == render 'footer'
          | Copyright &copy; #{@year} #{@author}
    </body>
      
</html>


 Asuntos de sangría, pero la profundidad de penetración se pueden elegir a su gusto. Si quieres primer guión 2 espacios, luego 5 espacios, es tu elección. Para anidar marcado sólo necesitas guión por un espacio, el resto es salsa.


 Verbatim text | :

 La tubería dice Delgado para copiar sólo la línea. En esencia, escapa a cualquier procesamiento. Cada línea siguiente que se sangría mayor que la tubería se copia.

<pre>
 body
  p
    |
      This is a test of the text block.
      
</pre>

 Inline html <  

 Usted puede escribir etiquetas HTML directamente en delgado que le permite escribir sus plantillas en una más html como el estilo con etiquetas de cierre o mezclar html y estilo Slim. Los principales <obras como un implícito |:

<html>

  <body>
    - if articles.empty?
    - else
      table
        - articles.each do |a|
          <tr><td>#{a.name}</td><td>#{a.description}</td></tr>
  </body>
  
</html>



atributos

Usted escribe atributos directamente después de la etiqueta. Para los atributos de texto normal, debe utilizar comillas dobles "" o individuales (atributos entre comillas


    a href="http://slim-lang.com" title='Slim Homepage' Goto the Slim homepage





atributos wrapper 

Si un delimitador hace la sintaxis más legible para usted, puede utilizar los caracteres {...}, (...), [...] para envolver los atributos. Puede configurar estos símbolos (véase la opción: attr_list_delims).


body
  h1(id="logo") = page_logo
  h2[id="tagline" class="small tagline"] = page_tagline


  Si envuelve los atributos, puede distribuirlos a través de varias líneas:


  h2[id="tagline"
   class="small tagline"] = page_tagline




   Usted puede usar los espacios alrededor de las envolturas y assignments:


			h1 id = "logo" = page_logo
			h2 [ id = "tagline" ] = page_tagline






		Configuración Slim :

		Slim y el marco Temple subyacente son altamente configurable. La manera cómo se configure slim depende un poco sobre el mecanismo de compilación (Rails o inclinación). Siempre es posible establecer opciones predeterminadas por clase slim :: Engine. Esto se puede hacer en los archivos de entorno de Rails. Por ejemplo, en config / entornos / development.rb es probable que desee:
