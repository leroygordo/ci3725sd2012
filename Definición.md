# Gisela

Gisela es un lenguaje imperativo inspirado en GCL [1], con algunos elementos
adicionales apropiados para los conceptos que deben aprenderse en este
curso.

### Identificadores

Un identificador de Gisela permite denotar una constante, una variable
o un procedimiento, pero no más de una a la vez. Se considera
identificador cualquier secuencia de caracteres que comience por una
letra y luego continúe con letras y dígitos. Los identificadores
son sensibles a mayúsculas y minúsculas.

### Tipos de datos

Gisela es capaz de operar con tres tipos de datos

*  Caracteres (char), correspondientes a las primeras 127 posiciones ASCII.
   En el texto de los programas, se escriben literales entre
   comillas simples ('a'), comillas dobles ("a") o usando la forma \_a
  (underscore y el caracter) .

*  Valores de verdad (bool) true y false. 
   En el texto de los programas se escriben literalmente, pero pueden
   escribirse como combinación de mayúsculas y minúsculas, incluso
   parcialmente, i.e. t, Tr, trU y TRUE son exactamente lo mismo.

*  Enteros (int) de 32 bits.
   En el texto de los programas se escriben literalmente usando
   dígitos decimales, precedidos opcionalmente por el signo positivo
   o negativo.

Gisela tiene tipos fuertes, por lo que se considera un error construir
expresiones que involucren componentes de diferentes tipos de datos --
Gisela no contempla la conversión automática entre tipos de datos.

Pueden construirse expresiones o definirse variables con cualquiera de los
tres tipos de datos.

Todas las variables de Gisela deben ser declaradas antes de poder ser
utilizada. Puede haber declaraciones de variables globales en *cualquier*
punto del programa, siempre que esté *fuera* del bloque principal -- las
declaraciones globales aplican a *todo* el programa independientemente de
la posición en la cual aparezcan. Las declaraciones son de la forma

*tipo id0, ..., idN;*

donde tipo es bool, char o int, mientra que id0 hasta idN son
identificadores válidos en Gisela empleados para denotar las variables.
Los nombres de variables globales no pueden repetirse y tampoco ser
utilizados para denotar procedimientos.

Las variables de Gisela tienen inicialización automática por omisión: si
el programador no hace ninguna asignación explícita, las variables deben
elaborarse con:

*  !, para variables char.
*  false, para variables bool.
*  0, para variables int.

#### Operaciones con caracteres

El lenguaje provee las primitivas

*  chr :: int -> char
*  ord :: char -> int
*  isupper :: char -> bool
*  isalpha :: char -> bool
*  isdigit :: char -> bool
*  isspace :: char -> bool

#### Operaciones con booleanos

Pueden construirse expresiones booleanas cuya evaluación es
por corto-circuito con el siguiente orden de precedencia:

*  xor :: bool -> bool -> bool
*  and :: bool -> bool -> bool
*  or  :: bool -> bool -> bool
*  not :: bool -> bool -> bool

Los operadores conjunción y disyunción asocian hacia la izquierda,
mientras que el operador de negación asocia hacia la derecha. El
operador de disyunción exclusiva *no* es asociativo.

#### Operaciones con enteros

Gisela soporta operaciones de aritmética entera con el siguiente
orden de precedencia:

*  \** :: int -> int -> int   (a ** b, b-ésima potencia de a)
*  div, mod :: int -> int -> int   (cociente y módulo de división entera)
*  \*  :: int -> int -> int   (producto)
*  +, - :: int -> int -> int   (suma y resta)

Los operadores suma, resta y producto asocian hacia la izquierda,
mientras que los operadores cociente, módulo y potencia asocian hacia
la derecha.

El interpretador debe verificar a tiempo de ejecución las condiciones
de división por cero y desbordamiento.

Los valores numéricos pueden ser comparados usando

*  >, >=, <, <=, ==, != :: int -> int -> bool
*  >, >=, <, <=, ==, != :: char -> char -> bool

Estas operaciones no son asociativas.

### Comandos

Gisela tiene una separación estricta entre expresiones e instrucciones.

#### Instrucciones simples

* skip -- no hacer nada y continuar a la siguiente instrucción en el
  flujo del programa.

* abort -- interrumpir la ejecución del programa.

* Asignación

  v0,v1,v2,...,vn &nbsp; := &nbsp; e0,e1,e2,...,en

  donde las v son variables del programa y las e son expresiones del
  mismo tipo según la variable correspondiente. Todas las expresiones
  son evaluadas simultáneamente antes de asignar sus valores a las
  variables correspondientes.

* Entrada y Salida

  Para la entrada de datos, se provee la instrucción

  read msg v

  que emite en pantalla el mensaje 'msg' y espera a que el usuario
  suministre un valor del tipo adecuado para la variable v. El
  interpretador debe verificar a tiempo de ejecución que el valor
  suministrado tenga sentido según el tipo de la variable v.
  
  Para la salida de datos, se provee la instrucción

  print msg e

  que emite en pantalla el mensaje 'msg' y luego el valor de la
  expresión e.

  En ambas instrucciones el mensaje 'msg' corresponde a una cadena de
  caracteres encerrada entre comillas dobles o sencillas: si comienza
  con dobles, termina con dobles; si comienza con sencillas, termina
  con sencillas. En ambas instrucciones, la presencia de 'msg' es
  *opcional*.

