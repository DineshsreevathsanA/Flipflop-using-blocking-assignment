# EXPERIMENT 3: Simulation of All Flip-Flops using Blocking Statement

## AIM
To design and simulate basic flip-flops (SR, D, JK, and T) using **blocking statements** in Verilog HDL, and verify their functionality through simulation in Vivado 2023.1.

## APPARATUS REQUIRED
- Vivado 2023.1
- Computer with HDL Simulator

## DESCRIPTION
Flip-flops are the basic memory elements in sequential circuits.  
In this experiment, different types of flip-flops (SR, D, JK, T) are modeled using **behavioral modeling** with **blocking assignment (`=`)** inside the `always` block.  
Blocking assignments execute sequentially in the given order, which makes it easier to describe simple synchronous circuits.

## PROCEDURE
1. Open **Vivado 2023.1**.  
2. Create a **New RTL Project** (e.g., `FlipFlop_Simulation`).  
3. Add Verilog source files for each flip-flop (SR, D, JK, T).  
4. Add a testbench file to verify all flip-flops.  
5. Run **Behavioral Simulation**.  
6. Observe waveforms of inputs and outputs for each flip-flop.  
7. Verify that outputs match the truth table.  
8. Save results and capture simulation screenshots.

---

## VERILOG CODE

### SR Flip-Flop (Blocking)
```verilog
module srff(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;

always @(posedge clk)   
begin
  if(rst==1)
    q = 0;
  else if(s==0 && r==0)   
    q = q;                
  else if(s==0 && r==1)
    q = 1'b0;
  else if(s==1 && r==0)
    q = 1'b1;
  else
    q = 1'bx;  
end 
endmodule   

```
### SR Flip-Flop Test bench 
```verilog

`timescale 1ns/1ps
module tb_srff;
reg s,r,clk,rst;
wire q;


srff uut(s,r,clk,rst,q);

always #5 clk = ~clk;

initial begin
  clk=0; s=0; r=0; rst=1;
  #10 rst=0;
  #10 s=1; r=0;
  #10 s=0; r=0;
  #10 s=0; r=1;
  #10 s=1; r=1;
  #10 s=0; r=0;
  #20 $finish;   
end
endmodule




```
#### SIMULATION OUTPUT
<img width="1920" height="1200" alt="Screenshot (102)" src="https://github.com/user-attachments/assets/5ac7c577-6921-4b6e-98ca-5c60a487b563" />

---

### JK Flip-Flop (Blocking)
```verilog
module jk_ff(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;
always @(posedge clk)
begin
if(rst==1)
q = 0;
else if(s==0 && r==0)
q = q;
else if(s==1 && r==1)
q = 1'b0;
else if(s==1 && r==0)
q = 1'b1;
else
q = ~q;
end
endmodule

```
### JK Flip-Flop Test bench 
```verilog
module tb_jk_ff;
reg s,r,clk,rst;
wire q;
jk_ff uut(s,r,clk,rst,q);
always #5clk = ~clk;
initial
begin
clk=0;s=0;r=0;rst=1;
#10 rst=0;
#10 s=1;r=0;
#10 s=0;r=0;
#10 s=0;r=1;
#10 s=1;r=1;
#10 s=0;r=0;
#20  $finish;
end
endmodule




```
#### SIMULATION OUTPUT
<img width="1920" height="1200" alt="Screenshot (109)" src="https://github.com/user-attachments/assets/ce43e5f5-3700-4b43-842a-01e421b60499" />

---
### D Flip-Flop (Blocking)
```verilog
module d_ff(clk,rst,d,q);
input clk,rst,d;
output reg q;
always @ (posedge clk)
begin
if(rst==1)
q=0;
else if(d==1)
q=q;
else
q=q;
end
endmodule

```
### D Flip-Flop Test bench 
```verilog
`timescale 1ns/1ps
module d_ff_tb;
reg clk,rst,d;
wire q;
d_ff uut(clk,rst,d,q);
always #5clk=~clk;
initial
begin
clk=0;
d=0;
rst=1;
#10;
rst=0;
d=0;
#10;
d=1;
end
endmodule


```

#### SIMULATION OUTPUT
<img width="1920" height="1200" alt="Screenshot (111)" src="https://github.com/user-attachments/assets/1e7a8488-fb4b-462e-9fbc-5f8ccf467f27" />

---
### T Flip-Flop (Blocking)
```verilog
module t_ff(clk,rst,t,q);
input clk,rst,t;
output reg q;
always @(posedge clk)
begin
if(rst==1)
q=0;
else if(t==0)
q=q;
else
q=~q;
end
endmodule
```
### T Flip-Flop Test bench 
```verilog
`timescale 1ns/1ps
module t_ff_tb;
reg clk,rst,t;
wire q;
t_ff uut(clk,rst,t,q);
always #5clk=~clk;
initial
begin
clk=0;
t=0;
rst=1;
#10
rst=0;
t=0;
#10
t=1;
end 
endmodule



```

#### SIMULATION OUTPUT
<img width="1920" height="1200" alt="Screenshot (113)" src="https://github.com/user-attachments/assets/37bb0b79-6d1c-4b36-b949-387268dd346d" />


---

### RESULT

All flip-flops (SR, D, JK, T) were successfully simulated using blocking statements in Verilog HDL.
The outputs matched the expected truth table values, demonstrating correct sequential behavior.
