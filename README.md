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
![Screenshot 2024-12-12 163552](https://github.com/user-attachments/assets/2908c18e-8596-48f3-83b5-ddd142da7279)
