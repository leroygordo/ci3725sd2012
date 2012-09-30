**Consulta 1:** 

Te escribo para preguntarte como prefieren ustedes que se realice el proyecto, en la página proponen un ejemplo donde colocan muchos de los nombres de los tokens en lista y manejan muchos casos con una sola expresión regular, que está dentro de una función. O prefieren que se realice una expresión por cada token?

> (...) nota que la diferencia de definir los tokens en lista y como funcion depende del token a reconocer. La funcion te permite hacer una accion sobre token, por ejemplo, extraer el valor.

> En PLY, esa lista corresponde a las palabras reservadas de Gisela. Ustedes son libres de escoger las decisiones de desarrollo de su proyecto.

**Consulta 2:**

cito, en el enunciado de la primera entrega:

"Las cadenas de caracteres encerradas entre comillas. Debe ser un único token cuyo contenido sea la cadena leída."

Comillas simples, dobles o ambas?

> Ambas. Si están encerrados entre comillas simples, no puede haber alguna comilla simple dentro de esta cadena, el mismo caso se aplica a las comillas dobles.

**Consulta 3:**

si tengo este código en gisela:

go<br>
  print **'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;()&nbsp;&nbsp;&nbsp;&&nbsp;&nbsp;&nbsp;"  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;] $ % % @!~` -123 lll$%[]{} ;: \  $ sd '   z;<br>
  char x:= 'a'**<br>
og

El lexer me devuelve lo siguiente: 
TkINI\_BLOQUE "go" (Linea 1, Columna 1)
TkPRINT "print" (Linea 2, Columna 4)
TkCADENA "'         ()  &    "  ;      ] $ % % @!~` -123 lll$%[]{} ;: \  $ sd ' z;
  char x:='a'" (Linea 2, Columna 10)
TkFIN_BLOQUE "og" (Linea 3, Columna 2)

Es decir me reconoce como un token "cadena" todo lo que esta entre las comillas simples que estan en **rojo**. Esto es porque las cadenas permiten todos los caracteres ASCII. Al permitir en las cadenas el "\n" y las comillas simples, el lexer toma como una cadena desde la primera comilla simple que encuentra hasta la ultima.

Yo pienso que las cadenas que empiezan con comilla simple ( ' ) no deberian poder contener la comilla simple, pero si las dobles. Lo mismo pasa con las cadenas que empiezan con comillas dobles ( " ), estan no deben contener las comillas dobles. 

> Estás en lo cierto. La consulta anterior a ésta responde tu pregunta. Por otra parte, la cadena de caracteres sólo estarán en una línea, por lo tanto, saltos de líneas "\n" no estará permitido en una cadena de caracteres.

**Consulta 4:**

Tenemos la siguiente duda
1. ¿El archivo .gsl del q leerá pueda estar en otra carpeta que no sea en la actual que se está corriendo el programa?

Y no sabemos como escribir la expresion regular para reconocer la palabra reservada let's
hemos intentado con cosas del estilo
 let\'s
let\\\'s
let(\\\')s
let(\')s

pero no funciona, simplemente reconoce el let como un identificador y la comilla simple la ve como una caracter inesperado.

> Piensa mejor cómo reconocer "let's". No está mal que te reconozca éste como varios tokens. Una solución rápida podrías controlarla con el análisis sintáctico.