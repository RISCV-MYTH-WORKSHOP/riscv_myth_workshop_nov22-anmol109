# RISC-V_MYTH_Workshop

For students of "Microprocessor for You in Thirty Hours" Workshop, offered by for VLSI System Design (VSD) and Redwood EDA, find here accompanying live info and links.

Refer to README at [stevehoover/RISC-V_MYTH_Workshop](https://github.com/stevehoover/RISC-V_MYTH_Workshop) for lab instructions.

Add your codes in the [calculator_solutions.tlv](calculator_solutions.tlv) and [risc-v_solutions.tlv](risc-v_solutions.tlv) files and **keep committing** to your repository after every lab.
![flyer](https://user-images.githubusercontent.com/67062356/200188093-c97ee488-2d62-425c-9cc9-80443cf2b426.png)
# RISC-V based MYTH WORKSHOP
This repository contains all the information needed to build a RISC-V pipelined core, which has support of base interger RV32I instruction format using TL-Verilog on makerchip platform. This was done as part of a 5 day workshop organised by VSD and Redwood EDA
# Makerchip 
- Makerchip is a free online IDE for developing in Verilog or TL-Verilog. It can be used directly in your browser. You can code, simulate and view block diagrams and waveforms.
- It also features multiple examples and templates.
- Using TL Verilog in makerchip saves a lot of time and code as compared to other HDLs
# Combinational Logic
- Starting with basic example in combinational logic is an inverter. To write the logic of inverter using TL-verilog is $out = ! $in;. 
- Implementation of other logic gates and other basic designs such as a 2:1 MUX 
- ![image](https://user-images.githubusercontent.com/67062356/200193758-495b1cf7-0115-49a8-a88f-ccc059e09e15.png)
- And Gate output
- ![image](https://user-images.githubusercontent.com/67062356/200193774-0d9b2122-5a9b-4453-a9f9-9e3b830309f3.png)
- Mux Output
- ![image](https://user-images.githubusercontent.com/67062356/200193797-a09b5741-4faa-4f89-8dac-55804db6fb1c.png)
- Basic Calculator Output
# Sequential Logic
Starting with basic example in sequential logic is Fibonacci Series with reset. To write the logic of Series using TL-Verilog is ``` $num[31:0] = $reset ? 1 : (>>1$num + >>2$num)``` . 
- Here >>1 and >>2 provides the output value from previous cycles.
- Sequential calculator with reset and memory
- ![image](https://user-images.githubusercontent.com/67062356/200193898-7302995d-3355-4000-826c-1ee7ae818852.png)
# Pipelined Logic

Pipelining is done to operate the circuit at a higher frequency. 
- The pipeline is divided into stages, and each stage can execute its operation concurrently with the other stages.
- In TL-Verilog we declare a pipeline as ``` |<pipline name>``` and its stages as ```@<stage>```
- Timing Abstract Representation is a powerful feature of TL-Verilog which makes pipelining and retiming a lot easier compared to other HDLS
- ![image](https://user-images.githubusercontent.com/67062356/200195162-a6794cca-9238-4c0d-a666-19964abca9dd.png)
- Pipelined Calculator
# Validity
Validity is the notion of when values of signals are meaningful.
- It makes waveform easier to debug and provides clock gating.
- Clock gating is a technique used in many sequential circuits to reduce power dissipation. It removes the clock signal when the circuit is not in use . 
- Clock Gating is not a well defined concept in other HDLs
- Code under ```|pipe``` with stages defined as ```@?``` is used for valid when? check
 ![image](https://user-images.githubusercontent.com/67062356/200195327-a81dd7e2-faf9-4c79-88d2-f3ec558c53f3.png)
- Calculator with validity
 ![image](https://user-images.githubusercontent.com/67062356/200195376-177e3444-8751-442f-adac-d4678d9e3137.png)
- Calculator with memory and recall

# RISC-V Micro Architecture
- ![image](https://user-images.githubusercontent.com/67062356/200195603-0a5bc7f6-94c1-4b3a-a9f1-002bdee32d14.png)
 We will implement this design using 4 stages:
- Fetch
- Decode
- Read and write
- ALU
## Fetch Cycle
- PC(Program Counter) contains the address for the next instruction.
- IMEM contains the set of instructions.
- The processor will fetch the instruction whose address is stored in PC.
![image](https://user-images.githubusercontent.com/67062356/200195752-031152ed-6c0d-46dc-99fd-b2d7ffba80c5.png)
- Fetch Logic Implemented output
## Decode Cycle
There are 6 types of Instructions:
- R-type - Register
- I-type - Immediate
- S-type - Store
- B-type - Branch (Conditional Jump)
- U-type - Upper Immediate
- J-type - Jump (Unconditional Jump)
- We will decode ```instr[6:2]``` which is the opcode of the instruction, we are ignoring the first 2 bits since they are always 1.

- We will also consider immediate value, source address, destination address, funct7, funct3.

- Once we have all of the above fields we can now extract which type of instruction is being fetched
![image](https://user-images.githubusercontent.com/67062356/200195968-287d3ff6-a9fe-4a37-b6d2-e22e42603833.png)
- Final decoding operation
## ALU
- After getting the values from register file read, we store ```$rf_rd_data1[31:0]``` and ```$rf_rd_data2[31:0]``` in ```$src1_value[31:0]``` and ```$src1_value[31:0]``` respectively.
- For now we will perform the arithematic operations 'add' and 'addi' on them. We will add more operations in the final code.
- add : will perform addition operation on the two operands.
- addi : will add the first operand value with immediate value ```$imm```.
- Register file write will be performed after ALU operations.
![image](https://user-images.githubusercontent.com/67062356/200274437-e3df4e76-13bd-44b1-99a8-d871ac2cdc57.png)
- Final ALU code
## Register File Read and Write
- Register file in this cpu is capable of performing 2 reads and 1 write simultanously
![image](https://user-images.githubusercontent.com/67062356/200196099-31ab081a-5c3b-447e-b89e-23a7dc561fa6.png)
Inputs:

- ```$rf_rd_en1``` : enable signal for the first read operation.
- ```$rf_rd_en2``` : enable signal for the second read operation.
- ```$rf_rd_index1[4:0]```: first address from where data has to be read.
- ```$rf_rd_index2[4:0]```: second address from where data has to be read.
- ```$rf_wr_en``` : enable signal for write operation.
- ```$rf_wr_index[4:0]``` : address where data has to be written.
- ```$rf_wr_data[31:0]``` : data to be written in the write address.
Outputs:

- ```$rf_rd_data1[31:0]```: data from read index 1.
- ```$rf_rd_data2[31:0]```: data from read index 2.
![image](https://user-images.githubusercontent.com/67062356/200196301-50c0fe86-945d-4e0a-990a-05908a841230.png)
- final code for reg file read and write


## Control Logic
In RISC V branches are defined as conditional branches, i.e, they will only execute when certain conditions are met whereas jumps are unconditional.
![image](https://user-images.githubusercontent.com/67062356/200275235-6f634ba1-a55b-4c9e-81fc-75fe48048211.png)
- Final branch Code
![image](https://user-images.githubusercontent.com/67062356/200275492-511fcad9-0afe-4236-9716-6ded3618b925.png)
- Final output after implementing branch, working RISC-V core
# Pipelining
![image](https://user-images.githubusercontent.com/67062356/200276363-2f5e9d8b-fc1d-4fb6-b906-2a91f86b7e87.png)
- Converting non-piepleined CPU to pipelined CPU using timing abstract feature of TL-Verilog. This allows easy retiming wihtout any risk of funcational bugs
- A waterfall logic diagram makes it easier for us to see the flow of logic and makes pipelining simpler.
- Pipelining is performed to increase speed and throughput, but while pipelining  problems arise,
![image](https://user-images.githubusercontent.com/67062356/200277050-4db1e274-02ca-431a-9997-087023cb6d20.png)
## Hazards
Due to interdependent nature of data between cycles, issues arise, these are known as hazards.
In the figure above, 2 kinds of hazards are shown
- First is related to the branch instruction, this is known as a control flow hazard. Here PC is expecting a value from branch target two cycles before that value is actually calculated.
- Second is related to the register file write, this is known as a read after write hazard. We dont need to read a value that is written until stage 4 in the first instruction but we might need to read it for the second instruction in stage 2, which is a one cycle early.
![image](https://user-images.githubusercontent.com/67062356/200277683-e9a262e5-7301-42fd-8de9-edd6cf75a688.png)
-Instruction cycle explanantion
One simple solution is to make the circuit run every 3 cycles, but this leads to slower performance
![image](https://user-images.githubusercontent.com/67062356/200277973-ce70cebf-d4e2-4026-8365-4823765b0de8.png)
- This resolves the control flow hazard
- We will use the following code to implement this:
- ```$start = ((>>1$reset)&&(!$reset))? 1'b1: 1'b0;```
- ```$valid = $start ? 1'b1: >>3$valid ? 1'b1 : 1'b0;```
- To avoid the read after write hazard use the following code:
- ```$src1_value[31:0] = ((>>1$rd == $rs1) && (>>1$rf_wr_en))? >>1$result : $rf_rd_data1[31:0];```
- ```$src2_value[31:0] = ((>>1$rd == $rs2) && (>>1$rf_wr_en))? >>1$result : $rf_rd_data2[31:0];```
- Here we take 2 cycle penalty for branch instructions

## Load Store Instructions
#### Inputs:

- ```$dmem_wr_en``` :Enable signal for write operation
- ```$dmem_rd_en``` :Enable signal for read operation
- ```$dmem_addr[3:0] ```:Address where we have to read/write
- ```$dmem_wr_data[31:0]```:Data to be written in address (store)
#### Output:

- ```$dmem_rd_data[31:0]```:Data to be read from address (load)
![image](https://user-images.githubusercontent.com/67062356/200279738-957909a9-43c3-49ef-a048-6e0c05d34e23.png)
- interfacing signals
## Jump Instructions
Jumps are unconditional branches
We deal with 2 kinds of jump instructions
- ```$is_jal```: Jump and link
- ```$is_jalr```: Jump and link register
![image](https://user-images.githubusercontent.com/67062356/200280283-728d88e0-7eeb-4d83-9e4b-1be488ae68e2.png)
- Codes for jump
# Complete RISC-V CPU Core
Finally after adding all the functionality and instructions, the Pipelined RISC-V CPU is ready.
![image](https://user-images.githubusercontent.com/67062356/200280694-fe3543e7-6531-4f9a-b995-1d51017af2c7.png)
![image](https://user-images.githubusercontent.com/67062356/200280730-4eef5216-e05e-46a6-a578-7b31cf67be86.png)
![image](https://user-images.githubusercontent.com/67062356/200280863-e1c94aee-3cc1-4424-979a-cfa7a52af961.png)
# Acknowledgements
- [Kunal Ghosh](https://github.com/kunalg123) , Co-founder, VSD Corp. Pvt. Ltd.
- [Steve Hoover](https://github.com/stevehoover), Founder, Redwood EDA
- [Shivam Potdar](https://github.com/shivampotdar), TA 
- [Shivani Shah](https://github.com/shivanishah269), TA 
