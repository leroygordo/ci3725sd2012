**Consulta 1:** 

a) La declaracion de los tipos de datos se hace con las palabras 'bool', 'char', 'int'. Esto significa que se debe hacer un token "TipoDato"??

> a) Son palabras reservadas, así que haz un token para cada tipo.

b) Los procedimientos: "read", "print", "chr" , "ord", "isupper", "isalpha", "isdigit" y "isspace" se modelan con el "Token identificador" o cada uno es un token por separado. Por ejemplo los operadores booleanos y aritmeticos: "xor", ..., "not", "+", "mod", ..., "div"; los modelamos con un token para cada uno.

> b) Todas esas palabras representan instrucciones u operadores del lenguaje, así que son palabras reservadas y debes hacer un token para cada una, tal cual como hiciste con los operadores booleanos y aritméticos.


c) Segun el enunciado el bloque principal debe empezar con "les' t go ". Nosotros creamos un token "Ini_Bloque" para "go", lo que no sabemos es si se debe crear uno para 
"lest's go" completo y uno para "go" o si crear uno para "let's" y otro para "go".

> c) Está bien que hagas un token para 'let's' y otro para 'go'.

d) Las palabras "var" y "proc" se usan cuando se crea un procedimiento, tenemos la duda se si crear un token para cada una.

> d) Si, como son palabras reservadas debes hacer un token para cada una.

e)Se especifica que los enteros en gisela tienen 32 bits. Si se coloca en el programa algun entero que supere este tamaño, el lexer debe reportarlo como un error, o colocarle el valor 0?

> e) Repórtalo como error.

f) De acuerdo al enunciado de la entrega 1, se debe crear un token para las "cadenas de caracteres". Estas cadenas son un nuevo tipo de datos String, o solo son cadenas que seran pasadas literales a los procedimientos de gisela "read" y "print". Es decir que un programa en gisela nunca podra tener  " x:= "hola mundo", pues no  existe ese tipo de datos cadena.

> f) Son las cadenas que se pasan a las instrucciones read y print, no son un tipo de dato nuevo.

---

**Consulta 2:**

Gisela permite definir procedimientos de la forma

proc name ( arg0, arg1, ..., argN ) 
    D 
    S0

¿Qué significa "D" y "So" y además como identificamos si un procedimiento se terminó?? con el return???

> En la definición de procedimientos, D es para Declaración de variables. Al comienzo de un procedimiento puedes definir una o más variables locales al procedimiento. S0 es para Statement inicial. El cuerpo de un procedimiento consiste de una instrucción de Gisela.

> Un procedimiento termina cuando se encuentra con una instrucción return o termina de ejecutar su última instrucción.

Otra duda, se que existe un único programa principal que se identifica así:

let's go  S0 
;               S1 
... 
;               Sn 
og

pero donde va la definición de los procedimiento, adentro o afuera del programa principal??

> Los procedimientos y variables globales van fuera del bloque let's go.


---

**Consulta 3:**


1-"Se considera identificador cualquier secuencia de caracteres que comience por una letra Y luego continúe con letras Y dígitos", ¿es obligatorio el uso de las letras y los dígitos o es opcional ?.

> 1- Piensa los identificadores como las variables en cualquier otro lenguaje, la única condicion es que empiece por una letra, mayúscula o minúscula, después de eso puede o no haber una letra o un número.
>
 Ej: Válidos= X, y, X2, x2go

<br>

> No me exprese bien en la pregunta 1, que puede o no haber una o más letras o números, incluso mezclados.
   

2- En el uso de los bloques(go, og) y para los ciclos (do, od),  ¿debo colocar un token por cada palabra reservada? es decir TkDo , TkOd, TkGo  y TkOg.

>   2- Sí, debes usar un token por cada palabra reservada.

---

**Consulta 4:**

a)
cita: 

Gisela es capaz de operar con tres tipos de datos:
Caracteres (char), correspondientes a las primeras 127 posiciones ASCII. En el texto de los programas, se escriben literales entre comillas simples ('a'), comillas dobles ("a") o usando la forma _a (underscore y el caracter) .

Cuando dicen literales se refieren a caracteres simples? ('t', "y", _u, etc..)

> Sí, un caracter.

b)
cita:

Valores de verdad (bool) true y false. En el texto de los programas se escriben literalmente, pero pueden escribirse como combinación de mayúsculas y minúsculas, incluso parcialmente, i.e. t, Tr, trU y TRUE son exactamente lo mismo.

Es decir que para el lexer tr, tR, tRu..y toda cadena de caracteres que podria completar la palabra true...son tkTrue?

> Así es. Recomiendo no *cablear* esto y pensar bien en la expresión regular para  este token.

---

**Consulta 5:**

En el enunciado del proyecto mencionan que entre los tokens relevantes del lenguaje se encuentran:
Los caracteres literales. Debe ser un único token cuyo contenido sea el caracter.

Las cadenas de caracteres encerradas entre comillas. Debe ser un único token cuyo contenido sea la cadena leída.



Cuál es la diferencia entre estos dos??

> Un caracter corresponde a un tipo de datos. La cadena de caracteres no corresponde a algun tipo de datos, es la entrada para las intrucciones *read* y *print*.

---

**Consulta 6:**

a) Si tengo algo como read "a" v. El lexer me reconoce "a" como un caracter y no como una cadena. Esto esta bien asi o debe un token cadena.

> a) Está bien que lo reconozca así, a nivel del lexer no vale la pena el trabajo para diferenciarlos.

b) Las cadenas pueden tener caracteres que no sean los 127 primeros de la tabla ASCII?. Por cierto como solo se usan los 127 primeros caracteres ASCII entonces no se puede tener caracteres vacios ni cadenas vacias. 

> b) No puedes tener caracteres además de los 127 primeros (en realidad esto es esencialmente todos los caracteres ASCII excepto DEL, así que no debe ser un problema), y ciertamente el lenguaje no contempla caracteres o cadenas vacías.

c) Por ultimo si tengo algo como a+5 me reconoce el token de "a", el token "+" y el token "5".  En el caso en el que tengo a+-5 me reconoce los tokens "a", "+", "-" y "5" esto esta bien asi?

> c) Si está bien. De hecho te va a convenir que el símbolo - sea siempre un token aparte porque a nivel del lexer no puedes diferenciar cuando se usa para indicar un número negativo y cuando se usa como operador.
