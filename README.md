# SoC-Design-and-Planning
<br>
Welcome to the OpenLane workshop! In this workshop, we will delve into the process of designing an Application Specific Integrated Circuit (ASIC) from the Register Transfer Level (RTL) to the Graphical Data System (GDS) file using the OpenLane ASIC flow. The flow is composed of several key steps, starting with an RTL file and culminating in a GDS file.
<br>

## Lessons Learned

Understanding the RTL to GDS Flow:

1. Grasped the end-to-end process of converting a high-level hardware description to a physical ASIC layout.
Recognized the importance of each step in the flow, from synthesis to sign-off.

2. Synthesis Learned how RTL is converted to a gate-level netlist using standard cell libraries.
Identified the different views of cells (Liberty, HDL, SPICE, Layout).

3. Floor and Power Planning Understood the significance of floor planning in chip partitioning and I/O pad placement.

## Section 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK Day 1

### Theory

<details>
  <summary>
Expand or Collapse
  </summary>

#### Package

*In any embedded board we encounter, what we typically refer to as the "chip" is actually the PACKAGE of the chip—a protective layer or casing that encloses the actual chip. The actual manufactured chip is usually located at the center of this package. Connections from the package to the chip are established through the WIRE BOND method, which is essentially a basic wired connection.
<br>
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

1.  Understanding the use of various linux commands

  -  pwd : It displays the present working directory and its path.

   - cd : Using this command we can move in both ways in the directory tree.

- ls : It lists all the sub-directories and files present in the current directory.

 - mkdir : Using this command, we can create a new directory.

  -  rmdir : Using his command, we can delete an existing directory.

 -   rm : This command is used to delete the files.

  -  help : using this command we can know the working of any command.

   - clear : This command clears the terminal.



  Key Files and Directories:

    libs.ref: Houses the design libraries, including standard cells, IO cells, and other related files.
        lef: Library Exchange Format files describing the cell layouts.
        lib: Liberty files for timing and power analysis.
        gds: GDSII files containing the graphical layout of the cells.
        verilog: Verilog models of the cells.

    libs.tech: Contains technology files tailored for specific EDA tools.
        magic: Magic technology files.
        klayout: KLayout technology files and layer properties.
        ngspice: SPICE models for circuit simulation.
        openroad: Files for OpenROAD flow.
        drc: Design Rule Check files.
        lvs: Layout Versus Schematic check files.
        pex: Parasitic Extraction files.

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
docker
```
```tcl
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages 
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design 
prep -design picorv32a

# Now that the design is prepped and ready, we can run synthesis using the command
run_synthesis
```
Once the preparation is complete, a new directory with the current date will be generated within the “runs” folder. Inside this directory, all the necessary subdirectories for storing results, reports, and other relevant data will be created.
The preparation step involves the following actions for the picorv32a design within the openLANE flow:

**Directory Structure Setup:**

A new directory structure is created to organize the design files.
This structure includes subdirectories for different components (e.g., results, reports).

- LEF Merging:
The technology LEF (.tlef) and cell LEF (.lef) files are merged into a unified format.The technology LEF contains layer information (such as metal layers), while the cell LEF contains cell informations.

- Design Placement:
All design-related files are placed under the designs directory.

This ensures that the necessary files are organized and accessible during subsequent steps.

 `config.tcl`	  contains the configurations used by openLANE                     
 `src`  contains verilog files and constraints file

Screenshots of running the commands

![Screenshot 2024-12-14 152420](https://github.com/user-attachments/assets/5f4206bb-6126-4bf1-b60a-d96182ca7287)
<br>
![Screenshot 2024-12-14 154234](https://github.com/user-attachments/assets/4d1c7608-a57d-4c0a-8583-be9b35a2b638)

#### 2. Calculate the flop ratio.

Screenshots of synthesis statistics with required values

![Screenshot 2024-12-14 160609](https://github.com/user-attachments/assets/5c0eec3e-e613-462a-8491-5e6d12dd2563)
![Screenshot 2024-12-14 160621](https://github.com/user-attachments/assets/79016848-a30a-48f8-87eb-ab05aed833ad)

Calculation of Flop Ratio and DFF % from synthesis statistics report file

```math
Flop\ Ratio = \frac{1613}{14876} = 0.108429685
```
```math
Percentage\ of\ DFF's = 0.108429685 * 100 = 10.84296854\ \%
```
# Day 2

## Good FloorPlan Vs Bad FloorPlan and Introduction to Library Cells
Chip FloorPlanning Considerations

![Screenshot 2024-12-23 182719](https://github.com/user-attachments/assets/8c329dde-649e-4d44-b4ea-4f59807455af)

Utilization Factor and Aspect Ratio
In order to find out the Utilization Factor and Aspect Ratio, first we need to know how to define height and width of core and die areas.

- Core is an area in a chip which is used to place all the logic cells and components in a chip. It is the place where logic lies in a chip.

- Die is an area that encircles the core area and used for placing I/O related components.


The height and width of core area will be decided by the netlist of the design. It will be based on the no.of components required in order to execute the logic and the height and width of the die area will be dependent on the core area height and width.


![Screenshot 2024-12-23 182729](https://github.com/user-attachments/assets/bfe35d3a-bde0-429a-b8d3-01e29732af70)

For example, lets consider a netlist that is having two logic gates and two flipflops each having area of 1 sq.unit. The netlist contains 4 elements and the minimum total area required for the core area will be 4 sq.units.

![Screenshot 2024-12-23 182737](https://github.com/user-attachments/assets/62e5dfca-573e-4dee-a276-7aefd4544b87)

![Screenshot 2024-12-23 182743](https://github.com/user-attachments/assets/b10af20a-cb19-47fa-8866-26fca8b8a966)

*Utilization Factor :*  Utilization Factor is defined as "The ratio of the core area occupied by the netlist to the total core area".For a good FloorPlan, The Utilization Factor should never be '1' because when the Utilization factor becomes '1' , there will be no place for adding additional logic if needed and it will be considered as a bad FloorPlan.


`Utilization Factor = (Area occupied by netlist / Total core area)`

*Aspect Ratio :*  Aspect Ratio is defined as "The ratio of Height of the core to the width of the core". If the Aspect ratio is '1' , then the core is said to be in a square shape and other than '1' the core will be a rectangle.

`Aspect Ratio = (Height of the core / Width of the core)`

![Screenshot 2024-12-23 182748](https://github.com/user-attachments/assets/1136065b-0b77-41cb-9b98-da09f2801b0a)

In this case, when calculated

- Utilization factor = (4 squnits)/(4 squnits) = 1

- Aspect Ratio = (2 units)/(2 units) = 1 //The core is in a square shape.

In this case, when calculated


![Screenshot 2024-12-23 182752](https://github.com/user-attachments/assets/3763557e-5995-43a1-bdaf-c18ce41e7cee)

- Utilization factor = (4 squnits)/(8 squnits) = 0.5

- Aspect Ratio = (2 units)/(4 units) = 0.5 //The core is in a rectangular shape.
### Implementation

Section 2 tasks:- 
1. Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.
2. Calculate the die area in microns from the values in floorplan def.
3. Load generated floorplan def in magic tool and explore the floorplan.
4. Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.
5. Load generated placement def in magic tool and explore the placement.

```math
Area\ of\ die\ in\ microns = Die\ width\ in\ microns * Die\ height\ in\ microns
```
#### 1. Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.

Commands to invoke the OpenLANE flow and perform floorplan

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

# Now we can run floorplan
run_floorplan
```

