+++
author = "Joan Tolos"
categories = ["code"]
date = "2022-06-15"
description = "A simple problem solved for two different complexity times"
featured = "pic01.png"
featuredalt = ""
featuredpath = "/img/bigO2/"
linktitle = ""
title = "Big O notation example"
type = "post"
+++

ALU
El objetivo final del micropocesador es la computacion: manipular numeros de manera estructurada y con un proposito... por ejemplo, una suma
Esto lo hace la ALU -> Arithmetic Logic Unit
Es la parte centra de cualquier ordenador, TODO termina usando la ALU
Arithmetic... operaciones aritmeticas como sumar, incrementar etc

Logic... puertas logicas binarias, AND, OR, NOT, XOR, u otras funciones como sumar o restar, incluir o excluir según sus propiedades lógicas.
Todo esto esta encapsulado en un solo chip, la primera vez esto lo hizo Intel, y fue una revolucion. No podia multiplicar o dividir
	Respecto a la unidad aritmetica - Si lo que te llevas supera el numero de bits que puedes almacenar, se producte un overflow. Pacman level 256 overflow. 2^8 = 256 -> 255 niveles
La ALU es el elemento basico de una CPU, de un microprocesador

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


TODO JUNTO
Lenguaje ensamblador
...
El ciclo del microprocesador, fetch - decode - execute


### References:
* _Photo by {{< url-link "Niek Doup" "https://unsplash.com/@niekdoup?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText" >}} on {{< url-link "Unsplash" "https://unsplash.com/s/photos/cpu?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText" >}}_
* _{{< url-link "How CPU executes a program" "https://www.youtube.com/watch?v=XM4lGflQFvA" >}}_
* _{{< url-link "How computers calculate - ALU" "https://youtu.be/1I5ZMmrOfnA" >}}_
* _{{< url-link "Registers and RAM" "https://youtu.be/fpnE6UAfbtU" >}}_
* _{{< url-link "The Central Processing Unit" "https://youtu.be/FZGugFqdr60" >}}_
* _{{< url-link "Instructions and Programs" "https://youtu.be/zltgXvg6r3k" >}}_
