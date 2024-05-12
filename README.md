# VLSI-LAB-EXP-4
# SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

# AIM: 
 To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Xilinx ISE.

# APPARATUS REQUIRED:

Xilinx 14.7 Spartan6 FPGA

# PROCEDURE:
1. Open Vivado: Launch Xilinx Vivado software on your computer.

2. Create a New Project: Click on "Create Project" from the welcome page or navigate through "File" > "Project" > "New".

3. Project Settings: Follow the prompts to set up your project. Specify the project name, location, and select RTL project type.

4. Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files from the file browser.

5. Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation language (Verilog in this case) and simulation tool (Vivado Simulator).

6. Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch the Vivado Simulator and compile your design for simulation.

7. Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set automatically. This determines how long the simulation will run.

8. Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.

9. View Results: After the simulation completes, you can view waveforms, debug signals, and analyze the behavior of your design.


**LOGIC DIAGRAM**

# SR FLIPFLOP

![324383228-4e11d72e-7401-4fa7-9e17-977a8e5c056a](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/143347356/fa367f8e-0e8f-43a6-a73d-529b17148bfa)


# JK FLIPFLOP

![324383595-20ec58e1-ff7d-48ad-896f-325fd15b9978](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/143347356/e6713289-601a-46a1-a0a8-dc17ed630d99)


# T FLIPFLOP


![324383825-f59a93a1-c4a1-4f0d-b8ec-59afae83aaba](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/143347356/b29f33dd-0a06-478c-abb1-8225bd041932)


# D FLIPFLOP

![324383952-061329ff-7ea8-4011-88a0-a346b84b7329](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/143347356/30e9f19c-2b71-4be8-b014-c061f2c5229d)


# COUNTER

![324384065-48d8dfc6-1504-43fc-8178-4baca02ac055](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/143347356/c468ecca-427e-419a-b5c9-d86a62b7b49e)



# VERILOG CODE:

# D Flip Flop
```
module DFlipFlop (D, clk, reset, Q) ;
input D;
input clk;
input reset; 
output reg Q; 
always @ (posedge clk)
begin
    if(reset == 1'b1)
        Q <= 1'b0;
    else
        Q <= D;
end
endmodule
```
# JK Flip Flop
```
module JK_flipflop (q, q_bar, j,k, clk, reset);
  input j,k,clk, reset;
  output reg q;
  output q_bar;
  always@(posedge clk) begin
    if(!reset)        q <= 0;
    else 
  begin
      case({j,k})
        2'b00: q <= q;  
        2'b01: q <= 1'b0; 
        2'b10: q <= 1'b1;
        2'b11: q <= ~q; 
      endcase
    end
  end
  assign q_bar = ~q;
endmodule
```
# SR Flip Flop
```
module SR_flipflop (q, q_bar, s,r, clk, reset);
  input s,r,clk, reset;
  output reg q;
  output q_bar;
  always@(posedge clk) begin 
    if(!reset)        q <= 0;
    else 
  begin
      case({s,r})
        2'b00: q <= q;    
        2'b01: q <= 1'b0; 
        2'b10: q <= 1'b1; 
        2'b11: q <= 1'bx; 
      endcase
    end
  end
  assign q_bar = ~q;
endmodule
```
# T Flip Flop
```
module tff (t,clk, rstn,q);  
 input t,clk, rstn;
 output reg q;
  always @ (posedge clk) begin  
    if (!rstn)  
      q <= 0;  
    else  
        if (t)  
            q <= ~q;  
        else  
            q <= q;  
  end  
endmodule
```
# Ripple Carry Counter
```
module D_FF(q, d, clk, reset);
output q;
input d, clk, reset;
reg q;
always @(posedge reset or negedge clk)
if (reset)
q = 1'b0;
else
q = d;
endmodule
module T_FF(q, clk, reset);
output q;
input clk, reset;
wire d;
D_FF dff0(q, d, clk, reset);
not n1(d, q); 
endmodule
module ripple_carry_counter(q, clk, reset);
output [3:0] q;
input clk, reset;
T_FF tffo(q[0], clk, reset);
T_FF tff1(q[1], q[0], reset);
T_FF tff2(q[2], q[1], reset);
T_FF tff3(q[3], q[2], reset);
endmodule
```
# MOD 10 Counter
```
module counter(
input clk,rst,enable,
output reg [3:0]counter_output
);
always@ (posedge clk)
begin 
if( rst | counter_output==4'b1001)
counter_output <= 4'b0000;
else if(enable)
counter_output <= counter_output + 1;
else
counter_output <= 0;
end
endmodule
```
UP-DOWN COUNTER

VERILOG CODE:
```
module updown_counter(clk,rst,updown,out);
input clk,rst,updown;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1)
out=4'b0000;
else if(updown==1)
out=out+1;
else
out=out-1;
end
endmodule
```

# OUTPUT WAVEFORM:

# D Flip Flop
![327071393-1594f4d7-8e42-43ca-9cc0-f8dbebdd367f](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/143347356/94587e00-7366-4ed5-be22-a702d2940c2b)

<img width="962" alt="327071413-656845cc-29e9-48d0-b2d7-d510d921ee6c" src="https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/143347356/5b53d099-6d50-446a-a12c-b64a5db6a423">


# JK Flip Flop
![327071445-02ef104f-8e85-4ec2-a6ea-2b24dd40eabf](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/143347356/07ce331d-2841-476d-970b-c05fd153d54a)



<img width="962" alt="327071467-7a065d7c-9898-4c7f-88d3-3357386ce2e0" src="https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/143347356/f5d794e8-8a8b-4c4a-b37f-be5979e143b6">




# SR Flip Flop
![327071505-b2267d45-902d-4e3f-9569-e98b50cfee9f](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/143347356/2e17bbfe-13e5-499b-b3ed-ce50875df062)

<img width="962" alt="327071535-bea76a0e-4ef9-48b5-954a-c88ec757408a" src="https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/143347356/f1d63678-58dc-44e5-a44f-156331fbbe2d">


# T Flip Flop

![327071572-e37658b4-49e8-417f-afcb-03c3e1f20b39](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/143347356/27fcb748-5bd0-44e3-b1f0-fb8682ff0fdc)

<img width="962" alt="327071595-6d52d36b-f685-416e-85d6-7faad0c8aee3" src="https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/143347356/b35b971c-5571-4036-bd92-cef7151b03b5">


# MOD-10 Counter

<img width="962" alt="327071620-f3a3b9bc-9645-4ce1-91bf-65237fdd5b93" src="https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/143347356/9b2fb001-7951-45fd-97c6-84e625eb4371">

<img width="962" alt="327071657-01931e66-6c86-4542-86a8-100f296cd0e4" src="https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/143347356/c5a5bf6d-68df-49df-8792-6456f1aa0592">

# Ripple Carry Counter
<img width="962" alt="327071685-21a39d4e-fd2d-43bb-955e-78c6781c53bd" src="https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/143347356/5afc1b43-f253-4349-bb9f-7e0b3c5e0918">


<img width="962" alt="327071711-f01225a9-b09b-4a7e-a9ae-b50cbe80c779" src="https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/143347356/c9a1f290-acd0-4851-a1eb-5f788756539b">


# UP Down Counter
<img width="617" alt="327071740-3988b689-eaa0-4ef2-8a4d-c0c035f5c232" src="https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/143347356/fd0ed067-265b-459f-b8b2-0fbd077fe456">

<img width="962" alt="327071763-5dc92778-9179-41f6-b14d-37740f2cb1c8" src="https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/143347356/618c5718-cd38-446a-a442-79c961b9e512">


# RESULT:
Hence thus given To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using vivado
