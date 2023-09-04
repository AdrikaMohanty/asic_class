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
 Intoduction to iverilog , Design and testbench using verilog 

 Design : Verilog code that is intended to functionally meet the required specifications 
 Test bench : Setup to apply the stimulus to design , basically to verify if the design is working properly .
 
 
 How the testbench works :

 ![Screenshot from 2023-08-31 21-03-04](https://github.com/AdrikaMohanty/asic_class/assets/84654826/01a484aa-5844-47ac-a553-1d96757e9e2a)

Output of simulator is a VCD (value change dump ) 
To view the waveform we use gtk wave in which we can observe for the  change in input how the output changes 


 ![Screenshot from 2023-08-31 21-08-20](https://github.com/AdrikaMohanty/asic_class/assets/84654826/58c02483-2245-45b0-a46f-caa4bd19472a)




 
### LAB 1:

Installing prerequisite , git cloning and running the iverilog file 

VSD directory 
```mkdir vsd```

```cd vsd```

```git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git```

You can go into the directory and explore the files , typing ```ls``` will give all the files in the directory .

The directory ```verilog_files``` has several verilog files example , for starters we will be loading and getting wave form for a mux .

```iverilog good_mux.v tb_good_mux.v```

This will compile the verilog file and test bench .

the output will be a vcd file , you can see it by typing ```./a.out```

To get the waveform type the below command 

```gtkwave tb_good_mux.vcd```

Common commands to compile the code and get the waveform :

``` iverilog filename.v filename_tb.v```

```gtkwave filename_tb.vcd```

![Screenshot from 2023-08-31 21-31-15](https://github.com/AdrikaMohanty/asic_class/assets/84654826/683e1a5d-9091-4459-b993-8d64dfcbda33)

![Screenshot from 2023-08-31 21-33-26](https://github.com/AdrikaMohanty/asic_class/assets/84654826/3c3eaa3f-7ec1-40c4-9328-4aaaa66fca23)

We can observe when sel line is low i0 is copied to y and sel is high i1 is copied to y .

### LAB 2:

Code of testbench and design module 


timescale 1ns / 1ps
module tb_good_mux;
	// Inputs
	reg i0,i1,sel;
	// Outputs
	wire y;

        // Instantiate the Unit Under Test (UUT)
	good_mux uut (
		.sel(sel),
		.i0(i0),
		.i1(i1),
		.y(y)
	);

	initial begin
	$dumpfile("tb_good_mux.vcd");
	$dumpvars(0,tb_good_mux);
	// Initialize Inputs
	sel = 0;
	i0 = 0;
	i1 = 0;
	#300 $finish;
	end

always #75 sel = ~sel;
always #10 i0 = ~i0;
always #55 i1 = ~i1;
endmodule

Design module :

module good_mux (input i0 , input i1 , input sel , output reg y);
always @ (*)
begin
	if(sel)
		y <= i1;
	else 
		y <= i0;
end
endmodule


## Introduction to yosys :

+ Yosys is a synthesizer 
+ Synthesis is the process of converting the RTL to netlist .
  ![Screenshot from 2023-08-31 21-50-20](https://github.com/AdrikaMohanty/asic_class/assets/84654826/7e02c685-67d8-4250-9106-6b507a681302)

  
 + With the ```write_verilog``` command it gives the netlist in terms of standard cells .
 + The netlist is the representation of the designs in terms of standard cells present in the ``` .lib``` file .


## Introduction to logic synthesis :

+ Logic synthesis :The design written in Verilog or VHDL is converted in to netlist .
+ .lib : This contains the standard cells to implement any boolean logic functionalities .

### Why do you need different flavours of gates ?
To achieve max clock speed and the least delay , we need to have various flavours of gates .
For ex to have no HOLD delays we need to have slower cells , hence we need to have different flavours of gates , slow as well as fast cells !
+ To charge/ discharge the capcitance we need transistors , these transistors decide the delays .
+ Wider transistors have lesser delay but consume more area and power
+ Narrow transistors have more delay but consume less area and performance .
+ Speed is a tradeoff with power and area .

Therefore the selection of cells for synthesiser should be done carefully , this selection is given as guidance to the synthesizer in terms of "constraints" .

### Yosys lab : LAB 3
Interactive flow :
+ Invoke yosys by just typing yosys in the the command prompt.
+ Specify technology libraray to be used , by typing this :
  ``` read_liberty -lib <PATH_TO_.libfile/sky130_fd_sc_hd__tt_025_1v80.lib>```
  ![yosys1](https://github.com/AdrikaMohanty/asic_class/assets/84654826/03e2afce-31ce-4d15-9bd4-7e6b94e0dc19)


+ Specify all verilog file to be synthesized , if you have multiple files then specify all of them .
  ![yosys2](https://github.com/AdrikaMohanty/asic_class/assets/84654826/399afab8-1047-47ed-b2e4-8b448331d04e)

+ ```synth -top good_mux``` for the synthesis of mux.

  ![yosys3](https://github.com/AdrikaMohanty/asic_class/assets/84654826/e6399b01-d274-4527-b62b-9ded2e4d8202)

+ ```abc``` is command that will convert our RTL file in to netlist/gate available in the sky130 lib file
+ Now to see the graphical representation of netlist use the command ```show```

  ![Screenshot from 2023-09-03 20-52-58](https://github.com/AdrikaMohanty/asic_class/assets/84654826/d10a6964-4c07-4bbd-90c5-ef65cb028cab)
+ To write the netlist to a verilog file use ```write_verilog <filename>.v ```

+ ```-noattr``` removes unwanted information from the mapped netlist
+With ```-noattr``` :

![Screenshot from 2023-09-03 21-02-01](https://github.com/AdrikaMohanty/asic_class/assets/84654826/c81c3e76-4e03-4709-9cb4-2c961f991273)

  
+Without ```-noattr```

![Screenshot from 2023-09-03 21-07-12](https://github.com/AdrikaMohanty/asic_class/assets/84654826/a8e8132c-119a-4fac-ab75-841637127b8f)

</details>

<details>
<summary>DAY2</summary>
 When you analyze the lib file you will see many new terms , all of these can be explored in the videos
	
 +  ```sky130``` : 130nm technology node
 +  ```fd``` : Foundary design
 +  ```sc``` : standard cell
 +  ```025C``` : temperature
 +  CMOS technology
 +  PVT : Process , voltage , temperature 
 ## Two types of synthesis: Hierarchical synthesis & flat synthesis 
 In hierarchial synthesis , submodules will be displayed as submodule block .
 In Flat synthesis the sub module data isn't visible , only the top module will be visible .

 the file used is ```multiple_modules.v``` it has two submodule and one main module 
  ```read_liberty -lib /home/adrika/vsd/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
     read_verilog multiple_modules.v
     synth -top multiple_modules
     abc -liberty /home/adrika/vsd/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
     show multiple_modules

```
### LAB1 AND LAB2
### Hierarchial Synthesis :
If you observe in the netlist file the hierarchy is preserved .


![Screenshot from 2023-09-03 22-03-06](https://github.com/AdrikaMohanty/asic_class/assets/84654826/60c4a224-da78-481f-b442-7ac15e02f17c)

### Flattened synthesis :


![Screenshot from 2023-09-03 22-08-56](https://github.com/AdrikaMohanty/asic_class/assets/84654826/f73dd814-a76e-4544-b041-e5bc33c96742)

Module level synthesis preffered when we have multiple instances of same module or divide and conquer approach .

## Different coding style of flops and why you need flops ??
To avoid additional additional effects of glitches due to propagation delay of gates we will have flops at the end of each combinational block , the flops store the initial value and avoid the glitch .

## D flip flop with asynchronous reset 

Gtkwave :

![Screenshot from 2023-09-03 22-48-40](https://github.com/AdrikaMohanty/asic_class/assets/84654826/0c109e4c-a2ca-4c4f-b261-ea014c3c0ce9)

![Screenshot from 2023-09-03 23-17-57](https://github.com/AdrikaMohanty/asic_class/assets/84654826/89e6bbac-ca07-411f-9440-11c1902e810a)

![Screenshot from 2023-09-03 23-22-20](https://github.com/AdrikaMohanty/asic_class/assets/84654826/10be3f17-f6ca-4edf-8b3b-031bc79af919)

## D flip flop with asynchrounous set 

Gtkwave :

![Screenshot from 2023-09-03 22-54-16](https://github.com/AdrikaMohanty/asic_class/assets/84654826/f7cae465-e8dc-4cfa-9cc3-bb39578722a5)

![Screenshot from 2023-09-03 23-25-10](https://github.com/AdrikaMohanty/asic_class/assets/84654826/27712500-e61b-4016-a668-f2736491ab2d)

## D flip flop with synchronous reset 

![Screenshot from 2023-09-03 23-13-04](https://github.com/AdrikaMohanty/asic_class/assets/84654826/591f6bf7-5113-44d2-a0eb-5dadf7c30ce1)

![Screenshot from 2023-09-03 23-26-33](https://github.com/AdrikaMohanty/asic_class/assets/84654826/2ef72818-1f24-4783-84f4-5dbbf7afe248)

![Screenshot from 2023-09-03 23-28-08](https://github.com/AdrikaMohanty/asic_class/assets/84654826/4237af4b-6014-4cc2-baac-fc2ab74fabad)

## Interesting optimizations :
### mult_2



if we observe the synthesis no cells will be present

![Screenshot from 2023-09-03 23-48-49](https://github.com/AdrikaMohanty/asic_class/assets/84654826/5b92f820-1429-445a-9540-c666d67d2aa6)

Now when you do ```abc``` it shows nothing to map since there is no standard cell to map

![Screenshot from 2023-09-03 23-50-32](https://github.com/AdrikaMohanty/asic_class/assets/84654826/dcff975b-64b2-415e-a10f-59fcba036c06)
![Screenshot from 2023-09-03 23-52-27](https://github.com/AdrikaMohanty/asic_class/assets/84654826/fd2e364e-f49d-4ab4-8700-eff277b45a4e)

multiplication with two is right shifting the number once 
### mult_8

![Screenshot from 2023-09-03 23-56-39](https://github.com/AdrikaMohanty/asic_class/assets/84654826/7ae073d7-d2bc-40f4-9b15-1a62eb95526f)



netlist :


![Screenshot from 2023-09-03 23-57-51](https://github.com/AdrikaMohanty/asic_class/assets/84654826/096f0381-7e78-4a6e-81b8-679059cae7fc)

 
</details>
<details>
<summary>DAY3</summary>

 Combinational and sequential logic optimizations

 + Combinational logic optimization : Squeeze the logic to get the most optimized design , efficient in terms of area and power . 
   + Constant propagation
   + Boolean logic optimization
 + Sequential logic optimization
   + Basic
     + Sequential constant propagation
   + Advanced :
     + Retiming
     + State optimization
     + Sequential logic cloning
    
### LAB:

+ Opt_check


  ![Screenshot from 2023-09-04 10-11-39](https://github.com/AdrikaMohanty/asic_class/assets/84654826/90e022f2-ad79-4a91-8666-b1a5073a0734)

  Command to do the combinational optimization is ```opt_clean -purge``` , shoud be done befor linking to abc



   ![Screenshot from 2023-09-04 10-14-55](https://github.com/AdrikaMohanty/asic_class/assets/84654826/5c1dee9a-5606-45da-9afc-c0014b96fdd9)


+ opt_check2


   ![Screenshot from 2023-09-04 10-16-04](https://github.com/AdrikaMohanty/asic_class/assets/84654826/8671ffde-929b-40fd-bd8c-029055d94567)


   ![Screenshot from 2023-09-04 10-16-51](https://github.com/AdrikaMohanty/asic_class/assets/84654826/a26bb33c-c70f-474b-9a0d-3b5a55de49c2)


+ opt_check3



  ![Screenshot from 2023-09-04 10-26-32](https://github.com/AdrikaMohanty/asic_class/assets/84654826/5ea7e460-6192-4e00-9848-88a246d232b6)



   ![Screenshot from 2023-09-04 10-28-16](https://github.com/AdrikaMohanty/asic_class/assets/84654826/7fcb0df4-be4c-4413-8502-6db809a64756)


+ multiple_modules_opt


  ![Screenshot from 2023-09-04 10-31-24](https://github.com/AdrikaMohanty/asic_class/assets/84654826/5db659a8-4979-4933-95eb-94624298d682)


  ![Screenshot from 2023-09-04 10-33-07](https://github.com/AdrikaMohanty/asic_class/assets/84654826/7df13a15-818e-4420-b015-b0660c93f53b)

for the multiple_modules_opt since it is a hierarchial design you need to flatten it before optimization .


### Sequential optimization techniques 

+ dff_const1


  ![Screenshot from 2023-09-04 11-03-01](https://github.com/AdrikaMohanty/asic_class/assets/84654826/64fa8f0d-f827-4cd0-9273-3baff5f7657a)



![Screenshot from 2023-09-04 11-03-53](https://github.com/AdrikaMohanty/asic_class/assets/84654826/126e57ea-6793-48cb-a8bf-f3d3a86eb63e)



+ dff_const2

  ![Screenshot from 2023-09-04 11-06-16](https://github.com/AdrikaMohanty/asic_class/assets/84654826/c2b16ee9-1907-42a9-b27d-d0ae56d36026)


+ dff_const3

 ![Screenshot from 2023-09-04 11-19-11](https://github.com/AdrikaMohanty/asic_class/assets/84654826/dd2dfbf7-8b89-4d79-b10b-5d0d41e88ff8)


 ![Screenshot from 2023-09-04 11-20-21](https://github.com/AdrikaMohanty/asic_class/assets/84654826/c854ad88-acb8-4282-b1eb-d05f6529ad4b)
 


+ dff_const4

  ![Screenshot from 2023-09-04 11-07-28](https://github.com/AdrikaMohanty/asic_class/assets/84654826/c6a4cd74-04d1-49d6-945d-212db19fa4c3)


 ![Screenshot from 2023-09-04 11-08-05](https://github.com/AdrikaMohanty/asic_class/assets/84654826/b5949085-b2a3-4bac-b8c0-b77e6885d8e2)



+ dff_const5

  ![Screenshot from 2023-09-04 11-11-53](https://github.com/AdrikaMohanty/asic_class/assets/84654826/fbc0da28-c508-4881-96e0-872f185f288b)



 ![Screenshot from 2023-09-04 11-17-33](https://github.com/AdrikaMohanty/asic_class/assets/84654826/9fadd954-9c53-4e8a-b593-22d2e134b628)


### Optimization of unused output 

+ counter_opt

  ![Screenshot from 2023-09-04 11-23-23](https://github.com/AdrikaMohanty/asic_class/assets/84654826/0e5147f4-a542-4cef-bf49-8ac407a88c4b)


  ![Screenshot from 2023-09-04 11-26-17](https://github.com/AdrikaMohanty/asic_class/assets/84654826/cba8db47-1716-483f-a49a-fb7bb547bbcc)


since 3 bit counter we would require only 3 flops , but output is only dependent on LSB so the other 2 are optimized . If there are primary out put and there are logic which are nowhere related to primary output then they will be all optimized .


+ counter_opt2

  ![Screenshot from 2023-09-04 11-33-07](https://github.com/AdrikaMohanty/asic_class/assets/84654826/4d7662ef-f1ab-4e11-abe6-f8a15b75b63a)

  ![Screenshot from 2023-09-04 11-34-07](https://github.com/AdrikaMohanty/asic_class/assets/84654826/2a632e97-7fd9-48c7-a810-4cac85666044)


</details>
