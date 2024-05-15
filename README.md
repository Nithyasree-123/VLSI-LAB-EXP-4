# VLSI-LAB-EXP-4
## SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

### AIM: 
To simulate and synthesis SR, JK, T, D - FLIPFLOPS, COUNTERS design using vivado.

### APPARATUS REQUIRED:

vivado 2023.2

### PROCEDURE:

STEP:1 Start the vivado software, Select and Name the New project.

STEP:2 Select the device family, device, package and speed.

STEP:3 Select new source in the New Project and select Verilog Module as the Source type.

STEP:4 Type the File Name and module name and Click Next and then finish button. Type the code and save it.

STEP:5 Select the run simulation and then run Behavioral Simulation in the Source Window and click the check syntax.

STEP:6 Click the simulation to simulate the program and give the inputs and verify the outputs as per the truth table.

STEP:7 compare the output with truth table.


## LOGIC DIAGRAM:

## SR FLIPFLOP:

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/77fb7f38-5649-4778-a987-8468df9ea3c3)


### VERILOG CODE:

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

### OUTPUT:

<img width="1007" alt="320183966-e21bd2e2-b69f-424b-9da2-ced2f8da8622" src="https://github.com/Nithyasree-123/VLSI-LAB-EXP-4/assets/164908713/2b4979d6-b46d-4498-a32b-84b1bfab9665">

## JK FLIPFLOP:

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/1510e030-4ddc-42b1-88ce-d00f6f0dc7e6)

### VERILOG CODE:

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

endmodule

### OUTPUT:

<img width="1012" alt="320184046-d989b3ab-a0fb-4bb9-969d-0817eff565eb" src="https://github.com/Nithyasree-123/VLSI-LAB-EXP-4/assets/164908713/ca8cfa60-36dc-42b4-90c8-9ca0fe12d505">


## T FLIPFLOP:

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/7a020379-efb1-4104-85ee-439d660baa08)

### VERILOG CODE:

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

### OUTPUT:

<img width="942" alt="320184083-bf2966e2-f9d8-40cd-ad7d-289702a75078" src="https://github.com/Nithyasree-123/VLSI-LAB-EXP-4/assets/164908713/c47d1144-9914-439a-931c-1ed94c5ed17a">

## D FLIPFLOP:

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0)

### VERILOG CODE:

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

### OUTPUT:

<img width="943" alt="320184078-c9027cd8-06a8-4647-a4b2-fd48536a5e04" src="https://github.com/Nithyasree-123/VLSI-LAB-EXP-4/assets/164908713/c691cde8-da11-4378-bb62-d2efb2dfe688">


## COUNTER:

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/a1fc5f68-aafb-49a1-93d2-779529f525fa)

## UPDOWN COUNTER:

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

### OUTPUT:

<img width="1089" alt="320184128-22f1ecee-4349-4d37-bb84-4310ec89e00a" src="https://github.com/Nithyasree-123/VLSI-LAB-EXP-4/assets/164908713/e5ba5169-1631-45d2-8847-14403760f0d4">

## MOD 10 COUNTER:

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

### OUTPUT:

<img width="1017" alt="320184154-56d42f95-1ad0-4396-97f3-5fee5ec0d539" src="https://github.com/Nithyasree-123/VLSI-LAB-EXP-4/assets/164908713/ec1a38fa-b947-4967-9ce5-8dcee4250a53">

## RIPPLE COUNTER:

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

### OUTPUT:

![320185653-f37d8d04-cbc1-44b2-8704-ba28fe340d2f](https://github.com/Nithyasree-123/VLSI-LAB-EXP-4/assets/164908713/cf2fa2c7-aae2-43d3-ac47-cf41f25c3453)


## RESULT:

Thus,the simulation and synthesis of SR,JK,T,D flipflops,counters by using vivado has been successfully excecuted and verified.
