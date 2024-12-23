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

## Section 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK Day 1

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
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/floorplan/

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
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/placement/

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



| Cell LEF	 | Abstract view of the cell which holds information about PR boundary, pin positions and metal layer information.  |
|---------------|---------------|
| Technology LEF | Holds information about the metal layers, via, DRC technology used by placer and router.|

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
