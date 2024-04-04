#  Intro to Assembly Language

##  1.Assembly Overview

1. Assembly language

   - a low level  programming language,witch could only do the single part of the process

     > e.g. a=(b+c)-(d+e):
     >
     > `add t1,s1,s2`
     >
     > `add t2,s3,s4`
     >
     > `sub s0,t1,t2`

   - instructions
     - add,sub,read/write memories;
     - if condition or other complex instructions;

2. RISC-V

   - a reduced instruction set computing device,
     - contains the most simply instructions
     - run faster

## 2.Registers

1. Register
   - a fast storage hardware
2.  the number of registers
   - more registers->more variables but lower speed

3. Registers in RICS-V
   - 32 registers------x0-x31
     - holds programmer variables->s0-s11
     - holds temporary variables - t0-t6
   - the "Zero" register ---x0
     - hold '0' permanently
     - read only

## 3.Basic arithmetic instructions (op dst,src1,src2) 

1. add

   > c:  `a=b+c;`
   >
   > RISC V: `add s1,s2,s3`

2. sub

   > c:  `a=b-c;`
   >
   > RISC V: `sub s1,s2,s3`

## 4.Immediate instructions (opi dst,src1,imm) 

- add/sub

	> c:  `a=b+5(-5);`
	>
	> RISC V: `addi s1,s2,5(-5)`

## 5.Data Transfer Instructions (memop reg,off(bAddr))

1. Word instructions

   - lw sw

     > c:`array[10]=array[3]+b;`
     >
     > RISC-V:
     >
     > ​	`lw t0,12(s3)`
     >
     > ​	`add t0,s2,t0`
     >
     > ​	`sw t0,40(s3)`
     

2. sign extension

   - sign extend 
     - 0b11=0b1111
   - zero/one pad
     - Zero Pad: 0b 11 = 0b 0011
     - One Pad: 0b 11 = 0b 1111

3. Byte instructions

   - `lb(load byte) ` upper24 bits are *ignored*

   - `sb(store byte)` upper 24 bits are *sign-extended*
     
     > s0 = 0x00000180:
     >
     > `lb s1,1(s0)   # s1=0x00000001`
     >
     > `lb s2,0(s0)   # s2=0xFFFFFF80`
     >
     > `sb s2,2(s0)  #*(s0)=0x00800180`

4. Half-Word instructions
	- `lh reg, off(bAddr)`  upper 16 bits are *sign-extended*
	- `sh reg, off(bAddr)`  upper 16 bits are *ignored*

5. Unsigned Instructions
	- `lhu reg, off(bAddr)`“load half unsigned”
	- `lbu reg, off(bAddr)`“load byte unsigned”
	- wupper bits are zero extended

## 6.Control Flow Instructions

 1. Branches and Jump

    - **Branch if Equal **`beq reg1,reg2,label` 

      - if reg1=reg2,go to label
      - otherwise go to the next instruction
    - **Branch If Not Equal** `bne reg1,reg2,label `
	  - If value in reg1 ≠ value in reg2, go to label
    
    - **Jump **   ` j label `
    
      - Unconditional jump to label
      ``` c
	  if(s0==s1){
	      s2=s3+0;//s2=s3
	    }
	  else{
	      s2=0-s3;//s2=-s3
	    }
	  ```
	  
       ``` assembly
       RISCV (beq):
       beq s0,s1,then
       else:
       sub s2, x0, s3
       j end			#unconditional jump
       then:
       add s2, s3, x0
	   end:
	   
	   RISCV (bne):
	   bne s0,s1,else
	   then:
	   add s2, s3, x0
	   j end
	   else:
	   sub s2, x0, s3
	   end:
	   ```
	
	- **Branch Less Than**    `blt reg1,reg2, label `
	  -  If value in reg1 < value in reg2, go to label
	
	- **Branch Greater Than or Equal**  `bge reg1,reg2, label`
	  -  If value in reg1 >= value in reg2, go to label
		``` c
		if(S0<S1) {
		s2 = s3 /* then */
		} else {
		s2 = -s3 /* else */
		}	  
		```
		``` assembly
		RISCV(blt):
		blt s0,s1,else
		else:
		add s2,s3,x0
		j end
		else:
		sub s2,x0,x3
		end:
		
		RISCV(bge):
		bge s0,s1,else
		then:
		sub s2,x0,s3
		j end
		else:
		add s2,s3,x0
		end:
		
		```

2. Program Counter
	- Branches and Jumps works by modifying the PC
	- The PC is a *special register* that contains the address of the current instructions(codes) that is being executed

## 7. Shifting Instructions

- **Logical shift**

- **Arithmetic shift**

  |      Instruction Name      |      RISCV       |
  | :------------------------: | :--------------: |
  |     Shift Left Logical     |  `sll s1,s2,s3`  |
  |   Shift left Logical Imm   | `slli s1,s2,imm` |
  |    Shift Right Logical     |  `srl s1,s2,s3`  |
  |  Shift Right Logical Imm   | `srli s1,s2,imm` |
  |   Shift Right Arithmetic   |  `sra s1,s2,s3`  |
  | Shift Right Arithmetic Imm | `srai s1,s2,imm` |

	>When using immediate,only values 0-31 are practical
	>
	>When using variable,only the lowest 5 bits are used (2^5=32)

## 8.Other Useful Instructions

1. Multiplication 
   - `mul dst,src1,src2`->lower 32 bits
   - `mulh dst,src1,src2`->upper 32 bits

2. Division
   - `div dst,src1,src2`->quotient
   - `rem dst,src1,src2`->remainder

3. Bitwise Instructions

	|      Instruction       |        c        |      RISCV       |
	| :--------------------: | :-------------: | :--------------: |
	|          And           |   `s1=s2&s3;`   |  `and s1,s2,s3`  |
	|     And Immediate      |  `s1=s2&0x1;`   | `andi s1,s2,0x1` |
	|           Or           |   `s1=s2|s3;`   |  `or s1,s2,s3`   |
	|      Or Immediate      |  `s1=s2|0x5;`   | `ori s1,s2,0x5`  |
	|      Exclusive Or      |   `s1=s2^s3;`   |  `xor s1,s2,s3`  |
	| Exclusive Or Immediate | `a = b ^ 0xF; ` | `xori s1,s2,0xF` |
	
	

4. Compare Instructions
   - Set Less Than
     - `slt dst,reg1,reg2`
     - if `reg1<reg2`,dst=1,else dst=0
   - Set Less Than Immediate
     - `slti dst,reg1,imm`
     - if `reg1<imm`,dst=1,else dst=0

	```c
	if(s0<s1){
	    s2 = s3 /* then */
	} else {
		s2 = -s3 /* else */
	}
	```

	```Assembly
	RISCV:
	slt t0,s0,s1
	beq x0,t0,else
	then:
	add s2, s3, x0
	j end
	else:
	sub s2, x0, s3
	end:
	```