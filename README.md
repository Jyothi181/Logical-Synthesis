# Logical-Synthesis
Logical Synthesis of Arithmetic Logic Unit

# Introduction
 This repository demonstrates the logical synthesis of Arithmetic Logic Unit by using synopsys tool.

Logical synthesis refers to the process of converting a high-level abstract description of a digital circuit, typically written in a hardware description language (HDL) such as verilog or VHDL, into a gate level netlist that represents the circuit as interconnected logic gates (AND, OR, NOT, flipflops) and other digital components. In other words, it is the process of converting RTL netlist to a gate level netlist. Logical synthesis is important as it tanslates the high-abstraction specifications into hardware designs and optimizes the design in terms of area, power and performance. It also provides a systematic approach for designing complex integrated cirucits efficiently. Once the HDL is converted into synthesis netlist, it provides the detailed interconnection of logic gates which needs to be implemtented on the layout of the design.

# Terminologies

- **Netlist:** It is a textual or graphical representation of the circuit that describes how the components of the circuit are interconnected.

- **RTL Netlist:** This represents the design at the Register Transfer Level(RTL), often generated from the hardware description languages(Verilog or VHDL). It defines the logical behaviour of the circuit.

- **Gate Level Netlist:** This is obtained after synthesis. This netlist is interconnection of logic gates in the circuit. 

- **dc_shell - Design compiler:** Tool translates, maps and optimizes the schematic into a gate level netlist by embedding technology to the schematic.

- **Target Library :** Contains technology-specific cells (e.g., gates, flip-flops) with physical and electrical parameters.

- **Link Library :** Contains logical cell descriptions (e.g., AND, OR, NOT gates) without physical characteristics.

# Requirements
- **Technology:** 32nm
- **Cells Used:** HVT
- **Process:** Slow-Slow
- **Voltage:** 0.95v
- **Temperature:** 125 degrees Celsius
- **Software shell for synthesis:** dc_shell
- **Inputs:** RTL netlist, SDC file, library/liberty file
- **Files in inputs directory ->** alu.v; alu.sdc; saed32hvt_ss0p95v125c.lib
- **Shell ->** csh or tcsh
- **Path ->** /home/tools/synopsys/cshrc_synopsys
- The file cshrc_synopsys is used to invoke the Synopsys tool. It contains licence and tool executable paths.
- The maximum delay in sdc is set to 1.5

# Steps in Logical Synthesis

Load the input files into tool
  
1. Load the liberty or library file using target and link library
   
     `set target_library ./inputs/saed32hvt_ss0p95v125c.db`
   
     `set link_library ./inputs/saed32hvt_ss0p95v125c.db`
   
3. Loading RTL file includes two steps - analyze and elaborate
   
   - Analyze RTL file by using analyze command and automatically read the RTL to tool by using autoread.

    `analyze -format verilog ./inputs/alu.v -autoread -top ALU`

   - Then elaborate the design to resolve the hierarchies. `elaborate ALU`

5. Read the SDC file by using source command.

  `source ./inputs/alu.sdc`

5. Perform synthesis to map the cells to the given library by using compile_ultra command

   `compile_ultra -no_autoungroup`
   
7. To check the synthesized netlist for issues - `check_design`

8. The synthesized netlist can be written into a text file -> `write_file -format verilog -hierarchy -output ./outputs/alu.vg`

# Reports

The area, timing and power information of cells can be obtained.

report_area



report_timing

report_power








