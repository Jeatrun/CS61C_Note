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

   - lb(load byte) sb(store byte)

     > s0 = 0x00000180:
     >
     > `lb s1,1(s0)   # s1=0x00000001`
     >
     > `lb s2,0(s0)   # s2=0xFFFFFF80`
     >
     > `sb s2,2(s0)  #*(s0)=0x00800180`

4. Half-Word instructions

