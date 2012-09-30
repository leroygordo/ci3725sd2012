Universidad Simón Bolívar<br>
Departamento de Computación y Tecnología de la Información<br>
CI3725 - Traductores e Interpretadores<br>
Septiembre - Diciembre 2012

# Entrega 1 (5%)
## Análisis Lexicográfico

Esta entrega consiste en la implantación de un analizador lexicográfico
para el lenguaje Gisela, el cual constituye la primera fase del interpretador
que se desea construir a lo largo del trimestre. Basado en la definición
del lenguaje, disponible en la página oficial del laboratorio, deberá identificar
los *tokens* relevantes, formular expresiones regulares que los reconozcan, e
implantar el analizador utilizando la herramienta generadora que le corresponda.

Entre los tokens relevantes del lenguaje se encuentran:

* Cada palabra reservada del lenguaje Gisela.

* Los identificadores de variables, procedimientos y constantes. Debe ser un único token
  cuyo contenido sea el nombre del identificador asociado.

* Cada símbolo utilizado para denotar operadores y separadores.

* Los números enteros. Debe ser un único token cuyo contenido sea el número reconocido.

* Los caracteres literales. Debe ser un único token cuyo contenido sea el caracter.

* Las constantes booleanas.

* Las cadenas de caracteres encerradas entre comillas. Debe ser un único token cuyo contenido
  sea la cadena leída.

Otras consideraciones:
  
* Los espacios en blanco, tabuladores, saltos de línea y comentarios deben ser ignorados.
  Es inaceptable manejarlos como tokens.

* Se debe preservar la diferencia entre mayúsculas y minúsculas.

Su programa principal debe llamarse *gisela* y recibir como primer argumento el archivo a
analizar. La salida debe mostrar todos los tokens reconocidos de manera legible e incluyendo
para cada uno la línea y columna donde se encontró. Por ejemplo:

    $ gisela prueba.gsl
    TkIdentificador "variable" (Línea 1, Columna 1)
    TkIgual "=" (Línea 1, Columna 15)
    TkEntero 400 (Línea 2, Columna 1)
    ...

En caso de encontrar errores léxicos, debe mostrar *todos* y *sólo* los errores encontrados.
La salida no puede tener una mezcla de tokens reconocidos y errores léxicos. Es inaceptable
que se manejen los errores como tokens. Por ejemplo:

    $ gisela errores.gsl
    Error: caracter inesperado "ñ" en línea 5, columna 4.
    ...
    
### Herramientas a utilizar

Para realizar el proyecto debe utilizar uno de los tres lenguajes de programación listados
a continuación y la herramienta generadora correspondiente.
El lenguaje que elija ahora será el que deberá usar para todas las entregas. *No* podrá
cambiarlo después.

#### C

* Compilador *gcc* 4.4.5

* Generador de analizadores lexicográficos *Flex* 2.5.37

#### Haskell

* Compilador *ghc* 6.12.1

* Generador de analizadores lexicográficos *Alex* 2.3.3

* Sólo puede utilizar Haskell si ya domina el uso de Monads.

#### Python

* Python 2.6.6

* Generador de analizadores lexicográficos y sintácticos *PLY* 3.3.3. Note que para esta entrega
  solo le interesa utilizar la parte *lex* de PLY, puede ignorar por ahora todo lo relacionado
  con yacc.

### Detalles de entrega

* *Fecha tope de entrega*: 5 de Octubre de 2012 (Viernes de Semana 3) hasta las 11:59:59 pm VET.

* Valor: 5%.

* Debe enviar su entrega adjunta a un correo electrónico a su preparador asignado.
  Podrá encontrar sus correos en la página oficial.
  
* Incluya un Makefile si va a utilizar C o Haskell. Si su entrega no compila no será corregido.

* Su ejecutable debe llamarse *gisela*.

* Respete las reglas de juego expuestas en la página oficial del curso.