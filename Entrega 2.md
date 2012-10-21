Universidad Simón Bolívar<br>
Departamento de Computación y Tecnología de la Información<br>
CI3725 - Traductores e Interpretadores<br>
Septiembre - Diciembre 2012

# Entrega 2 (5%)
## Gramática Inicial y TAD Tabla de Símbolos

En esta entrega se debe dar una implementación inicial de las reglas que definen la gramática para el lenguaje de programación *Gisela*. Además, debe proveer su implementación del tipo para la tabla de símbolos.

Su gramática y su tabla de símbolos deben ser lo suficientemente completos tales que se enfoquen en cada detalle de la [definición](definicion.html) de Gisela, por ejemplo, anidamiento de bloques, llamadas a funciones.

Usted debe implementar, en adición a la definición de las reglas de su gramática,  un módulo correspondiente a la tabla de símbolos **SymTable** el cual debe incluir como mínimo las siguientes funciones:

* *SymTable.new()*: o algún método de nombre análogo que permita crear una tabla de símbolos vacía.
* *SymTable.insert(...)*: inserta un elemento en la tabla de símbolos.
* *SymTable.delete(...)*: borra un elemento de la tabla de símbolos.
* *SymTable.update(...)*: actualiza la información de un elemento en la tabla de símbolos.
* *SymTable.isMember(...)*: preguntar la existencia de un elemento en la tabla de símbolos.
* *SymTable.find(...)*: retorna la información de un elemento en la tabla de símbolos, asumiendo que el mismo existe.

**Nota:** Los parámetros de cada método se dejan a su preferencia y conveniencia.

El módulo **SymTable** debe estar en un archivo aparte llamado *SymTable.hs*, *SymTable.c* o *SymTable.py*, según sea el caso del lenguaje escogido.

Su programa principal deberá llamarse *gisela* y recibirá como argumento el nombre del archivo a analizar. La ejecución del mismo mostrará una salida **limpia** (sin nada), únicamente mostrará en pantalla los errores sintácticos o lexicográficos conseguidos durante el análisis, pero no ambos a la vez. Por ejemplo:

    $ gisela con_errores_lexicograficos.gsl
    Error: caracter inesperado "ñ" en línea 5, columna 4.
    ...

o

    $ gisela con_errores_sintacticos.gsl
    Error de sintaxis en línea 5, columna 4.
    ...

Para este último el número de *línea* es relativo al archivo y el número de *columna* es relativo a los tokens. Válgase de los beneficios de la herramienta escogida.
    
### Herramientas a utilizar

Usted puede apoyar su TAD tabla de símbolos usando alguna librería de código abierto y notificar al preparador correspondiente el nombre y la versión exacta de la misma. 

**Recuerde:** Debe continuar trabajando con el lenguaje de programación escogido desde la primera entrega. 

Sólo se permitirá el uso de las siguientes herramientas:

#### C
* Compilador *gcc* 4.4.5
* Generador de analizadores sintácticos *bison* 2.6.2

#### Haskell
* Compilador *ghc* 6.12.1
* Generador de analizadores sintácticos *happy* 1.18.4

#### Python
* Python 2.6.6
* Generador de analizadores lexicográficos y sintácticos *PLY* 3.3.3.

### Detalles de entrega

* *Fecha tope de entrega*: 22 de Octubre de 2012 (Lunes de Semana 6) hasta las 11:59:59 pm VET.

* Valor: 5%.

* Debe enviar su entrega adjunta a un correo electrónico a su preparador asignado.
  Podrá encontrar sus correos en la página oficial.
  
* Incluya un Makefile si va a utilizar C o Haskell. 

* Si su entrega no compila no será corregido.

* Respete las reglas de juego expuestas en la página oficial del curso.