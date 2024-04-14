# RISC-V, RISC-V Functions

## 1 Pseudo-Instructions

### 1.1 Pseudo-Instructions

- instructions that aren't really implemented by the hardware

- translated into real instructions

	``` assembly
	Example: 
		mv dst,reg1
	translates_into:
		addi dst,reg1,0
	```

### 1.2 More Pseudo-Instructions

-  Load Immediate

  ```assembly
  li dst,imm
  #loads 32-bit immediate into dst
  #utilizes addi ,lui
  ```

- Load Address

  ```assembly
  la dst,label
  #loads address of specified label into dst
  #translates to : auipc dst,<offset to label>
  ```

- No Operation

  ```assembly
  nop
  #Do nothing
  #translates to : addi x0.x0.0
  ```

  

## 2 Functions in Assembly

### 2.1 Six Steps of Calling a Function

1. put *arguments* in a place where the function can access them -- Place arguments

2. Transfer control to the function --Jump to  function

3. The function will acquire any (local) storage resources it needs --create local storage
4. The function performs its desired task --what to do
5. The function puts *return value* in an accessible place and ''cleans up'' --what we want
6. Control is returned to you --jump back to caller

- **For 1 and 5: Where should we put the arguments and return values?** 

  - `a0-a7`: eight *argument* registers to pass parameters

  - `a0-a1` : two *argument* registers used to return values

    > Orders of arguments matters
    >
    > if we need more ,use the **STACK**! 

- **For 2 and 6 : How do we Transfer Control?**

  - Jump

    ```assembly
    #Note that j is a pseudo instruction
    	j label
	  translate_into:
    	jal x0,label
	  ```
  
	- 'Link': saves the location of instruction in a register before jumping
  
    - jump and  Link
  
	    ```assembly
      jal dst,label #store the current address to dst and jump to label
	    ```
  
    - Jump and Link Register 
  
	    ```assembly
	    jalr dst,src,imm #store the current address to dst and jump to src[imm]
	    ```
	
	  > these two used to invoke a function
	
	- Jump Register
	
	  ```assembly
	  jr src 
	  ```
	
	  > used to return from a function
	
	- ra:  return address register, used to save *where a function is called from*, so we can get back

- **for 3:Local storage for variables**

  - Stack pointer holds the address of the bottom of the stack

    ```assembly
    #store t0 to the stack
    addi sp,sp,-4 #stack grows downwards,need to decrement it
    sw t0,0(sp)
    ```

### 2.2 Function Calling Conventions

- **Calle*R***: the calling function
- **Calle*E*** : the function being called

```c
void functionA(void) //calleR
{
    // do stuff
    functionB(void);//calleE
    // do more stuff
    return;
}
```

- **Saved** Registers(Callee Saved)
  - These registers are supposed to be the same before and after calling  functions
    - if Callee wants to use them,it must restore these registers
  - s0-s11(saved registers)
  - sp(stack pointer)
- **Volatile** Registers (Caller Saved)
  - These registers *can be freely changed* by the calleE
    - if calleR needs them,it must store these values before calling a function
  - t0-t6(temporary registers)
  - a0-a7(argument registers)
  - ra(return address)

