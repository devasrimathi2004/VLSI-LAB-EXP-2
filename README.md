SIMULATION AND IMPLEMENTATION OF  COMBINATIONAL LOGIC CIRCUITS

AIM: 
 To simulate and synthesis ENCODER, DECODER, MULTIPLEXER, DEMULTIPLEXER, MAGNITUDE COMPARATOR using Xilinx ISE.

APPARATUS REQUIRED:
Xilinx 14.7
Spartan6 FPGA

**LOGIC DIAGRAM**

ENCODER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/3cd1f95e-7531-4cad-9154-fdd397ac439e)


DECODER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/45a5e6cf-bbe0-4fd5-ac84-e5ad4477483b)


MULTIPLEXER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/427f75b2-8e67-44b9-ac45-a66651787436)


DEMULTIPLEXER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/1c45a7fc-08ac-4f76-87f2-c084e7150557)


MAGNITUDE COMPARATOR

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/b2fe7a05-6bf7-4dcb-8f5d-28abbf7ea8c2)


  
PROCEDURE:
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

VERILOG CODE

ENCODER:
~~~
module encoder8to3(a0,a1,a2,d0,d1,d2,d3,d4,d5,d6,d7);
input d0,d1,d2,d3,d4,d5,d6,d7;
output a0,a1,a2;
or g1(a0,d1,d3,d5,d7);
or g2 (a1,d2,d3,d6,d7);
or g3(a2,d4,d5,d6,d7);
endmodule
~~~

OUTPUT:

![image](https://github.com/devasrimathi2004/VLSI-LAB-EXP-2/assets/166363441/96a7afb1-59d1-4924-9e32-386663a4a186)
![image](https://github.com/devasrimathi2004/VLSI-LAB-EXP-2/assets/166363441/62689c32-605f-4024-bf9a-4379ccd53f91)


DECODER:
~~~
module decoder_struct(
   input [2:0] a,
  output [7:0] d
   );
wire x,y,z;
not g1(z,a[0]);
not g2(y,a[1]);
not g3(x,a[2]);
and g4(d[0],x,y,z);
and g5(d[1],x,y,a[0]);
and g6(d[2],x,a[1],z);
and g7(d[3],x,a[1],a[0]);
and g8(d[4],a[2],y,z);
and g9(d[5],a[2],y,a[0]);
and g10(d[6],a[2],a[1],z);
and g11(d[7],a[2],a[1],a[0]);
endmodule
~~~

OUTPUT:

![image](https://github.com/devasrimathi2004/VLSI-LAB-EXP-2/assets/166363441/f5ce91e5-56a8-4084-bd3b-8496f2739372)
![image](https://github.com/devasrimathi2004/VLSI-LAB-EXP-2/assets/166363441/d3472584-a110-4255-b1e3-a7c987a578fe)


DEMULTIPLEXER:
~~~
module demultiplexer1to8(y,s,a);
output reg[7:0]y;
input[2:0]s;
input a;

always@(*)
begin 
y=0;
case(s)
3'd0:y[0]=a;
3'd1:y[1]=a;
3'd2:y[2]=a;
3'd3:y[3]=a;
3'd4:y[4]=a;
3'd5:y[5]=a;
3'd6:y[6]=a;
3'd7:y[7]=a;
endcase
end
endmodule
~~~

OUTPUT:

![image](https://github.com/devasrimathi2004/VLSI-LAB-EXP-2/assets/166363441/e8a9eb8c-7ab5-4ebd-b9ac-24b256f4427c)
![image](https://github.com/devasrimathi2004/VLSI-LAB-EXP-2/assets/166363441/f79a3de3-0d1b-44f2-a6b9-109e834d77e1)


MAGNITUDECOMPARATOR:
~~~
module comparator(a,b,eq,It,gt);
input[3:0]a,b;
output reg eq,It,gt;
always@(a,b)
begin
if(a==b)
begin
eq=1'b1;
It=1'b0;
gt=1'b0;
end 
else if(a>b)
begin
eq=1'b0;
It=1'b0;
gt=1'b1;
end
else
begin
eq=1'b0;
It=1'b1;
gt=1'b0;
end
end 
endmodule
~~~

OUTPUT:

![image](https://github.com/devasrimathi2004/VLSI-LAB-EXP-2/assets/166363441/d35b901d-20e6-43c8-a8c9-06885ffc8b85)
![image](https://github.com/devasrimathi2004/VLSI-LAB-EXP-2/assets/166363441/f0f4f178-63cf-49f5-8d9f-5b5f2e74a817)


MULTIPLEXER:
~~~
module mux_8to1(in,sel,out);
input [7:0] in; input [2:0] sel;
output reg out;
always @(*)
begin 
case(sel)
3'b000: out = in[0];
3'b001: out = in[1];
3'b010: out = in[2];
3'b011: out = in[3];
3'b100: out = in[4];
3'b101: out = in[5];
3'b110: out = in[6];
3'b111: out = in[7];
default:out = 1'bx;
endcase
end
endmodule
~~~

OUTPUT:

![image](https://github.com/devasrimathi2004/VLSI-LAB-EXP-2/assets/166363441/010cd361-49ab-43dd-8066-4ebae853d161)
![image](https://github.com/devasrimathi2004/VLSI-LAB-EXP-2/assets/166363441/089174e5-2441-4306-8b63-357b2c9cc835)


RESULT:Hence ENCODER, DECODER, MULTIPLEXER, DEMULTIPLEXER, MAGNITUDE COMPARATOR are simulated and sysnthesised using vivado 2023.1.







