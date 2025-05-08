# 4Bit-Up-Down-Asynchronous-Reset-Counter-Synthesis

## Aim:

Synthesize 4Bit-Up-Down-Asynchronous-Reset-Counter design using Constraints and analyse reports, Timing, area and Power.

## Tool Required:

Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim)

Synthesis: Genus

### Step 1: Getting Started

Synthesis requires three files as follows,

◦ Liberty Files (.lib)
 ![WhatsApp Image 2025-05-08 at 10 15 29_3ba4456d](https://github.com/user-attachments/assets/7c348360-ad4c-4d3a-bfce-2d63ae931dc1)

◦ Verilog/VHDL Files (.v or .vhdl or .vhd)

### TESTBENCH
```
timescale 1ns/1ps
module up_down_counter_tb();

reg clk;
reg reset;
reg up down;
reg enable;
wire [3:0] count;

up_down_counter uut (
    .clk(clk),
    .reset(reset),
    .up_down(up_down),
    .enable(enable),
    .count(count)
};

initial begin
   clk = 0;
   forever #5 clk = clk;
end

initial begin
   reset 1;
   up down 1;
   enable=0;
   #20 reset 0;
   #10 enable = 1;
   #200;

   up down=0;
   #200;

enable=0

#50;

reset 1;

#20 reset =0;

#50;

$finish;

end

initial begin

$monitor("Time: %t, Reset: %b Up/Down: b, Enable: Sb, Count: b",

Stime, reset, up down, enable, count);

end

endmodule
```

### DESIGN
```
imescale 1ns/1ps module up_down_counter(input wire clk,
input wire reset,
input wire up_down,
input wire enable,
output reg [3:0] count);

    always (posedge clk or posedge reset) begin
       if (reset)
       begin
          count <= 4'60000;
       end

       else if (enable)
       begin
         if (up_down)
         begin
           count <= count + 1'b1;
         end

         else begin
            count <= count 1'b1;
         end
       end
     end

endmodule
```

◦ SDC (Synopsis Design Constraint) File (.sdc)
![WhatsApp Image 2025-05-02 at 11 03 41_856d7899](https://github.com/user-attachments/assets/78cf3bc2-d3b1-48f7-a952-152408a99cb0)


 ### Step 2 : Creating an SDC File

•	In your terminal type “gedit input_constraints.sdc” to create an SDC File if you do not have one.
![Screenshot 2025-05-08 104722](https://github.com/user-attachments/assets/42538c18-c013-4ae1-b751-94c0cd1a44b4)



•	The SDC File must contain the following commands;

create_clock -name clk -period 2 -waveform {0 1} [get_ports "clk"]

set_clock_transition -rise 0.1 [get_clocks "clk"]

set_clock_transition -fall 0.1 [get_clocks "clk"]

set_clock_uncertainty 0.01 [get_ports "clk"]

set_input_delay -max 0.8 [get_ports "rst"] -clock [get_clocks "clk"]

set_output_delay -max 0.8 [get_ports "count"] -clock [get_clocks "clk"]

i→ Creates a Clock named “clk” with Time Period 2ns and On Time from t=0 to t=1.

ii, iii → Sets Clock Rise and Fall time to 100ps.

iv → Sets Clock Uncertainty to 10ps.

v, vi → Sets the maximum limit for I/O port delay to 1ps.

### Step 3 : Performing Synthesis

The Liberty files are present in the library path,

• The Available technology nodes are 180nm ,90nm and 45nm.

• In the terminal, initialise the tools with the following commands if a new terminal is being
used.

◦ csh

◦ source /cadence/install/cshrc

• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.
![Screenshot 2025-05-08 095741](https://github.com/user-attachments/assets/4d4f5f76-893c-4d76-a7c9-153af5d3380f)


• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist.

#### Synthesis RTL Schematic :

#### Area report:
![Screenshot 2025-05-08 095811](https://github.com/user-attachments/assets/947673c9-3c18-4144-bdeb-62a535a38aa5)


#### Power Report:
![Screenshot 2025-05-08 095837](https://github.com/user-attachments/assets/335c63cd-046d-4b65-8aec-3aeefc70e63d)


#### Timing Report: 
![Screenshot 2025-05-08 095853](https://github.com/user-attachments/assets/51bf3c04-53db-4b62-83d5-75058d286d93)


#### Result: 

The generic netlist has been created, and area, power, and timing reports have been tabulated and generated using Genus.
![WhatsApp Image 2025-05-02 at 11 47 16_2f731f3b](https://github.com/user-attachments/assets/aaa9528b-f5a0-4844-b48a-b062924254bd)