Screenshot of floorplan run


![Screenshot 2024-12-16 194830](https://github.com/user-attachments/assets/8ced04f7-6f24-4c0a-acf4-c2fed82c6318)
![Screenshot 2024-12-16 194840](https://github.com/user-attachments/assets/7b42f1de-eeee-45eb-8b9a-d20158cfd06e)

### 2. Calculate the die area in microns from the values in floorplan def.

Screenshot of contents of floorplan

![Screenshot 2024-12-16 212502](https://github.com/user-attachments/assets/adeba3e5-4217-41fd-a518-b554cbb0c895)

According to floorplan def
```math
1000\ Unit\ Distance = 1\ Micron
```
```math
Die\ width\ in\ unit\ distance = 660685 - 0 = 660685
```
```math
Die\ height\ in\ unit\ distance = 671405 - 0 = 671405
```
```math
Distance\ in\ microns = \frac{Value\ in\ Unit\ Distance}{1000}
```
```math
Die\ width\ in\ microns = \frac{660685}{1000} = 660.685\ Microns
```
```math
Die\ height\ in\ microns = \frac{671405}{1000} = 671.405\ Microns
```
```math
Area\ of\ die\ in\ microns = 660.685 * 671.405 = 443587.212425\ Square\ Microns
```

#### 3. Loading generated floorplan def in magic tool and explore the floorplan.

Commands to load floorplan def in magic in another terminal

```bash
# Change directory to path containing generated floorplan def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/16-12_14-12/results/floorplan/

# Command to load the floorplan def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```

## Design Alignment Instructions

### Centering the Design:
1. Press `S` to select the entire design.
2. Press `V` to vertically align it to the middle of the screen.

### Zooming In on a Specific Area:
1. Left-click and drag to select the desired region.
2. Right-click to bring up the context menu.
3. Press `Z` to zoom in on the selected area.

### Getting Details of a Cell:
1. Move your cursor to the cell of interest.
2. Press `S` to select the cell.
3. In the `tkcon` window, enter the command "what"  to display cell details.

Screenshots of floorplan def in magic

![Screenshot 2024-12-16 220052](https://github.com/user-attachments/assets/bc849ffd-0697-4119-9e70-f6a43a33aa55)
![Screenshot 2024-12-16 220130](https://github.com/user-attachments/assets/6a4d7d42-4e79-499a-850a-2b2e67e9d7b6)

Port layer as set through config.tcl

![Screenshot 2024-12-16 221902](https://github.com/user-attachments/assets/81d3dce4-ab8a-49b5-9b5b-73e0efe23389)

![Screenshot 2024-12-16 222138](https://github.com/user-attachments/assets/5bbf0ac2-b589-40e5-b6dc-56c9db0fbcdf)

#### 4. Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.

Placement plays a crucial role in VLSI (Very Large Scale Integration) design. It involves determining the physical locations of standard cells or logic elements within a chip or block. Let's break it down:

1. **Global Placement:**
   - Global placement assigns general locations to movable objects (cells).
   - Some overlaps between placed objects are allowed during this stage.
   - The goal is to achieve a rough layout that satisfies area constraints.

2. **Detailed Placement:**
   - Detailed placement refines the object locations obtained from global placement.
   - It enforces non-overlapping constraints and ensures that cells are placed on legal cell sites.
   - The quality of detailed placement significantly impacts subsequent routing stages.

Command to run placement

```tcl
# Congestion aware placement by default
run_placement
```

Screenshots of placement run

![Screenshot 2024-12-17 221757](https://github.com/user-attachments/assets/8734e380-1803-4320-b4ef-b69f2e8a1c9a)

#### 5. Load generated placement def in magic tool and explore the placement.

Commands to load placement def in magic in another terminal

```bash
# Change directory to path containing generated placement def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/16-12_14-12/results/placement/

# Command to load the placement def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```

Screenshots of floorplan def in magic
![Screenshot 2024-12-17 223714](https://github.com/user-attachments/assets/770bc892-6880-40ae-98ad-3d447908f70c)

### Inputs Item                                                                                               

 PDKs                    Process Design Kits (PDKs) provide technology-specific information for chip design.        
 DRC and LVS rules        Design Rule Check (DRC) and Layout vs. Schematic (LVS) rules ensure layout compliance.      
SPICE models             These models describe transistor behavior for circuit simulation.                            
 Library & User-defined specs  Custom libraries and specifications specific to your project.                               

### Design Steps
1. **Circuit Design:**
   - Create the logical schematic of your circuit.
   - Define the functionality and connections of standard cells.

2. **Layout Design:**
   - Use layout tools (e.g., MAGIC) to create the physical layout.
   - Follow design rules and guidelines for placement and routing.

3. **Characterization using GUNA:**
   - Perform timing, power, and noise characterizations.
   - Validate the design against specifications.

### Outputs
- **CDL (Circuit Description Language):** A textual representation of the circuit.
- **GDSII:** The layout file in GDSII format for fabrication.
- **LEF (Library Exchange Format):** Contains information about cell sizes, pin locations, and other details.
- **Spice Extracted Netlist:** Includes parasitic information for circuit simulation.
- **Timing, Noise, and Power Libraries:** Generated during characterization.


## Section 3 - Design library cell using Magic Layout and ngspice characterization Day 3 

### Theory

# Inverter Characterization using Sky130 Model Files


## CMOS Inverter Simulation with ngspice

This guide demonstrates how to create a basic CMOS inverter netlist, perform DC and transient analyses using ngspice, and understand key static and dynamic characteristics.

## Static Characteristics

1. **Switching Threshold (Vth):**
   - The voltage at which the inverter transitions from the high state (logic 1) to the low state (logic 0).
2. **Input Low Voltage (Vil):**
   - The maximum input voltage considered as logic 0.
3. **Input High Voltage (Vih):**
   - The minimum input voltage considered as logic 1.
4. **Output Low Voltage (Vol):**
   - The voltage at which the output transitions from high to low.
5. **Output High Voltage (Voh):**
   - The voltage at which the output transitions from low to high.
6. **Noise Margins:**
   - The voltage range between Vil and Vol (low noise margin) and between Vih and Voh (high noise margin).

## Dynamic Characteristics

1. **Propagation Delays:**
   - The time taken for the output to change after a change in input.
2. **Rise Time (tr):**
   - The time taken for the output to transition from Vol to Voh.
3. **Fall Time (tf):**
   - The time taken for the output to transition from Voh to Vol.



# Design library cell using Magic Layout and ngspice characterization
## Creating Standard Cell Layout

1. **Design the Inverter Layout:**
   - Use a layout tool (such as MAGIC) to create the inverter layout.
   - Follow process-specific design rules and guidelines.
   - Place standard cells (transistors, metal layers, etc.) based on the logical schematic.

2. **Extraction Process:**
   - After layout creation, extract parasitic capacitances and resistances.
   - In the `tkcon` window, execute the command `extract all`.
   - This generates an extracted file with parasitic information (e.g., capacitances, interconnect resistance).
   - The extracted file is saved in the `vsdstdcelldesign` directory.

3. **SPICE Netlist:**
   - Use the extracted data to create a SPICE-compatible netlist (usually in `.sp` or `.cir` format).
   - Include transistor models, capacitances, and resistances.
   - Use this netlist for simulation in tools like ngspice.


## Introduction to LEF Files in VLSI Design
In VLSI (Very Large Scale Integration) design, LEF (Library Exchange Format) files play a crucial role in interfacing between layout tools and place-and-route (PnR) tools. Here’s what you need to know:

Purpose of LEF Files:

The entire layout information of a block (whether it’s a macro or a standard cell) is not necessary for PnR tools.
PnR tools require minimal information, including the PR boundary (bounding box) and pin positions.
LEF files provide an abstract representation of the block, exposing only the essential details needed for PnR.


Cell LEF	 Abstract view of the cell which holds information about PR boundary, pin positions and metal layer information. 
 Technology LEF Holds information about the metal layers, via, DRC technology used by placer and router.

![image](https://github.com/user-attachments/assets/4e4795f0-60d3-4080-bbb8-5f26ad1b97c5)

VLSI Routing: Tracks and Routes

In VLSI design, understanding tracks and routes is essential for successful interconnect design. Let's break it down:

## Tracks

- **Definition:**
  - Tracks represent predefined horizontal and vertical paths on each metal layer.
  - They serve as guidelines for routing wires (metal traces) within a chip.

- **Purpose:**
  - Tracks help maintain uniform spacing and alignment during routing.
  - They simplify the routing process by providing fixed paths.

## Routes

- **Definition:**
  - Routes are the actual metal traces that carry signals (such as interconnects or wires).
  - These traces can be placed over the tracks, following specified routing rules.

- **Functionality:**
  - Routes connect different components (cells) within the chip.
  - They form the wiring network for data flow.

## `tracks.info` File

- The `tracks.info` file:
  - Provides information about horizontal and vertical tracks available on each metal layer.
  - Specifies pitch, spacing, and other relevant details necessary for efficient routing.


### Implementation

* Section 3 tasks:-
1. Clone custom inverter standard cell design from github repository: [Standard cell design and characterization using OpenLANE flow](https://github.com/nickson-jose/vsdstdcelldesign).
2. Load the custom inverter layout in magic and explore.
3. Spice extraction of inverter in magic.
4. Editing the spice model file for analysis through simulation.
5. Post-layout ngspice simulations.
6. Find problem in the DRC section of the old magic tech file for the skywater process and fix them.

#### 1. Clone custom inverter standard cell design from github repository

```bash
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Clone the repository with custom inverter design
git clone https://github.com/nickson-jose/vsdstdcelldesign

# Change into repository directory
cd vsdstdcelldesign

# Copy magic tech file to the repo directory for easy access
cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech .

# Check contents whether everything is present
ls

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &
```

Screenshot of commands run
![Screenshot 2024-12-18 231253](https://github.com/user-attachments/assets/23ec7409-aedb-403a-ad4f-17d622277448)

#### 2. Load the custom inverter layout in magic and explore.

Screenshot of custom inverter layout in magic NMOS and PMOS identified

![Screenshot 2024-12-19 214039](https://github.com/user-attachments/assets/e56518d8-de6d-4f02-add9-d1cecf2ca8c3)

![Screenshot 2024-12-19 214132](https://github.com/user-attachments/assets/fa9de724-f830-43e4-892a-e0b1c72f4de8)

#### 3. Spice extraction of inverter in magic.

Commands for spice extraction of the custom inverter layout to be used in tkcon window of magic

```tcl
# Check current directory
pwd

# Extraction command to extract to .ext format
extract all

# Before converting ext to spice this command enable the parasitic extraction also
ext2spice cthresh 0 rthresh 0

# Converting to ext to spice
ext2spice
```
![Screenshot 2024-12-20 004218](https://github.com/user-attachments/assets/ee6b7964-8022-4b9b-8461-48f7df369d11)

Screenshot of created spice file

![Screenshot 2024-12-19 222928](https://github.com/user-attachments/assets/445fd979-f08b-4cd3-ad4e-887b751f496a)

#### 4. Editing the spice model file for analysis through simulation.

Measuring unit distance in layout grid

![Screenshot 2024-12-20 004218](https://github.com/user-attachments/assets/7e713f18-81d6-4f1e-a848-5169e861bea6)

Final edited spice file ready for ngspice simulation

![Screenshot 2024-12-20 011035](https://github.com/user-attachments/assets/182902f8-d54d-4241-b873-628af1e3ef39)

#### 5. Post-layout ngspice simulations.

Commands for ngspice simulation

```bash
# Command to directly load spice file for simulation to ngspice
ngspice sky130_inv.spice

# Now that we have entered ngspice with the simulation spice file loaded we just have to load the plot
plot y vs time a
```

Screenshots of ngspice run

![Screenshot 2024-12-20 021308](https://github.com/user-attachments/assets/ab770af2-5ce9-4c6a-a8d1-937a8f3a7be3)

![Screenshot 2024-12-20 021414](https://github.com/user-attachments/assets/e8f73dda-34c2-426a-b909-f26a3709ad5a)


Screenshot of generated plot
![Screenshot 2024-12-20 024040](https://github.com/user-attachments/assets/5032ae92-cbf0-42b1-9949-8126cdf4e7dc)


Rise transition time calculation

```math
Rise\ transition\ time = Time\ taken\ for\ output\ to\ rise\ to\ 80\% - Time\ taken\ for\ output\ to\ rise\ to\ 20\%
```
```math
20\%\ of\ output = 660\ mV
```
```math
80\%\ of\ output = 2.64\ V
```

20% Screenshots

![Screenshot 2024-12-20 154226](https://github.com/user-attachments/assets/fe5d52c4-4d06-433d-a9fa-0f078225948c)

![Screenshot 2024-12-20 154344](https://github.com/user-attachments/assets/e52d5389-a80a-4c39-8456-1057a2d07007)

80% Screenshots

![Screenshot 2024-12-20 154821](https://github.com/user-attachments/assets/fbddd18d-908e-465f-93d2-af6032969647)

![Screenshot 2024-12-20 154830](https://github.com/user-attachments/assets/53f1e5e6-d303-454e-a293-626b2c134664)

```math
Rise\ transition\ time = 6.25279 - 6.18538 = 0.06741\ ns = 67.41\ ps
```

Fall transition time calculation

```math
Fall\ transition\ time = Time\ taken\ for\ output\ to\ fall\ to\ 20\% - Time\ taken\ for\ output\ to\ fall\ to\ 80\%
```
```math
20\%\ of\ output = 660\ mV
```
```math
80\%\ of\ output = 2.64\ V
```

20% Screenshots

![Screenshot 2024-12-20 155819](https://github.com/user-attachments/assets/06d01d45-39e5-46bc-8747-338ccb53d5e0)
 
80% Screenshots
![Screenshot 2024-12-20 155757](https://github.com/user-attachments/assets/eae49709-61a1-4586-83e1-c47a98e76a9e)

![Screenshot 2024-12-20 155839](https://github.com/user-attachments/assets/d42b6d9b-a44e-459c-b061-e51f6645042b)

```math
Fall\ transition\ time = 8.09732 - 8.05527 = 0.04205\ ns = 42.05\ ps
```

Rise Cell Delay Calculation

```math
Rise\ Cell\ Delay = Time\ taken\ for\ output\ to\ rise\ to\ 50\% - Time\ taken\ for\ input\ to\ fall\ to\ 50\%
```
```math
50\%\ of\ 3.3\ V = 1.65\ V
```

50% Screenshots
![Screenshot 2024-12-20 160737](https://github.com/user-attachments/assets/dd2d2852-d12a-44c2-81d9-df4b6a2bd0ce)

![Screenshot 2024-12-20 160724](https://github.com/user-attachments/assets/137542d3-eb45-43cc-a423-42a6c4940f1f)

```math
Rise\ Cell\ Delay = 6.21492 - 6.14984 = 0.06508\ ns = 65.08\ ps
```

Fall Cell Delay Calculation

```math
Fall\ Cell\ Delay = Time\ taken\ for\ output\ to\ fall\ to\ 50\% - Time\ taken\ for\ input\ to\ rise\ to\ 50\%
```
```math
50\%\ of\ 3.3\ V = 1.65\ V
```

50% Screenshots

![Screenshot 2024-12-20 161027](https://github.com/user-attachments/assets/9344b0d2-8d76-4a20-98b4-19db906e24cd)

![Screenshot 2024-12-20 161017](https://github.com/user-attachments/assets/1f75ec54-5a73-467e-bca9-46780b31cfa9)


```math
Fall\ Cell\ Delay = 1.208- 1.20491 = 0.00309\ ns = 30.9\ ps
```

#### 6. Find problem in the DRC section of the old magic tech file for the skywater process and fix them.

## LEF File Creation
Now that we have successfully characterized the inverter, the next step is to create a LEF (Library Exchange Format) file.

**VLSI Layout Geometries and DRC Errors**

In this section, we explore independent example layout geometries (M3.1, M3.2, M3.5, and M3.6) and highlight the specific DRC (Design Rule Check) errors associated with each:

1. **M3.1 (Metal Width DRC):**
   - Violation: The metal trace width in M3.1 is below the specified minimum width threshold.
   - Error: Metal width does not meet design rules.

2. **M3.2 (Metal Spacing DRC):**
   - Violation: The distance between adjacent metal traces in M3.2 does not meet the required spacing.
   - Error: Metal spacing violation.

3. **M3.5 (Via Overlapping DRC):**
   - Violation: The vias in M3.5 overlap with each other.
   - Error: Via overlapping issue.

4. **M3.6 (Minimum Area DRC):**
   - Violation: The enclosed area within M3.6 does not meet the specified minimum area requirement.
   - Error: Minimum area violation.
Commands to download and view the corrupted skywater process magic tech file and associated files to perform drc corrections

```bash
# Change to home directory
cd

# Command to download the lab files
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz

# Since lab file is compressed command to extract it
tar xfz drc_tests.tgz

# Change directory into the lab folder
cd drc_tests

# List all files and directories present in the current directory
ls -al

# Command to view .magicrc file
gvim .magicrc

# Command to open magic tool in better graphics
magic -d XR &
```

Screenshots of commands run
![Screenshot 2024-12-20 235848](https://github.com/user-attachments/assets/f8e940b9-7f84-4eec-bdba-28581b9d98b2)

![Screenshot 2024-12-20 235936](https://github.com/user-attachments/assets/cc65f100-7c9b-489d-89d2-92a03ccec7cd)

# Using Magic Tool: Filling an Area with Metal 3 and Creating a VIA2 Mask

In this guide, we'll demonstrate how to fill a selected area with metal 3 and create a VIA2 mask using the Magic layout tool.

## Steps:

1. **Select an Area and Fill with Metal 3:**
   - Open the Magic GUI.
   - Select the desired area on your layout.
   - Guide the pointer to the metal 3 layer.
   - Press `P` to fill the selected region with metal 3.

2. **Create the VIA2 Mask:**
   - Open the `tkcon` terminal within Magic.
   - Type the command: `cif see VIA2`.
   - The metal 3-filled area will now be associated with the VIA2 mask.

Incorrectly implemented poly.9 rule no drc violation even though spacing < 0.48u

![image](https://github.com/user-attachments/assets/c2a6d5db-2e05-45c8-9496-139aafacbc21)

New commands inserted in sky130A.tech file to update drc

![Screenshot 2024-12-21 003938](https://github.com/user-attachments/assets/be0687ce-ef8a-4b96-a294-5035c9b40094)

![Screenshot 2024-12-21 004437](https://github.com/user-attachments/assets/0cb69ff9-1f14-4a3a-92c4-adda08252eab)


Commands to run in tkcon window

```tcl
# Loading updated tech file
tech load sky130A.tech

# Must re-run drc check to see updated drc errors
drc check

# Selecting region displaying the new errors and getting the error messages 
drc why
```

Screenshot of magic window with rule implemented

![Screenshot 2024-12-21 005623](https://github.com/user-attachments/assets/487b5768-83ba-4fae-972a-dba9bca893e3)

**Incorrectly implemented nwell.4 complex rule correction**

Screenshot of nwell rules

![image](https://github.com/user-attachments/assets/f1b30b9e-dee4-4297-94fa-8b7341f68ba4)

Incorrectly implemented nwell.4 rule no drc violation even though no tap present in nwell
![Screenshot 2024-12-21 020849](https://github.com/user-attachments/assets/a07df1a0-9b55-47eb-bfb9-9cad1ea18383)

New commands inserted in sky130A.tech file to update drc

![Screenshot 2024-12-21 020733](https://github.com/user-attachments/assets/1c249221-9482-4fe9-98c7-deda5f24e8da)

Commands to run in tkcon window

```tcl
# Loading updated tech file
tech load sky130A.tech

# Change drc style to drc full
drc style drc(full)

# Must re-run drc check to see updated drc errors
drc check

# Selecting region displaying the new errors and getting the error messages 
drc why
```

Screenshot of magic window with rule implemented

![Screenshot 2024-12-21 021017](https://github.com/user-attachments/assets/eaee46f8-a1f0-4725-b891-1a03f6154db7)

# Day 4 : Pre-layout timing analysis and importance of good clock tree 
## Section 4 - Pre-layout timing analysis and importance of good clock tree 

### Theory

# Timing Modeling Using Delay Tables and Converting Grid Info to Track Info

In this section, we'll explore timing modeling using delay tables and the process of converting grid information to track information. Let's break it down step by step:

## Timing Modeling with Delay Tables

1. **Delay Tables:**
   - Delay tables provide information about the delay (propagation time) of signals through various components (such as gates, wires, and interconnects).
   - These tables help estimate signal arrival times and ensure proper timing in the design.

2. **Usage:**
   - During the physical design process, delay tables are used to model the behavior of standard cells, macros, and other components.
   - They guide the placement and routing tools to optimize signal paths for timing closure.

## Converting Grid Info to Track Info

1. **Purpose:**
   - In physical design, we need to convert grid information (such as rows and columns) into track information.
   - Tracks represent predefined horizontal and vertical paths on each metal layer.

2. **Considerations:**
   - When designing standard cells, keep the following in mind:
     - Input and output ports should align with the intersection of vertical and horizontal tracks.
     - The standard cell's width should be an odd multiple of the track pitch, and its height should be an odd multiple of the vertical track pitch.

3. **LEF File Extraction:**
   - To proceed further, we require the LEF (Library Exchange Format) file for the Inverter cell.
   - Extract it from the current Inverter cell to provide essential information for the place-and-route (PNR) process.

4. **Understanding Tracks:**
   - Open the `tracks.info` file to learn more about the horizontal and vertical tracks available on each metal layer.
   - This file specifies pitch, spacing, and other relevant details necessary for efficient routing.

### Implementation

* Section 4 tasks:-
1. Fix up small DRC errors and verify the design is ready to be inserted into our flow.
2. Save the finalized layout with custom name and open it.
3. Generate lef from the layout.
4. Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory.
5. Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow.
6. Run openlane flow synthesis with newly inserted custom inverter cell.
7. Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.
8. Once synthesis has accepted our custom inverter we can now run floorplan and placement and verify the cell is accepted in PnR flow.
9. Do Post-Synthesis timing analysis with OpenSTA tool.
10. Make timing ECO fixes to remove all violations.
11. Replace the old netlist with the new netlist generated after timing ECO fix and implement the floorplan, placement and cts.
12. Post-CTS OpenROAD timing analysis.
13. Explore post-CTS OpenROAD timing analysis by removing 'sky130_fd_sc_hd__clkbuf_1' cell from clock buffer list variable 'CTS_CLK_BUFFER_LIST'.

#### 1. Fix up small DRC errors and verify the design is ready to be inserted into our flow.

Conditions to be verified before moving forward with custom designed cell layout:
* Condition 1: The input and output ports of the standard cell should lie on the intersection of the vertical and horizontal tracks.
* Condition 2: Width of the standard cell should be odd multiples of the horizontal track pitch.
* Condition 3: Height of the standard cell should be even multiples of the vertical track pitch.

Commands to open the custom inverter layout

```bash
# Change directory to vsdstdcelldesign
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &
```

Screenshot of tracks.info of sky130_fd_sc_hd

![Screenshot 2024-12-22 124653](https://github.com/user-attachments/assets/ea5ac0cc-3cc5-475c-8ea6-06a3dcef5763)

Commands for tkcon window to set grid as tracks of locali layer

```tcl
# Get syntax for grid command
help grid

# Set grid values accordingly
grid 0.46um 0.34um 0.23um 0.17um
```
Screenshot of commands run & Condition 1 verified

![Screenshot 2024-12-22 133405](https://github.com/user-attachments/assets/b8b59c22-8384-46f1-8b4e-0a39bdc9abd9)

Condition 2 verified

```math
Horizontal\ track\ pitch = 0.46\ um
```

![Screenshot 2024-12-22 133938](https://github.com/user-attachments/assets/bd761146-6db3-4e7a-bcdc-213e4138bb0a)

```math
Width\ of\ standard\ cell ~1.38\ um = 0.46 * 3
```
Condition 3 verified

```math
Vertical\ track\ pitch = 0.34\ um
```

![Screenshot 2024-12-22 134136](https://github.com/user-attachments/assets/78baa0f1-def0-4f25-9f40-0eba3cf4dae2)

```math
Height\ of\ standard\ cell ~ 2.72\ um = 0.34 * 8
```


#### 2. Save the finalized layout with custom name and open it.

Command for tkcon window to save the layout with custom name

```tcl
# Command to save as
save sky130_vsdinv.mag
```

Command to open the newly saved layout

```bash
# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_vsdinv.mag &
```

Screenshot of newly saved layout
![Screenshot 2024-12-22 134743](https://github.com/user-attachments/assets/b440aa3c-e6ab-4721-a415-fc88f30aaf90)

#### 3. Generate lef from the layout.

Command for tkcon window to write lef

```tcl
# lef command
lef write
```

Screenshot of command run

![Screenshot 2024-12-22 134935](https://github.com/user-attachments/assets/2f76c86b-3c9c-4604-a982-0771f483ec7f)

Screenshot of newly created lef file

![Screenshot 2024-12-22 142452](https://github.com/user-attachments/assets/a52bbcbc-9ce6-442f-925c-1262e0f65ea0)

#### 4. Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory.

Commands to copy necessary files to 'picorv32a' design 'src' directory

```bash
# Copy lef file
cp sky130_vsdinv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# List and check whether it's copied
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# Copy lib files
cp libs/sky130_fd_sc_hd__* ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# List and check whether it's copied
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
```

Screenshot of commands run

![Screenshot 2024-12-22 143716](https://github.com/user-attachments/assets/16194843-fe13-4ea1-8f57-98adffb57ea7)


#### 5. Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow.

Commands to be added to config.tcl to include our custom cell in the openlane flow

```tcl
set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]
```

Edited config.tcl to include the added lef and change library to ones we added in src directory

![Screenshot 2024-12-22 144904](https://github.com/user-attachments/assets/f89c51ec-0e5d-4231-babc-b0c4d8d92269)

#### 6. Run openlane flow synthesis with newly inserted custom inverter cell.

Commands to invoke the OpenLANE flow include new lef and perform synthesis 

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

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

Screenshots of commands run

![Screenshot 2024-12-22 145315](https://github.com/user-attachments/assets/1ec35d3b-e571-46fa-921c-cb6265c77a57)

![Screenshot 2024-12-22 150129](https://github.com/user-attachments/assets/e873a026-2619-46bb-aa46-d114fa21b5df)

#### 7. Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.

Noting down current design values generated before modifying parameters to improve timing

![Screenshot 2024-12-22 150212](https://github.com/user-attachments/assets/08dd8582-b8e0-4189-bdcc-ebfca5a6da26)

![Screenshot 2024-12-22 150223](https://github.com/user-attachments/assets/406e353e-9d78-495f-b17d-488382f5d2c7)

Commands to view and change parameters to improve timing and run synthesis

```tcl
# Now once again we have to prep design so as to update variables
prep -design picorv32a -tag 24-03_10-03 -overwrite

# Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to display current value of variable SYNTH_STRATEGY
echo $::env(SYNTH_STRATEGY)

# Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

# Command to display current value of variable SYNTH_BUFFERING to check whether it's enabled
echo $::env(SYNTH_BUFFERING)

# Command to display current value of variable SYNTH_SIZING
echo $::env(SYNTH_SIZING)

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
echo $::env(SYNTH_DRIVING_CELL)

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

Screenshot of merged.lef in `tmp` directory with our custom inverter as macro

![Screenshot 2024-12-22 155033](https://github.com/user-attachments/assets/6b550e6e-0c2d-414a-be92-90cb9536683c)

Screenshots of command run

![Screenshot 2024-12-22 154324](https://github.com/user-attachments/assets/af59e4b2-ee67-44f8-a6ee-6e84d344935c)

Comparing to previously noted run values area has increased and worst negative slack has become 0

![Screenshot 2024-12-22 154455](https://github.com/user-attachments/assets/beeb9fd1-e5cd-4741-b89e-8161b23b4f34)

![Screenshot 2024-12-22 154505](https://github.com/user-attachments/assets/923a0c60-1dc0-464a-ae3d-a5426a88b1f6)


#### 8. Once synthesis has accepted our custom inverter we can now run floorplan and placement and verify the cell is accepted in PnR flow.

Now that our custom inverter is properly accepted in synthesis we can now run floorplan using following command

```tcl
# Now we can run floorplan
run_floorplan
```
we get error while running the command

![Screenshot 2024-12-22 160903](https://github.com/user-attachments/assets/e55bd4cc-4b65-42c5-8b18-bd85fa30c718)


```tcl
# Follwing commands are alltogather sourced in "run_floorplan" command
init_floorplan
place_io
tap_decap_or
```

Screenshots of commands run

![Screenshot 2024-12-22 161945](https://github.com/user-attachments/assets/f1025b8b-0ea2-4ea5-a473-772c59631471)
```tcl
# Now we are ready to run placement
run_placement
```

Screenshots of command run

![Screenshot 2024-12-22 162024](https://github.com/user-attachments/assets/4ace1b6f-df56-45a7-a58b-7fdcc9648cf5)

![Screenshot 2024-12-22 162356](https://github.com/user-attachments/assets/7711d8fa-32d4-465d-9ee4-a7c272f625a7)

Commands to load placement def in magic in another terminal

```bash
# Change directory to path containing generated placement def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/24-03_10-03/results/placement/

# Command to load the placement def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```

Command for tkcon window to view internal layers of cells

```tcl
# Command to view internal connectivity layers
expand
```

Screenshot of custom inverter inserted in placement

![Screenshot 2024-12-22 163249](https://github.com/user-attachments/assets/7cd5c66c-3ce1-4bd3-bdd8-5dca66f2955e)

#### 9. Do Post-Synthesis timing analysis with OpenSTA tool.

Since we are having 0 wns after improved timing run we are going to do timing analysis on initial run of synthesis which has lots of violations and no parameters were added to improve timing

Commands to invoke the OpenLANE flow include new lef and perform synthesis 

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

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```
Newly created `pre_sta.conf` for STA analysis in `openlane` directory

![Screenshot 2024-12-22 231405](https://github.com/user-attachments/assets/cab2565e-5311-4b79-a1c1-3a989cd4e5ca)


Newly created `my_base.sdc` for STA analysis in `openlane/designs/picorv32a/src` directory based on the file `openlane/scripts/base.sdc`

![Screenshot 2024-12-22 231258](https://github.com/user-attachments/assets/90fff94a-b7c4-4c54-b485-9c82eacfa272)


Commands to run STA in another terminal

```bash
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Command to invoke OpenSTA tool with script
sta pre_sta.conf
```
![Screenshot 2024-12-22 231247](https://github.com/user-attachments/assets/472e556a-388a-4d5f-b375-90ad75021880)

![Screenshot 2024-12-22 231520](https://github.com/user-attachments/assets/80d6ca83-361f-4c86-99e4-44c14c1283cf)

To fix this slack we use

```
# Now once again we have to prep design so as to update variables
prep -design picorv32a -tag 22-12_11-34 -overwrite

# Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to display current value of variable SYNTH_STRATEGY
echo $::env(SYNTH_STRATEGY)

# Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

# Command to display current value of variable SYNTH_BUFFERING to check whether it's enabled
echo $::env(SYNTH_BUFFERING)

# Command to display current value of variable SYNTH_SIZING
echo $::env(SYNTH_SIZING)

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
echo $::env(SYNTH_DRIVING_CELL)

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```
![Screenshot 2024-12-22 231532](https://github.com/user-attachments/assets/e8933b30-68c1-4896-871e-e128adf22a1b)

finally after running placement 

![Screenshot 2024-12-23 011656](https://github.com/user-attachments/assets/d54f1257-e7f9-4ae7-94cb-6717d15f8ecc)

## Section 5 - Final steps for RTL2GDS using tritonRoute and openSTA 

### Theory


## Power Distribution Network (PDN) Generation in OpenLANE

In OpenLANE, the PDN (Power Distribution Network) is crucial for proper power delivery within the chip. Let's walk through the steps to build the PDN:

## 1. PDN Generation

- The PDN ensures that all standard cells and macros receive adequate power.
- It provides a network of power rails (VDD and VSS) across the chip.

## 2. Using `gen_pdn` Procedure

- The `gen_pdn` procedure is responsible for running the PDN generation process.
- It sets up the power grid, defines power rails, and ensures proper connectivity.

## Common Issues

1. **`LIB_SYNTH_COMPLETE`:**
   - This variable must be defined in the `config.tcl` file.
   - It is called by the `gen_pdn` procedure defined in the `or_pdn.tcl` file.

2. **`LEF_MERGED_UNPADDED`:**
   - Ensure that this variable is correctly set in the `config.tcl` file.
   - It provides essential information for PDN generation.

### Implementation

* Section 5 tasks:-
1. Perform generation of Power Distribution Network (PDN) and explore the PDN layout.
2. Perfrom detailed routing using TritonRoute.
3. Post-Route parasitic extraction using SPEF extractor.
4. Post-Route OpenSTA timing analysis with the extracted parasitics of the route.

#### 1. Perform generation of Power Distribution Network (PDN) and explore the PDN layout.

Commands to perform all necessary stages up until now

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

# Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

# Following commands are alltogather sourced in "run_floorplan" command
init_floorplan
place_io
tap_decap_or

# Now we are ready to run placement
run_placement

# Incase getting error
unset ::env(LIB_CTS)

# With placement done we are now ready to run CTS
run_cts

# Now that CTS is done we can do power distribution network
gen_pdn 
```


Commands to load PDN def in magic in another terminal

```bash
# Change directory to path containing generated PDN def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/22-12_11-34/tmp/floorplan/

# Command to load the PDN def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read 14-pdn.def &
```

![Screenshot 2024-12-23 011945](https://github.com/user-attachments/assets/37b0808e-cecc-40c5-935c-41b945a3343e)

#### 2. Perfrom detailed routing using TritonRoute and explore the routed layout.

Command to perform routing

```tcl
# Check value of 'CURRENT_DEF'
echo $::env(CURRENT_DEF)

# Check value of 'ROUTING_STRATEGY'
echo $::env(ROUTING_STRATEGY)

# Command for detailed route using TritonRoute
run_routing
```

Screenshots of routing run
![Screenshot 2024-12-23 012632](https://github.com/user-attachments/assets/c6297ef4-0968-4314-bf6d-1338e9adf16c)


![Screenshot 2024-12-23 013136](https://github.com/user-attachments/assets/dc1c75ea-ec90-4315-8554-39ea73c406d6)

Commands to load routed def in magic in another terminal

```bash
# Change directory to path containing routed def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/22-12_11-34/results/routing/

# Command to load the routed def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.def &
```

Screenshots of routed def

![Screenshot 2024-12-23 013812](https://github.com/user-attachments/assets/58540b6d-f625-44bb-bee5-6cb2fd4e50fb)


![Screenshot 2024-12-23 014742](https://github.com/user-attachments/assets/a846fdf9-a55f-408f-b604-b982518711ce)


![Screenshot 2024-12-23 013948](https://github.com/user-attachments/assets/d98684f8-529e-44b8-b31e-d7a8202fac6e)

Screenshot of fast route guide present in `openlane/designs/picorv32a/runs/22-12_11-34/tmp/routing` directory

![Screenshot 2024-12-23 015127](https://github.com/user-attachments/assets/a305541c-4fa8-43ac-8202-78b831beed35)

## VLSI Routing: Global Route and Detail Route

In VLSI design, the routing process is divided into two main stages: global route (or fast route) and detail route. Let's explore each stage:

## 1. Global Route (Fast Route)

- **Purpose:**
  - The global route focuses on quickly establishing a high-level routing solution.
  - It divides the chip into rectangular grid cells, forming a 3D routing graph.

- **Key Points:**
  - The global route creates a routing guide, which consists of boxes (representing pins of cells).
  - The output of the global route is a set of routing guides for each net.

## 2. Detail Route

- **Performed by Engine:**
  - Detail route is executed by the engine called tritonRoute.
  - It refines the routing solution obtained from the global route.

- **Using Global Route Output:**
  - Detail route utilizes the output from the global route, including the routing guides.
  - Algorithms are applied to find the best possible connectivity among all the routing points.

#### 3. Post-Route parasitic extraction using SPEF extractor.

Commands for SPEF extraction using external tool

```bash
# Change directory
cd Desktop/work/tools/SPEF_EXTRACTOR

# Command extract spef
python3 main.py /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/22-12_11-34/tmp/merged.lef /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/22-12_11-34/results/routing/picorv32a.def
```

#### 4. Post-Route OpenSTA timing analysis with the extracted parasitics of the route.

Commands to be run in OpenLANE flow to do OpenROAD timing analysis with integrated OpenSTA in OpenROAD

```tcl
# Command to run OpenROAD tool
openroad

# Reading lef file
read_lef /openLANE_flow/designs/picorv32a/runs/22-12_11-34/tmp/merged.lef

# Reading def file
read_def /openLANE_flow/designs/picorv32a/runs/22-12_11-34/results/routing/picorv32a.def

# Creating an OpenROAD database to work with
write_db pico_route.db

# Loading the created database in OpenROAD
read_db pico_route.db

# Read netlist post CTS
read_verilog /openLANE_flow/designs/picorv32a/runs/22-12_11-34/results/synthesis/picorv32a.synthesis_preroute.v

# Read library for design
read_liberty $::env(LIB_SYNTH_COMPLETE)

# Link design and library
link_design picorv32a

# Read in the custom sdc we created
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

# Setting all cloks as propagated clocks
set_propagated_clock [all_clocks]

# Read SPEF
read_spef /openLANE_flow/designs/picorv32a/runs/22-12_11-34/results/routing/picorv32a.spef

# Generating custom timing report
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

# Exit to OpenLANE flow
exit
```

![Screenshot 2024-12-24 031209](https://github.com/user-attachments/assets/80a40f15-5964-492a-99ce-b3089d7e5408)

![Screenshot 2024-12-24 031221](https://github.com/user-attachments/assets/9369898b-875b-48fd-a14d-0e12c897daec)

![Screenshot 2024-12-24 031228](https://github.com/user-attachments/assets/de45ba9d-892d-4502-a015-a98dd253c9ef)

![Screenshot 2024-12-24 031234](https://github.com/user-attachments/assets/c6cbf686-5911-4ab0-aed1-633e7b1835c7)

# Certificate

![Digital-VLSI-SoC-Design-and-Planning-Certificate]![image](https://github.com/user-attachments/assets/c0f8ad1b-98e4-4c2e-999f-e7bbd25ef3d8)

 
# Acknowledgements

* [Kunal Ghosh](https://github.com/kunalg123), Co-founder, VSD Corp. Pvt. Ltd.
* [Nickson P Jose](https://github.com/nickson-jose), Physical Design Engineer, Intel Corporation.
* [R. Timothy Edwards](https://github.com/RTimothyEdwards), Senior Vice President of Analog and Design, efabless Corporation.


