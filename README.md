# asic_class

This repository guides you to complete the ASIC flow from scratch .
# VLSI Physical Design for ASICs 

The objective of VLSI physical design for ASIC is to transform a digital circuit logic representation into a physical layout meeting the power,performance,area and manufacturability requirements .


**If you need to know about basic instructions you can read through them here , the daywise labs are in thier respective folders , the commands needed for them along with their explanations are also in those folders. The pre-requisites for installation will be at the end of the readme file , feel free to scroll down and install them!**


## Table of contents 
<details>
 <summary> DAY1 </summary>


### DAY1
********
*Introduction to RISCV ISA and GNU Compiler Toolchain*


Basic keywords you need to know before proceeding :

* *ISA*
   - An ISA or the Instruction Set Architecture is part of the abstract model of the computer that defines how the CPU is controlled by the software . It acts as an interface between the hardware and the software,specifying both what the processor is capable of doing as well how it gets done.
 
 
* *RISC-V*
   - RISC-V is a versatile and open ISA that promotes collaboration and innovation in processor design and development.
  

* *Compiler*
   - A compiler is a software tool  that translates high-level programming code into machine code that can be executed directly by a computer's hardware .
 
 
* *Assembler*
   - A program or tool that translates assembly language code into machine code that can be executed by a computer's cpu.
 
* *ALP*
   - Assembly language is a low level programming lnguage that is closely related to the architecture of specificcomputer's cpu .
 
 
* *HDL*
   - Hardware Description language used for designing and describing digital hardware circuits . 
    - Eg: Verilog , System Verilog,VHDL
 
 
* *GDS*
   - Graphic data system: GDSII files contain information about the geometric shapes, layers, masks, and other essential details that make up the physical layout of a chip.
 
 
 
 
 
### Basic pre-requisites to be installed in your system and installation of the tool 
***********

```
sudo apt update 
sudo apt upgrade 

git clone https://github.com/kunalg123/riscv_workshop_collaterals.git

cd riscv_workshop_collaterals

chmod +x run.sh
 
./run.sh
```

## 1. Create a simple C program that calculates sum from 1 to N
**********



Compile it using C compiler 
 ```
 gcc sum1.c -o sum1.o
 ./sum1.o
 
 ```
 
![sum o](https://github.com/AdrikaMohanty/asic_class/assets/84654826/d9aa2424-8b57-4c4d-9943-7cc6ceb5dc3f)


Compiling using riscv compiler :
```
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1.o sum1.c

```
*********


+ ```O<number>```: refers to the level of optimization 
+ ```-mabi```:  specifies the ABI to be used during code generation according to the requirements 
+ ```-march```:  specifies target architecture 

*To view the disassembled ALP code*:

```riscv64-unknown-elf-objdump -d sum1.o```

* use the command ```riscv64-unknown-elf-objdump -d 1_to_N.o | less```
* use /instance to search for instance 
* press enter 
  *Main when used O1 optimisation*

![O1opt](https://github.com/AdrikaMohanty/asic_class/assets/84654826/c36f002f-05f4-4d8c-8a43-c7ed45b3b08b)

now use Ofast optimization :

![Ofast](https://github.com/AdrikaMohanty/asic_class/assets/84654826/0a345e54-7a30-4e6b-9d9c-dd24d132a2dd)

after using the spike debugger we can see line by line execution of the code :

```until pc 0 100b0```: tells until where it should execute and stop
after that press enter for line by line execution .
Here I have showed with the sp values :

![bfr_aftr_sp](https://github.com/AdrikaMohanty/asic_class/assets/84654826/b70770eb-d862-4332-8345-f5d038740293)




## 2. Write a program to display the max and min 64 bit signed number and max 64 bit unsigned numbers:



![Screenshot from 2023-08-21 15-19-41](https://github.com/AdrikaMohanty/asic_class/assets/84654826/b24b9f68-587f-4fb5-8cab-11938652baec)


</details>

<details>
 <summary>DAY2</summary>

 ### DAY2

### ABI: Application Binary Interface

Interface is the appearance provided to the user.
Given an application to run on hardware, there are multiple interface in between for it to run on hardware , this is done by application binary interface.
Given below is a pictorial representation of how from an application to hardware everything is interfaced 

![image](https://github.com/AdrikaMohanty/asic_class/assets/84654826/2b904f1d-a159-42f1-bd2c-13ca4d2802a1)

+ The parts of ISA that are accessible to User: User ISA
+ The parts of ISA accessible to the OS: system ISA
+ The access is done using system calls
+ The ABI accesses the system via *Registers*.

### ABI Names :
+ Specific name through which you can access the internal registers of the risc-v CPU core .
+ The ABI names and their corresponding usage are given below :
  ![image](https://github.com/AdrikaMohanty/asic_class/assets/84654826/47f643d1-b3fb-4ece-93c9-dca4b3fb5d0b)

### Base integer instructions :
*RISCV belongs to the little endian memory addressing system*
There are 47 base instructions present in RISC-V ISA 

1. R-type (Register type ):
   They operate on registers and have fixed format for their operands

2. I - types (Immediate type):
   These instructions have an immediate operand and one register operand.

3. S-type (Store-type):
   These instructions are used for storing values from registers to memory.

4. B-type (Branch-type):
   These instructions perform conditional branching based on comparisons.

5. U-type(Upper Immediate Type):
   Have a larger immediate field for encoding larger constants.

6. J-type (Jump type):
   Used for unconditional jumps and functional calls.


-------------

## Simulation of a C program using ABI function call and execution 
**********
![sum_cust](https://github.com/AdrikaMohanty/asic_class/assets/84654826/40a47d17-36a8-4434-93ea-cafc90954cd7)


 ![sum_cust_obj](https://github.com/AdrikaMohanty/asic_class/assets/84654826/55b7e09c-9e8e-4a8d-98ce-dfb9681644d5)

</details>
 
________________________________
____________________________________

# RTL Design using Verilog with SKY130 technology

_______________

<details>
 <summary>DAY1 </summary>

 
</details>

