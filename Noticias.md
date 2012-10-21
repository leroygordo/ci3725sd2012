- Deben reportar todos los errores lexicográficos y el primer error sintáctico, en caso de que haya.

- Para simplificar la complejidad de la propuesta de su gramática para Gisela, hemos decidido que las instrucciones complejas (**do**,**if**,**go**) también pueden ser secuenciadas con **;**

---

- Publicada la gramática para [SuperQuery](SuperQuery.pdf).

- Los comandos con guardia se usan en las instrucciones **if** y **do** mas no como instrucciones simples.

- Las instrucciones complejas **if** y **do** están definidas sintácticamente como una lista de comandos con guardia los cuales están definidos como un expresión booleana y una instrucción simple o cualquier otra instrucción más compleja, es decir, **if**, **do** y **go**.

- Fuera del bloque principal y al comienzo de un código escrito en Gisela pueden  ir la declaración de variables globales y procedimientos con su cuerpo.

- Las variables globales no se pueden inicializar. En general, nótese que no puede usarse la instrucción asignación en una declaración de variables.

- El operador para secuenciación de instrucciones solo se aplica a las simples.
 Es decir, para un **do**, **if** o **go** no habrá un **";"** al finalizar la instrucción compuesta en caso de que haya una instrucción luego de ésta. 

- Los operadores unarios para caracteres pueden implementarse como funciones embebidas o como un operador prefijo, pero no ambas, escoja usted la implementación que más le convengan. Por ejemplo: Para calcular **chr**  de **3**:


         ...
         x := chr(3)
         ... 

 ó

         ...
         x: = chr 3
         ...



---------- 

- Disponible los casos de prueba para la [Entrega 1](entrega1.tar.gz).


**ATENCION:** Postergada la segunda entrega de su proyecto para el Lunes de la Semana 6. NO VIERNES.

- Se agrega el operador de enteros, menos unario (-), el cual recibe una expresión entera y retorna el valor negativo de la misma.
    

 \- :: int -> int

- La cadena de caracteres pueden estar encerradas entre comillas dobles o simples. Si la cadena está encerrada entre comillas dobles, entre los caracteres de la cadena no puede haber alguna comilla doble; el mismo caso aplica a las comillas simples.

- La cadena de caracteres no contienen saltos de líneas (\n).