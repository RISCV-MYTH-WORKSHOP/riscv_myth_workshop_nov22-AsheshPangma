# VSD-RISC-V_based_MYTH

This repository provides all the information required to build RISC-V pipelined core that supports base integer RV32I instruction format using TL-Verilog on makerchip platform. First we develop a simple calculator and used the similar logic to built our RISC-V core.

# Table of Contents

- [Day 1 Introduction to RISC-V ISA and GNU compiler toolchain](#day-1-introduction-to-risc---v-isa-and-gnu-compiler-toolchain)
  * [RISC-V basics](#rics---v-basics)
  * [Integer number representation](#integer-number-representation)
  * [Signed and unsigned arithmetic operation](#signed-and-unsigned-arithmetic-operation)
- [Day 2 Introductoion to ABI and basic verification flow](#day-2-introduction-to-abi-and-basic-verification-flow)
  * [Application Binary Interface](#application-binary-interface)
  * [ABI function call](#abi-function-call)
  * [Verification flow using iverilog](#verifivation-flow-using-iverilog)
- [Day 3 Digital Logic with TL-verilog and Makerchip](#day-3-digital-logic-with-tl-verilog-and-makerchip)
  * [Combinational logic](#combinational-logic)
  * [Sequential and pipelined logic](#sequential-logic)
  * [Validity and Hierarchy](#validity-and-hierarchy)
- [Day 4 Basic RISC-V CPU micro-architecture](#day-4-basic-risc---v-cpu-micro-architecture)
  * [Fetch](#fetch)
  * [Decode](#decode)
  * [Read and Write](#read-and-write)
  * [Execute](#execute)
  * [RISC-V control logic](#risc---v-control-logic)
- [Day 5 Complete Pipelined RISC-V CPU micro-architecture/store](#day-5-complete-pipelined-risc---v-cpu-micor---architecture/store)
  * [Pipelining the CPU](#pipelining-the-cpu)
  * [Load and store instructions and memory](#load-and-store-instructions-and-memory)
  * [Completing the RISC-V CPU](#completing-the-risc---v-cpu)
- [Acknowledgement](#acknowledgement)

# Day 1 Introduction to RISC-V ISA and GNU compiler toolchain

RISC(Reduced Instruction Set Computer) computers are designed with simpler ISA for faster computation and less complexity. A RISC-V ISA is defined as a base integer ISA that is characterized by
  * Width of the integer register(XLEN)
  * Corresponding size of the address space
  * Number of integer registers (32 in RISC-V)

In Linux, GNU Toolchain can be used to make and compile code to produce a proge=ram or library. CPU consists of very large number of transistors and can only understand binary numbers, 1's and 0's. The combination of 1's and 0's are fed to the CPU and based on the input it performs certain task. These inputs are called Machine language code. The high level program writted by programmers are compiled by the compiler to produce executable code. Assembler converts these executable code to relocatable machine code and finally Linker converts it into Absolute machine code.

  * To use the RISC-V gcc compiler, we use the following command:
  
`riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o <object filename> <C filename>`

`riscv64-unknown-elf-gcc <compiler option -O1 ; Ofast> <ABI specifier -lp64; -lp32; -ilp32> <architecture specifier -RV64 ; RV32> -o <object filename> <C filename>`

![](images/day1/1_1.1_sum1tonCode.png)

  * To run this C program we use the following command:
  ```
  gcc sum1ton.c
  ./a.out
  ``` 
The below figure shows the output.
![](images/day1/1_1.2_sum1tonRun.png)

To view assembly code, we use the following command:

`riscv64-unknown-elf-objdump -d <object filename>`

![](images/day1/1_1.3_main.png)

We can also use Spike simulator to run risc-v object file using the following command:

`spike pk <object filename>`

Spike debugger can be used using the following command:

`spike -d pk <object Filename>`

The code below is used to run our program till the given PC(Program Counter).

`until pc 0 <pc of your choice>`

![](images/day1/1_2_sum1tonDebug.png)

## Signed and unsigned arithmetic operation

The following C code is used to print the highest unsigned integer that can be represented in risc-v.

![](images/day1/1_3_unsignedHighestCode.png)

![](images/day1/1_9_unsignedHighestRun.png)

The following C code is used to print the highest and lowest signed integer that can be represented in risc-v.


![](images/day1/1_11_signedHighestCodeRun.png)



Follow the below link to install complete risc-v toolchain locally on linux machine.

  * [RISC-V GNU Toolchain](http://hdlexpress.com/RisKy1/How2/toolchain/toolchain.html)
  * [RISC-V ISA Simulator - Spike](https://github.com/kunalg123/riscv_workshop_collaterals)


# Day 2 Introductoion to ABI and basic verification flow

An ABI(Application Binary Interface) is used for translating relocatable machine code to absolute machine code specific to the architecture of machine. This means, ABI interface are used by application program to access the register specific to the architecture. In out case, it is RISC-V and there are 32 registers that can be used by applicatio programmer.
First we clone the repository as shown in the figure below:

![](images/day2/2_1_ls.png)

The picture below shows us the C program and the load function that the C program calls.

![](images/day2/2_1.1_sum1to9.png)

We run the C program using RISC-V gcc compiler as shown by the picture below below:

![](images/day2/2_1.2_sum1to9Run.png)

The assembly code for the above run is shown below:

![](images/day2/2_1.3_sum1to9main.png)





The following picture shows the script that is used to create hex file and load the files in picorv32 memory and run it. Iverilog takes testbench.v and picorv32.v as inputs and gives testbench.vvp as output.

![](images/day2/2_3_rvimsh.png)



The verilog code for testbench.v is shown by the picture below. Here, we see picorv32 is the uut(unit under test) and the hex file being loaded in the testbench.

![](images/day2/2_2_testFile.png)

First we make the script executable and then run the script. The output is obtained as shown below:

![](images/day2/2_4_run.png)





# Day 3 Digital Logic with TL-verilog and Makerchip

# Day 4 Basic RISC-V CPU micro-architecture

# Day 5 Complete Pipelined RISC-V CPU micro-architecture/store

## [Acknowledgement](#acknowledgement)
  * Kunal Ghosh, Co-founder, VSD Corp. Pvt. Ltd.
  * Steve Hoover, Founder, Redwood EDA
  * Shivam Potdar, GSoC 2020 @fossi-foundation
  * Shivani Shah, TA
