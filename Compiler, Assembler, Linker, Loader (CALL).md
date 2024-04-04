# Compiler, Assembler, Linker, Loader (CALL)

## 1.Translation vs. Interpretation

- Interpreter
	- **Directly** execute the program in the source language
	- Use to interpret a *high level language* when we don't care about efficiency (easier,smaller but slower)
	- **Instruction Set Independence ** —— can run on any machine
- Translator/compiler
	- **Convert** the program from the source language into another language
	- Use to translate to *lower level language* when we need extra performance (run faster)
	- **High Security** —— could ''hide'' the source code

## 2.Compiler
- I/O
	- Input: higher level language code (e.g. foo.c foo.cpp)
	- Output: Assembly language code  (e.g. foo.s)
		>may contain *pseudo-instructions* which is not the true instruction to the machine

## 3.Assembler
- I/O
	- Input: Assembly language code  (e.g. foo.s)
	- Output: Object code (True Assembly),tables  (e.g. foo.o)
		- Replace *pseudo-Instructions*
		- Create machine language

### 3.1 Two Tables
- **Forward Reference problem**

  -  the label of branch instructions is below (after) it,which we don't know the address it is
- Deal with **(external) labels **and **references of data**
- **Symbol Table**

  - ''Items'' that may be *used by other files*
  	- Labels
  	- data

  - Keep tracking the labels, which fixes the FRP

- **Relocation Table**

  - “items” that will *need the address of later* (we don't know the address for now)
    - external labels
    - data referenced in data section

### 3.2 Object File Format

- object file header: size and position of the other pieces of the object file 

- text segment: the machine code 

- data segment: data in the source file (binary) 

- relocation table: identifies lines of code that need to be “handled” 

- symbol table: list of this file’s labels and data that can be referenced 

- debugging information 


## 4.Linker