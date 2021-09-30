+++
author = "Joan Tolos"
categories = ["code"]
date = "2022-06-15"
description = "A high level approximation of what happens at CPU level when running software"
featured = "pic01.png"
featuredalt = ""
featuredpath = "/img/cpu/"
linktitle = ""
title = "How computers process a program"
type = "post"
+++

Your code is executed by a computer somewhere... your own, a remote server, on the cloud, whatever... This computer is going to have a CPU, a central process unit that will deal with the instructions of your code one by one.

Let's explore the basic components of a CPU on a high level so we can try to figure out how it deals with the code.

# The arithmetic logic unit

The final goal of a microprocessor is the **computation.** Compute means manipulate numbers in a structured way and with a purpose, for example, an addition. That is a computation.

This is done by the Arithmetic Logic Unit (ALU):

> An arithmetic logic unit (ALU) is a combinational digital circuit that performs arithmetic and bitwise operations on integer binary numbers.

This is a simple schematic that you would find anywhere describing an ALU:

{{< img-post path="/img/cpu/" file="alu.png" alt="ALU Schematic" type="center" >}}

This is the very central core of any computer, **everything** ends up using the ALU one way or the other. It performs arithmetic and logic operations:

- Arithmetic: Additions, increments...
- Logic: Binary gates like AND, OR, NOT...

All of this is encapsulated in a single chip. The first time this was delivered in a single chip was by Intel with the 74181 chip

{{< img-post path="/img/cpu/" file="74181.png" alt="Intel 74181 ALU chip" type="center" >}}

This is the complete schematic including all the logic gates needed, it's a level down of abstraction respect the generalisation above. Just as a curiosity, here it is the whole detail:

{{< img-post path="/img/cpu/" file="74181aluschematic.png" alt="Intel 74181 ALU schematic" type="center" >}}

This circuit was a revolution on it's time and it is a classic today. Is still used to teach digital design. By the way, it couldn't multiply or divide.

# ALU overflow!

This is a very low level but imagine you have 8 bits to work with. The ALU will perform the arithmetic operation of "increment" which is _add one to the current number_. Imagine you are storing the level of your game and every time the user finishes a level, the ALU increments the level number. Now imagine that you have 8 bits to store this level number and the user is capable to go until level 256... ALU overflow of course. Now imagine that game is PACMAM... because it is.

If you have 8 bits to store the level number, you can go from 0 to 255 because:

{{< img-post path="/img/cpu/" file="8bits.png" alt="8 bits explanation" type="center" >}}

Of course, when the ALU tries to give the 256 as an answer, it overflows. This is just what happens to the PACMAN game if you are brave enough to reach the level 256:

{{< img-post path="/img/cpu/" file="pacmanGlitch.png" alt="8 bits explanation" type="center" >}}

Just remember: The ALU is the basic element of a CPU. It performs arithmetic and logic operations.

# Registers and RAM

Registros y RAM
Vale, ya tenemos nuestra unidad aritmetico logica con capacidad para hacer estas operaciones
Queremos hacer algo con ellas no? Encadenarlas a otras o guardar sus resultados
RAM -> Random Access Memory / Consistent memory
Se trata de diseñar un circuito que nos permita almacenar un bit... esto se hace con una puerta AND o OR cuya salida se retroalimenta a una de sus dos entradas. Este circuito logico se llama AND-OR-LATCH, con un nivel de abstraccion mas alto, se consigue el circuito que se llama "Gated latch", que funciona: tienes 2 inputs, el bit que quieres guardar y un bit que habilitara o no el guardado. Habilitas el guardado, metes un uno, desabilitas el guardado, y siempre te devolvera un uno... has almacenado un 1 en memoria!
Un grupo de latches se llama un register, un registro de memoria
Hay varias maneras de acumular latches para almecenar mas de un bit, por ejemplo, una matriz, Latch Matrix asi podemos almacenar 8 bits, 16 bits, 256 bits...
Esto nos llevaria al siguiente nivel de abstraccion que es un multiplexor... (definicion?)
Que es a su vez una matriz de esas matrices que hemos visto anteriormente...
Un nuevo nivel de abstraccion y a todo este conjunto se le llama: RAM!
Random access memory... o memoria a corto plazo (que he comido este mediodia vs recordar las vacaiones cuando tenias 15 años)
Este ejemplo seria SRAM, static... pero hay otros... DRAM. Flash Memory o NVRAM... lo que cambia es el circuito basico que es el latch.
Es como el juego de las muñecas rusas

