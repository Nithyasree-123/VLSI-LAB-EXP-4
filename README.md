# VLSI-LAB-EXP-4
## SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

### AIM: 
 To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Xilinx ISE.

### APPARATUS REQUIRED:

Xilinx 14.7
Spartan6 FPGA

**LOGIC DIAGRAM**

SR FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/77fb7f38-5649-4778-a987-8468df9ea3c3)


JK FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/1510e030-4ddc-42b1-88ce-d00f6f0dc7e6)

T FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/7a020379-efb1-4104-85ee-439d660baa08)


D FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0)


COUNTER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/a1fc5f68-aafb-49a1-93d2-779529f525fa)


  
### PROCEDURE:
STEP:1  Start  the Xilinx navigator, Select and Name the New project.
STEP:2  Select the device family, device, package and speed.       
STEP:3  Select new source in the New Project and select Verilog Module as the Source type.                       
STEP:4  Type the File Name and Click Next and then finish button. Type the code and save it.
STEP:5  Select the Behavioral Simulation in the Source Window and click the check syntax.                       
STEP:6  Click the simulation to simulate the program and  give the inputs and verify the outputs as per the truth table.               
STEP:7  Select the Implementation in the Sources Window and select the required file in the Processes Window.
STEP:8  Select Check Syntax from the Synthesize  XST Process. Double Click in the  FloorplanArea/IO/Logic-Post Synthesis process in the User Constraints process group. UCF(User constraint File) is obtained. 
STEP:9  In the Design Object List Window, enter the pin location for each pin in the Loc column Select save from the File menu.
STEP:10 Double click on the Implement Design and double click on the Generate Programming File to create a bitstream of the design.(.v) file is converted into .bit file here.
STEP:11  On the board, by giving required input, the LEDs starts to glow light, indicating the output.

### VERILOG CODE:
### SR FLIPFLOP:
```
module srff(clk,j,k,rst,q );

input s,r,clk,rst;

output reg q;

always@(posedge clk)

begin

if(rst==1)

q=1'b0;

else

begin

case({s,r})

2'b00: q=q;

2'b01:q=1'b0;

2'b10:q=1'b1;

2'b11:q=1'bx;

endcase

end

end

endmodule
```
### JK FLIPFLOP:
```
module jkff(clk,j,k,rst,q );

input j,k,clk,rst;

output reg q;

always@(posedge clk)

begin

if(rst==1)

q=1'b0;

else

begin

case({j,k})

2'b00: q=q;

2'b01:q=1'b0;

2'b10:q=1'b1;

2'b11:q=~q;

endcase

end

end
```
### T FLIPFLOP:
```
module tff(clk,reset,t,q);

input clk,reset,t;

output reg q;

always @(posedge clk)

begin

if(reset==1)

q=0;

else

begin

if(t==0)

q=q;

else

q=~q;

end

end

endmodule
```
### D FLIPFLOP:
```
module dff(clk,d,rst,q );

input d,clk,rst;

output reg q;

always@(posedge clk)

begin

if(rst==1)

q=1'b0;

else

q=d;

end

endmodule
```

### UPDOWN COUNTER:
```
module updown(clk,rst,up_down,count);

input clk,rst,up_down;

output reg[3:0]count;

always@(posedge clk)

begin

if(rst==1)

count <= 4'b0000;

else if (up_down == 1'b1)

count <= count + 1'b1;

else

count <= count-1'b1;

end

endmodule
```

### MOD 10 COUNTER:
```
module mod(clk,rst,count);

input clk,rst;

output reg[3:0]count;

always @(posedge clk)

begin

if(rst==1 | count==4'b1001)

count <= 4'b0000;

else

count <= count +1;

end

endmodule
```

### RIPPLE COUNTER:
```
module ripplecounter(clk,rst,q);

input clk,rst;

output [3:0]q;

tff tff1(q[0],clk,rst);

tff tff2(q[1],q[0],rst);

tff tff3(q[2],q[1],rst);

tff tff4(q[3],q[2],rst);

endmodule

module tff(q,clk,rst);

input clk,rst;

output q;

wire d;

dff df1(q,d,clk,rst);

not n1(d,q);

endmodule

module dff(q,d,clk,rst);

input d,clk,rst;

output q;

reg q;

always@(posedge clk or posedge rst)

begin

if(rst)

q=1'b10;

else

q=d;

end

endmodule
```

## OUTPUT WAVEFORM:
### SR flipflop:

<img width="1007" alt="320183966-e21bd2e2-b69f-424b-9da2-ced2f8da8622" src="https://github.com/Nithyasree-123/VLSI-LAB-EXP-4/assets/164908713/9b66f2aa-ec10-4d82-88c1-ff8be0872b69">

### JK flipflop:

<img width="1012" alt="320184046-d989b3ab-a0fb-4bb9-969d-0817eff565eb" src="https://github.com/Nithyasree-123/VLSI-LAB-EXP-4/assets/164908713/a2ad12e4-ccf2-42de-a6d6-1e56fb1c800e">

### T flipflop:
<img width="942" alt="320184083-bf2966e2-f9d8-40cd-ad7d-289702a75078" src="https://github.com/Nithyasree-123/VLSI-LAB-EXP-4/assets/164908713/e0c26837-131a-43bc-bc5f-2cf3bd15d60c">

### D flipflop:

<img width="943" alt="320184078-c9027cd8-06a8-4647-a4b2-fd48536a5e04" src="https://github.com/Nithyasree-123/VLSI-LAB-EXP-4/assets/164908713/24e68e11-c062-498e-9bdf-ff5f78888d96">

### Updown counter:
<img width="1089" alt="320184128-22f1ecee-4349-4d37-bb84-4310ec89e00a" src="https://github.com/Nithyasree-123/VLSI-LAB-EXP-4/assets/164908713/529d8c41-6605-4798-87ae-2052720a2a55">

### Mod 10 counter:
<img width="1017" alt="320184154-56d42f95-1ad0-4396-97f3-5fee5ec0d539" src="https://github.com/Nithyasree-123/VLSI-LAB-EXP-4/assets/164908713/defb0e11-10f7-40bd-b5e9-46e6d511c121">

### Ripple counter:
![320185653-f37d8d04-cbc1-44b2-8704-ba28fe340d2f](https://github.com/Nithyasree-123/VLSI-LAB-EXP-4/assets/164908713/1de1deb8-5c88-43d0-90f9-ff812a36034c)

## RESULT:

Thus,the simulation and synthesis of SR,JK,T,D flipflops,counters by using vivado has been successfully excecuted and verified.