* name ( e1, e2, ..., en ) -- Invocar un procedimiento.

  Esta instrucción permite invocar al procedimiento de nombre name.
  A tiempo de ejecución, se evaluarán las expresiones correspondientes
  a los parámetros actuales, de izquierda a derecha, y se harán
  corresponder con los parámetros formales del procedimiento.
  
  Inmediatamente se pasa a ejecutar el cuerpo del procedimiento, hasta
  que se encuentre una instrucción return o se alcance la última
  instrucción del procedimiento. En cualquier caso, la ejecución
  regresará a la instrucción siguiente para continuar.
 
  Gisela permite tener parámetros por valor o por referencia, por lo
  tanto *antes* de comenzar la ejecución, el interpretador debe
  verificar que para los parámetros por referencia el argumento sea
  una variable del tipo adecuado, en la cual poder operar.

* return -- Retornar de un procedimiento.

  Esta instrucción solamente tiene sentido dentro del cuerpo de un
  procedimiento, y su efecto es regresar al punto del program desde
  el cual fue invocado más recientemente el procedimiento.

#### Comandos con guardia

Un comando con guardia, es una instrucción de la forma

    G -> S

donde G es una expresión booleana (la "guardia") y S es una instrucción
simple. El caso extremo

    true -> S

debe poder escribirse directamente como

    S

La semántica de una instrucción con guardia requiere evaluar la expresión
booleana G, y si el resultado es true, ejecutar la instrucción S.

#### Secuenciación

Gisela emplea al punto y coma como *separador* de instrucciones simples.

#### Bloques

Gisela permite agrupar varias instrucciones en un bloque

go S0 <br>
; &nbsp;&nbsp;&nbsp; S1 <br>
; &nbsp;&nbsp;&nbsp;  S2 <br>
og

Esto permite que en cualquier lugar donde se requiera una instrucción
simple pueda escribirse un bloque. 

#### Selector

Gisela provee una instrucción condicional de selección (if) que se
construye como una lista de comandos con guardia

if G0 -> S0 <br>
| &nbsp; G1 -> S1 <br>
   ... <br>
| &nbsp; Gn -> Sn <br>
fi

A tiempo de ejecución se evalúan las guardias Gi en orden desde G0
hasta GN. Tan pronto como alguna se haga cierta, se ejecuta la instrucción
Si asociada. Si ninguna de las guardias se hace cierta, el programa
interrumpirá su ejecución.

Note que las Si pueden ser instrucciones simples o bloques.

#### Repetición

Gisela provee una instrucción de repetición no acotada (do) que se
construye como una lista de comandos con guardia

do&nbsp; G0 -> S0 <br>
| &nbsp;&nbsp;&nbsp;&nbsp; G1 -> S1 <br>
... <br>
| &nbsp;&nbsp;&nbsp;&nbsp; Gn -> Sn <br>
od

A tiempo de ejecución se evalúan las guardias Gi en orden desde G0
hasta GN. Tan pronto alguna se haga cierta, se ejecute la instrucción
Si asociada y se repite el proceso. Si ninguna de las guardias se hace
cierta, el programa continuará con la instrucción inmediatamente
siguiente al bloque do.

Note que las Si pueden ser instrucciones simples o bloques.

#### Programa principal

El programa principal Gisela es un bloque con nombre

let's
  go &nbsp;S0 <br>
  ; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; S1 <br>
  ... <br>
  ; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Sn <br>
  og 

sólo puede (y debe) haber un bloque así, que puede aparecer en *cualquier*
parte del texto del programa.

#### Procedimientos

Gisela permite definir procedimientos de la forma

proc name ( arg0, arg1, ..., argN ) <br>
&nbsp;&nbsp;&nbsp;  D <br>
&nbsp;&nbsp;&nbsp;  S0

En esta definición, name corresponde al identificador que denota al
procedimiento, que debe ser único en todo el texto del programa.
La lista de parámetros formales, que puede estar vacía, define los
nombres, tipos y método de pasaje de parámetros, pudiendo ser

*  tipo id -- pasaje por valor
*  var tipo id -- pasaje por referencia


Justo antes del cuerpo del procedimiento, puede agregarse una o más
declaraciones para variables *locales* al procedimiento. Aplican las
mismas reglas de sintaxis que para las variables globales, pero en
considerando que:

*  Una variable local *puede* tener el mismo nombre que una variable
   global, y en ese caso, la variable global queda fuera de alcance
   mientras se ejecuta en el cuerpo del procedimiento.

*  Una variable local *no puede* tener el mismo nombre que un
   argumento formal, pues los parámetros formales se consideran
   variables locales al procedimiento.

El cuerpo del procedimiento puede ser una instrucción simple, aunque
típicamente será una instrucción de bloque (if, do o go).

Los procedimientos pueden ser recursivos directa o indirectamente.

### Espacios en blanco y comentarios

Gisela ignora los espacios en blanco que estén fuera de las cadenas
de mensajes o fuera de las comillas que definen un caracter, de manera
que el programador tiene libertad de usarlos para indentar y organizar
su código de la manera más eficiente para su comprensión.

Además, se permite incluir comentarios en cualquier parte del texto
del programa. Al encontrar la secuencia //, el resto de los caracteres
hasta el final de la línea se consideran comentarios que serán ignorados
por el interpretador.

### Referencia

[1] [http://en.wikipedia.org/wiki/Guarded\_Command_Language](http://en.wikipedia.org/wiki/Guarded\_Command_Language)
