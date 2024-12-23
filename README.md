# SoC-Design-and-Planning
<br>
Welcome to the OpenLane workshop! In this workshop, we will delve into the process of designing an Application Specific Integrated Circuit (ASIC) from the Register Transfer Level (RTL) to the Graphical Data System (GDS) file using the OpenLane ASIC flow. The flow is composed of several key steps, starting with an RTL file and culminating in a GDS file.
## Lessons Learned

Understanding the RTL to GDS Flow:

1. Grasped the end-to-end process of converting a high-level hardware description to a physical ASIC layout.
Recognized the importance of each step in the flow, from synthesis to sign-off.

2. Synthesis:

Learned how RTL is converted to a gate-level netlist using standard cell libraries.
Identified the different views of cells (Liberty, HDL, SPICE, Layout).

3. Floor and Power Planning:
Understood the significance of floor planning in chip partitioning and I/O pad placement.

## Section 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK (14/03/2024 - 15/03/2024)

### Theory

<details>
  <summary>
Expand or Collapse
  </summary>

#### Package

*In any embedded board we encounter, what we typically refer to as the "chip" is actually the PACKAGE of the chip—a protective layer or casing that encloses the actual chip. The actual manufactured chip is usually located at the center of this package. Connections from the package to the chip are established through the WIRE BOND method, which is essentially a basic wired connection.
![image](https://github.com/user-attachments/assets/14fcd3c7-68c1-45f6-b069-fed347179d30)
![Screenshot 2024-12-12 163552](https://github.com/user-attachments/assets/2908c18e-8596-48f3-83b5-ddd142da7279)
![Screenshot 2024-12-23 131240](https://github.com/user-attachments/assets/a82e54f6-a402-499c-966e-5fbd336a5853)

#### Chip

* Looking inside the chip, we can see that all signals are sent through ***PADS*** from the outside world to the chip and vice versa. All of the chip's digital logic is located in the ***CORE*** region, which is enclosed by the pads. The ***DIE***, the fundamental manufacturing unit for semiconductor chips, is composed of both the core and pads.
![image](https://github.com/user-attachments/assets/806ed0a3-c433-4a79-932b-f997248e0e72)

* ***FOUNDRY***

While repeating digital logic blocks are known as ***MACROS***, semiconductor chips are made at ***FOUNDRY***, where ***FOUNDRY IP's*** are intellectual properties based on a particular foundry and require a certain amount of intelligence to generate.
![Screenshot 2024-12-23 133158](https://github.com/user-attachments/assets/e5939f3c-bfc5-4292-846c-6d1523b179f6)

####ISA (Intruction Set Architecture)

* A C program which has to be run on a specific hardware layout which is the interior of a chip in your laptop, there is certain flow to be followed.
* Initially, this particular C program is compiled in it's assembly language program which is nothing but ***RISC-V ISA (Reduced Instruction Set Compting - V Intruction Set Architecture)***.
* Following this, the assembly language program is then converted to machine language program which is the binary language logic 0 and 1 which is understood by the hardware of the computer.
* Directly after this, we've to implement this RISC-V specification using some ***RTL (a Hardware Description Language)***. Finally, from the RTL to ***Layout*** it is a standard PnR or RTL to GDSII flow.

![Screenshot 2024-12-23 133324](https://github.com/user-attachments/assets/1567d7ae-e05a-43ab-8f4c-1b23afaa28e9)

* A number of procedures must be followed in order for an application program to run on hardware. First, the application program is converted to binary language by entering a block known as system software. The OS (Operating System), compiler, and assembler are the three main layers or components of system software. The OS initially produces small functions in the C, C++, VB, or Java languages, which are then translated into instructions by the appropriate compiler. The syntax of these instructions differs depending on the hardware architecture that the system is built on. The assembler's next task is to take these instructions and translate them into their binary code, which is essentially referred to as a  machine language program. Finally, this binary language is fed to the hardware and it understands the specific functions it has to perform based on the binary code it receives.

-  Operating System (OS): In addition to general tasks like handling input/output operations, memory allocation, and low-level system functions, the OS translates application software into corresponding code in languages such as C, C++, or Java.

   - Compiler: The compiler takes the code produced by the OS and converts it into an instruction set (e.g., .exe files). These instructions are tailored to the specific type of hardware being used.

   - Assembler: The assembler then converts these executable files into binary language, which the hardware can understand and execute to perform the desired operations.

![Screenshot 2024-12-23 133509](https://github.com/user-attachments/assets/caafdaad-caf8-457f-9a1d-2052f33d21be)

##  OpenLane: Introduction to Components of Open-Source Digital ASIC Design

To design an open-source digital ASIC, several key components are required:


- RTL Designs
- EDA Tools
- PDK Data

![Screenshot 2024-12-23 133846](https://github.com/user-attachments/assets/bbea54ba-e2bd-412c-9c7e-83b18d19229c)

What are RTL Designs?

RTL (Register-Transfer-Level) design is a critical phase in the VLSI design flow, focused on creating electronic circuits using integrated circuits (ICs). It specifies a digital circuit by describing the flow of digital signals between hardware registers and the logical operations performed on these signals.
<br>
What are EDA Tools?

EDA (Electronic Design Automation) tools are software applications used to design and verify the functionality of integrated circuits (ICs). They ensure that the IC meets the required performance and density specifications.
<br>
What is PDK Data?
PDK (Process Design Kit) is a set of files used to model a fabrication process for EDA tools during IC design. This kit includes:
  -  Process Design Rules: DRC (Design Rule Check), LVS (Layout Versus Schematic), PEX (Parasitic Extraction)
 Device Models
Digital Standard Cell Libraries

 I/O Libraries
<br>
## Simplified RTL to GDS Flow

The simplified RTL to GDS flow begins with an RTL file and, through a series of stages, produces a GDS file, which can be sent to a foundry for fabrication. The steps in the RTL to GDS flow include:

![Screenshot 2024-12-23 170458](https://github.com/user-attachments/assets/d22f4f74-2c3b-44a0-8a4e-8d6ffdc1934c)

 Synthesis:
        The RTL file is converted into a circuit using components from the Standard Cell Library.
        Standard Cells in the library have a regular layout with the same height but different widths.
        Each cell has various models based on electrical, HDL, Spice, and layout (abstract and detailed) parameters.

![Screenshot 2024-12-23 170900](https://github.com/user-attachments/assets/628e73ec-0002-461c-a9ef-0435fb16bae6)


Floor Planning & Power Planning:
        Floor Planning: Determines the position of components on the chip to minimize area, including the placement of I/O pins, ports, and pads.
        Power Planning: Designs the power supply network (VDD and GND) using power rings, power straps, and power pads, typically on the top metal layers for minimal resistance and delay.

![Screenshot 2024-12-23 170940](https://github.com/user-attachments/assets/1b567952-6f7d-43c0-9bed-eba8341138b4)

Placement:
        Components are placed within the designated areas from the floor planning stage.
        Standard Cells required in the design are also placed within their cell boundaries.
        Placement is performed in two stages: Global Placement (where cells may overlap) and Detailed Placement (where cells are optimally placed following placement rules).

![Screenshot 2024-12-23 171028](https://github.com/user-attachments/assets/d25884ff-c87b-488c-8841-8d5f0caeae03)



 CTS (Clock Tree Synthesis):
        Clock routing is performed before signal routing to address clock skew, the difference in time for the clock to reach various destinations.
        Symmetric Tree Structures (H-tree, I-tree, X-tree) are used to eliminate clock skew.

![Screenshot 2024-12-23 171035](https://github.com/user-attachments/assets/8a6f256a-b330-43e4-be7f-f42e6feb63d9)

Routing:
        After clock routing, signal routing is performed using the remaining metal layers.
        Routing is divided into Global Routing (generates a routing guide based on PDK instructions) and Detailed Routing (actual routing according to the guide).

![Screenshot 2024-12-23 171046](https://github.com/user-attachments/assets/761e3cad-ccf8-43f1-90ad-21a63e7ca71a)


 Sign-off:
        Once routing is completed, the chip undergoes various checks during the sign-off stage:
            Physical Verification Checks: Design Rule Check (DRC) and Layout vs. Schematic (LVS). DRC verifies design rule compliance, while LVS ensures functional correctness against the gate-level netlist.
            Timing Checks: Static Timing Analysis (STA) checks the design for timing violations.

</details>

### Implementation

Section 1 tasks:- 

1. Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.

2. Calculate the flop ratio.

```math
Flop\ Ratio = \frac{Number\ of\ D\ Flip\ Flops}{Total\ Number\ of\ Cells}
```
```math
Percentage\ of\ DFF's = Flop\ Ratio * 100
```
# 1. Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.

Commands to invoke the OpenLANE flow and perform synthesis

```bash
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker
```
```tcl
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

# Exit from OpenLANE flow
exit

# Exit from OpenLANE flow docker sub-system
exit
```

