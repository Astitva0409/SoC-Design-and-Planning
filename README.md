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
