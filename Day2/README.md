
![flyer](https://user-images.githubusercontent.com/67062356/200188093-c97ee488-2d62-425c-9cc9-80443cf2b426.png)
# RISC-V based MYTH WORKSHOP
This repository contains all the information needed to build a RISC-V pipelined core, which has support of base interger RV32I instruction format using TL-Verilog on makerchip platform. This was done as part of a 5 day workshop organised by VSD and Redwood EDA
# Table of Contents

# Introduction to RISC-V ISA
ISA-Instruction Set Architecture
ISA acts as an interface between the hardware and the software(e.g. C)
Whenever you run an app on your computer, its function (high level program) is converted to its respective assembly language program using a compiler. It is then converted into machine level code using an assembler. Finally, this machine code (also known as a bitstream) is fed into the chip layout, which will perform its function accordingly.

This project aims to design a RISC V microprocessor core and understand its various functions. We will start with a simple c program then look into its assembly and machine language code. Before that, let us see some basic commands we need to know to implement this in a Linux based system
## Types of Instructions 
- Pseudo Instructions
- Base Integer Instructions
- Multiply Extension
- Single and Double precision floating point extension
- Application Binary Interface(ABI)
- Memory Allocation and Stack Pointer
# GNU Compiler toolchain
To view and edit your program file use the following command
```
leafpad <filename> & Leafpad is a texteditor.
```
To compile your program use the following command:
```
gcc <filename>
```
To view the output of the program use the following command: 
```
./a.out
```
To use the risc-v gcc compiler use the following command:
```

riscv64-unknown-elf-gcc -o1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
```
More generic command with different options:
```
riscv64-unknown-elf-gcc <compiler option -O1 ; Ofast> <ABI specifier -lp64; -lp32; -ilp32> <architecture specifier -RV64 ; RV32> -o <object filename> <C filename>
```

To view assembly code use the below command:
```
riscv64-unknown-elf-objdump -d <object filename>
```
To use SPIKE simualtor to run risc-v obj file use the below command,
```
spike pk <object filename>
```
To use SPIKE as debugger
``
spike -d pk <object Filename> 
``
with debug command as
``
until pc 0 <pc of your choice>
``
Output of program to compute the sum of numbers 1 to 9
- ![image](https://user-images.githubusercontent.com/67062356/200189355-33314d53-6f99-461f-aa70-dccb680283de.png)
# ABI
- Application Binary Interface(System call interface)
- The application program can directly access the registers of the RISC V architecture using system calls. 
- XLEN-Width of the registers
- RV64 and RV32, the widths are 64 bits and 32 bits, respectively.
- RISC V belongs to the little endian memory addressing system, which means that the least significant byte of a word is stored in the lowest memory address.
- Instructions which operate only on regs are called R type
- Instructions which operate on immediate and regs are called I type 
- Instructions which operate on source regs and storing instr are called S type 
- ![image](https://user-images.githubusercontent.com/67062356/200190201-ef26e0fc-674f-48cf-8ea6-5655b74a5467.png)



- ![image](https://user-images.githubusercontent.com/67062356/200189996-522312b1-08bf-4d82-9bd3-c467639c19f5.png)
Program to compute sum of nums using system calls
![image](https://user-images.githubusercontent.com/67062356/200190291-c4ffc775-2f45-4e77-b96e-76dd40315663.png)
- Assembly level program
![image](https://user-images.githubusercontent.com/67062356/200190330-7a26a613-4406-4372-a9db-bc6967789df0.png)

- Spike output
![image](https://user-images.githubusercontent.com/67062356/200191739-a1d7f9ea-2902-4d2b-97f5-c84addf92ef7.png)
- Assembly File
![image](https://user-images.githubusercontent.com/67062356/200191776-ed4a1fca-06b7-4332-826b-5aefcec574ff.png)
- Simulation output using RV core
![image](https://user-images.githubusercontent.com/67062356/200191803-9f2c9503-84a4-4d6f-935a-463f6862915e.png)
- Hex Output File
![image](https://user-images.githubusercontent.com/67062356/200191861-27d7db25-14be-4c75-af40-d9b93014f574.png)
## This concludes Day 2


