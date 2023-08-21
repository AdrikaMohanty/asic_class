# asic_class

This repository guides you to complete the ASIC flow from scratch .
# VLSI Physical Design for ASICs 

The objective of VLSI physical design for ASIC is to transform a digital circuit logic representation into a physical layout meeting the power,performance,area and manufacturability requirements .


**If you need to know about basic instructions you can read through them here , the daywise labs are in thier respective folders , the commands needed for them along with their explanations are also in those folders. The pre-requisites for installation will be at the end of the readme file , feel free to scroll down and install them!**


## Table of contents 

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
 -Hardware Description language used for designing and describing digital hardware circuits . 
 - Eg: Verilog , System Verilog,VHDL
 
 
* *GDS*
 - Graphic data system: GDSII files contain information about the geometric shapes, layers, masks, and other essential details that make up the physical layout of a chip.
 
 
 
 
 
### Basic pre-requisties to be installed in your system and installation of the tool 
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


```O<number>```: refers to the level of optimization 
```-mabi```:specifies the ABI to be used during code generation according to the requirements 
```-march```:specifies target architecture 

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





Before execution , sp values:




![bfr_sp](https://github.com/AdrikaMohanty/asic_class/assets/84654826/fba0a340-45ac-414f-ac34-837c1e055aac)







After execution sp values :




![after_sp](https://github.com/AdrikaMohanty/asic_class/assets/84654826/5d96715c-2612-45bd-a931-634cb75eccc4)









 
