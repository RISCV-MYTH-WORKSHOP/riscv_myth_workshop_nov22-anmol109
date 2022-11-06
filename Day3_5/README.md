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

- Pipelining is done to operate the circuit at a higher frequency. 
- The pipeline is divided into stages, and each stage can execute its operation concurrently with the other stages.
- In TL-Verilog we declare a pipeline as ``` |<pipline name>``` and its stages as ```@<stage>```
- Timing Abstract Representation is a powerful feature of TL-Verilog which makes pipelining and retiming a lot easier compared to other HDLS
- ![image](https://user-images.githubusercontent.com/67062356/200195162-a6794cca-9238-4c0d-a666-19964abca9dd.png)
- Pipelined Calculator
# Validity
- Validity is the notion of when values of signals are meaningful.
- It makes waveform easier to debug and provides clock gating.
- Clock gating is a technique used in many sequential circuits to reduce power dissipation. It removes the clock signal when the circuit is not in use . 
- Clock Gating is not a well defined concept in other HDLs
- Code under ```|pipe``` with stages defined as ```@?``` is used for valid when? check
- ![image](https://user-images.githubusercontent.com/67062356/200195327-a81dd7e2-faf9-4c79-88d2-f3ec558c53f3.png)
- Calculator with validity
- ![image](https://user-images.githubusercontent.com/67062356/200195376-177e3444-8751-442f-adac-d4678d9e3137.png)
-Calculator with memory and recall