CPU (Central processing unit)
ALU -> Ejecuta calculos con numeros binarios

RAM -> Capacidad de guardar estos calculos en memoria, persistidos, ni que sea temporalmente

Con esto ya podemos introducir el concepto de CPU -> Central Process Unit
Su trabajo es ejecutar programas, o mejor dicho, ejecutar instrucciones de programas
CPU necesita comunicarse con la memoria RAM
Necesita una serie de registros que dependeran del tipo de CPU y esos registros van a contener los datos necesarios para ejecutar una instruccion. Pero sea cual sea la arquitectura del procesador, hay dos registros que siempre existen:
- Instruction addres register
- Instruction register

A partir de aqui empieza el ciclo del microprocesador: FETCH-DECODE-EXECUTE

Nuestro procesador tiene asociada una tabla de instrucciones de todas las cosas que puede hacer (load, store, write...)

FETCH:
address register es 0
vamos a la ram a la posicion 0
colocamos su contenido en el instruction register
Ya hemos hecho el fetch, hemos ido a buscar nuestra primera instruccion en la memoria

DECODE:
Que es esa instruccion para poder ejecutarla y no descartarla
La instruccion se va a componer de dos partes, el codigo de operacion (load, store, write, add, etc) y la direccion de memoria de los datos a la que se tiene que aplicar esa operacion
Ya sabemos que operacion es, y que datos tiene implicados, ya hemos hecho el decode

EXECUTE:
Si por ejemplo en nuestro decode tenemos en los primeros 4 bits un LOAD y los ultimos 4 bits un 3. Para ejecutar esta instruccion usaremos otro de los registros disponibles para cargar ese tres.
Voila! Ya hemos cargado el 3, por lo que hemos terminado la instruccion que era precisamente, cargar el 3
Ahora lo que toca es incrementar el registro de instruccion address para volver a empezar con otro ciclo FETCH-DECODE-EXECUTE

Las diferentes opciones que te da un procesador para trabajar con las instrucciones estas embedidas en la arquitectura del propio procesador. Por eso, un procesador Intel es diferente de un procesador AMD. Por esto mismo, la manera que tiene de ejecutar las instrucciones sera diferente.
Algunos son mas eficientes en un sentido, otros en otro.

Por ejemplo, queremos hacer una suma:
Cargar numero a
Cargar numero b
Sumar numero a y numero b
Guardar el resultado en memoria
(esto lo podrias hacer en ensamblador por ejemplo)

4 instrucciones, cada una de ellas va a tener su ciclo completo de FETCH-DECODE-EXECUTE

La velocidad a la que la CPU puede hacer cada una de esas pequeñas operaciones del ciclo se llama la velocidad de reloj de la CPU, los famosos herzios de un microprocesador.
Intel The Core i7 tiene una velocidad de reloj de 2.9GHz Hertz es una unidad de frecuencia
1 herz es un ciclo por segundo
2,9 billones de ciclos por segundo
Yo he tardado unos 5 minutos en explicar un solo ciclo, soy el peor procesador de la historia


### References:
* _Photo by {{< url-link "Niek Doup" "https://unsplash.com/@niekdoup?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText" >}} on {{< url-link "Unsplash" "https://unsplash.com/s/photos/cpu?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText" >}}_
* _{{< url-link "How CPU executes a program" "https://www.youtube.com/watch?v=XM4lGflQFvA" >}}_
* _{{< url-link "How computers calculate " "https://youtu.be/1I5ZMmrOfnA" >}}_
* _{{< url-link "Registers and RAM" "https://youtu.be/fpnE6UAfbtU" >}}_
* _{{< url-link "The Central Processing Unit" "https://youtu.be/FZGugFqdr60" >}}_
* _{{< url-link "Instructions and Programs" "https://youtu.be/zltgXvg6r3k" >}}_
* _{{< url-link "Wikipedia: 74181" "https://en.wikipedia.org/wiki/74181" >}}_
