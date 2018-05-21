# Introducción a la programación

Un programa es un conjunto de instrucciones que el ordenador puede interpretar y ejecutar para realizar una tarea específica. Se codifica usando algún lenguaje de programación y con la ayuda de un compilador se traduce a lenguaje máquina. A esta traducción se le conoce como binario o simplemente ejecutable.

> De acuerdo a Bohm y Jacopini un programa puede ser escrito usando únicamente 3 estructuras (Secuencial, Selectiva y Repetitiva). Además de poseer solo un punto de entrada y uno de salida. Sin bucles infinitos y con al menos un camino hasta el final. A esto se le conoce como el teorema de "Bohm y Jacopini".

Un lenguaje de programación es un conjunto de símbolos ordenados por reglas sintácticas y semánticas; que componen un lenguaje formal entendible para el ser humano. Mientras más cercano al lenguaje natural se dice que es de mayor nivel. 

De acuerdo a esta clasificación tenemos
- **Lenguajes de alto nivel**: PHP, VB, C#, Java
- **Lenguaje de medio nivel**: Pascal, C, C++
- **Lenguaje de bajo nivel**: Binario o lenguaje maquina (10101001), Ensamblador (MOV 1AX,4CH)


Utilizando un lenguaje de programación podemos escribir un código que será la fuente de nuestro programa, mejor conocido como **código fuente**.

El compilador es el encargado de traducir el código fuente pasando por un código objeto o directamente a lenguaje máquina. Para realizar esta tarea se encarga de enlazar librerías y analizar el código fuente para asegurarse de que cumpla con las reglas del lenguaje de programación.
- **Análisis Léxico**: Valida que el conjunto de símbolos o instrucciones correspondan al lenguaje.
- **Análisis Sintáctico**: Valida las reglas para combinar de forma correcta las instrucciones.
- **Análisis Semántico**: Valida el significado de cada línea del código fuente.

Interprete
Existen lenguajes de programación que no son compilados sino leídos e interpretados directamente desde el código fuente. Por lo que no generan un ejecutable. Esto resta velocidad en cuanto a ejecución, sin embargo es útil para ser ejecutado en diferentes plataformas como es el caso de Python.

Una clasificación común para su estudio 
- **Programación estructurada**: Esta incluye el uso de diseño descendente (top-down), la división de problemas complejos en varios simples y el uso de estructuras básicas (secuenciales, selectivas y repetitivas).
- **Programación modular**: Consta de varias secciones que interactúan a través de llamadas a procedimientos o funciones. Su mayor ventaja es la reutilización de código y la facilidad para depurar el mismo. Ya que se puede modificar un módulo sin afectar a otros.
- **Programación orientada a objetos (POO)**: Consiste en la utilización de estructuras de código, las cuales poseen propiedades y atributos; por lo cual reciben el nombre de objetos.

El objetivo original de la programación consiste en la automatización de tareas, siendo la tarea del programador la abstracción, resolución y representación de una solución en un lenguaje de programación. Es de este proceso que surge la algoritmia, que es la ciencia y arte de solucionar problemas.

La algoritmia consiste en la resolución de problemas por métodos no triviales, es decir resolver un problema de la manera más eficiente posible. Ya sea usando el menor número de recursos o el menor tiempo computacional.

## Glosario

**Instrucción**: Conjunto de datos insertados en una secuencia estructurada que el procesador interpreta y ejecuta.
**Programa**: Conjunto de instrucciones, escritas para realizar una tarea específica.
**Lenguaje de programación**: Conjunto de reglas gramaticales que permiten formar un programa.
**Código fuente**: Instrucciones escritas en un lenguaje de programación y por lo tanto legible por un humano.
**Código objeto**: Contiene las instrucciones de alto nivel traducidas al lenguaje de maquina (por lo regular la extensión en .obj).

