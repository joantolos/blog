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

Now that we have this unit with the capability to perform those operations, we want to be able to do something with them. Chain them together, store the outputs... This is where the RAM memory becomes relevant (Random access memory)

We need to design a circuit that allows us to store one bit. You can do that with an AND, OR logic gate which output retro feeds into one of its inputs.

{{< img-post path="/img/cpu/" file="basicLatch.png" alt="Basic Latch" type="center" >}}

This circuit will "stuck" a bit in a way that no matter what the input is, it will always returns that bit. The actual circuit has a reset mechanism but it is easier to understand with this simplified version. The sophisticated version is called a _gated latch_ and works like this:

- Enable the storage
- Store the bit (a one for example)
- Disable the storage
- Will always return the one until enabling storage again

Congratulations! You have successfully stored a one in memory.

A group of latches is named a memory register. There are several different ways to accumulate latches to store more than one bit, for example a matrix, a latch matrix so we can store 8 bits, 16 bits, 256 bits...

Adding a new level of abstraction with multiplexors and the new block is what we call RAM memory.

> Random-access memory can be read and changed in any order, typically used to store working data and machine code. A random-access memory device allows data items to be read or written in almost the same amount of time irrespective of the physical location of data inside the memory.

The example with the latch is called SRAM (S from static), but there are others... DRAM, Flash Memory, NVRAM
Este ejemplo seria SRAM, static... pero hay otros... DRAM. Flash Memory o NVRAM... the idea is the same but the basic circuit (the latch), changes.

# Central process Unit

With these two elements (ALU and RAM) we can introduce the concept of CPU (Central Process Unit). Its work is execute programas, or better said, execute program instructions, one by one.

The CPU needs communication with the RAM memory and a series of registers. The definition and design of those registers will depend on the type of CPU and its architecture and they will be used to store the data needed in order to execute an instruction. No matter what architecture, there are two registers that need to be there:

- Instruction address register: Starts at zero, contains the memory address to the instruction to execute.
- Instruction register: Contains the instruction to execute.

Also, each CPU has a table of instructions of all the operations it can made (load, store, write...). For example:

{{< img-post path="/img/cpu/" file="instructionsTable.png" alt="Basic Latch" type="center" >}}

Now the **cicle** of the CPU starts. The cicle has three phases: FETCH - DECODE - EXECUTE

## Fetch

The address register starts at zero, so we are fetching the content of the RAM memory at the zero position. We put the content of that position on the instruction register.

This is the fetch phase of the cicle, we have reached our first instruction from memory.

## Decode

On this phase, we are going to look at the instruction so we can execute it or discard it. The instruction is going to be composed by two parts:

- The operation code
- The memory address of the data associated

Using the instruction table, you can match the operation code with the proper operation and you can reach the data neede for this instruction. We have successfully decoded the instruction.

## Execute

Now it's time to execute the decoded instruction. For example, the first four bits of the instructions tells us that we have to perform a LOAD operation, and the other four bits is the representation for the number three. So... "load the number three". We use the proper free register on the cpu to load that number three. Now it's time to increment the instruction address register and start a new cicle again.

## Example

The different options that you have on the CPU to work with the instructions are embedded on the CPU itself, in its architecture. That is why an Intel CPU is different than an AMD one, the architecture is different. Some operations will be more efficient, some others, not so much. That will vary from architecture to architecture.

For example, we want to make a simple addition. This will be split into four instructions:

- Load number A
- Load number B
- Add
- Store the output

This four lines remind a lot to Assembly Language which is a **low-level** programming language in which there is a very strong correspondence between the instructions in the language and the architecture's machine code instructions. Makes sense right?

Each one of this four instructions will have its own complete cicle of fetch, decode and execute.

## CPU clock

In order to finalise the CPU, it also needs a clock. The clock will define the speed it can perform each one of this cicle operations. It is measured on Hertz, a measure of frequency.

A 1 Hertz clock CPU means that it can perform a CPU cicle in one second. A Intel Core i7 with a clock speed of 2.9GHz which means it can perform 2,9 billions of cicles per second.

I have spend a least twenty minutes trying to explain just one cicle... that would probably makes me the worst CPU in history...

# Follow the yellow brick path of abstraction

It's a bit like the Russian dolls. If you look at one element by itself, it is not that complicated... but usually this element is part of a much more bigger element and if you try to understand the specifics it can be difficult. Then you add a new level of abstraction, and end up with a bigger doll that it is easy to understand.

{{< img-post path="/img/cpu/" file="russianDolls.png" alt="Basic Latch" type="center" >}}

Our day to day level of abstraction is so high that when we type an if statement, we don't think on all these terms. But we should have into account, that at the very end, the CPU will perform instruction by instruction of your if statement. Even more, we know for sure that the key operation that the CPU will do for each instruction will pass necessarily by the ALU, so your high level if statement can be reduced to a bunch of arithmetic and logic operations.

Now think of something really cool instead of an if statement, like a recursive method to calculate Fibonacci's series... All that work reduced to a bunch of simple arithmetic operations. Impressive, right?

Our beloved computers (and phones, watches...) are very good at performing very simple operations (like addition) very very fast. Just the opposite as us, humans, that we can perform very complex operations but we take our time. We also really suck at doing the same single task over and over again... Humans are good using creativity, thinking in high-level terms and machines are really good repeating simple things very fast. We are really made for each other.

That is why sometimes we struggle to solve certain problems with algorithms, because we humans think of them with a high level of abstraction, and we need to reduce them to operations that a machine can perform. If you design an algorithm that mimics the way a human will solve the problem it is probably a very poor algorithm. The key, the mind blowing, mind changing step, is always something that a human "wouldn't do" and that is usually the key of the algorithm.

### References:
* _Photo by {{< url-link "Niek Doup" "https://unsplash.com/@niekdoup?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText" >}} on {{< url-link "Unsplash" "https://unsplash.com/s/photos/cpu?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText" >}}_
* _{{< url-link "How CPU executes a program" "https://www.youtube.com/watch?v=XM4lGflQFvA" >}}_
* _{{< url-link "How computers calculate " "https://youtu.be/1I5ZMmrOfnA" >}}_
* _{{< url-link "Registers and RAM" "https://youtu.be/fpnE6UAfbtU" >}}_
* _{{< url-link "The Central Processing Unit" "https://youtu.be/FZGugFqdr60" >}}_
* _{{< url-link "Instructions and Programs" "https://youtu.be/zltgXvg6r3k" >}}_
* _{{< url-link "Wikipedia: 74181" "https://en.wikipedia.org/wiki/74181" >}}_
* _{{< url-link "Random access memory" "https://en.wikipedia.org/wiki/Random-access_memory" >}}_
