# OpenLANE-Workshop
The workshop on SoC design planning in Openlane flow using the latest Google-SkyWater 130nm process node.


<br />
<p align="center">

  ![](images/PD.png)

  <h3 align="center">Advanced Physical Design - OpenLANE Workshop</h3>
</p>
<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
    </li>
     <li>
      <a href="#day-1-introduction-to-physical-design-flow-and-open-source-eda">Day 1 Introduction to Physical Design Flow and Open Source EDA </a>
      <ul>
        <li><a href="#rtl-to-gdsii-process">RTL to GDSII Process</a></li>
        <li><a href="#openlane-asic-flow">OpenLANE ASIC Flow</a></li>
        <li><a href="#skywater-files">Skywater Files</a></li>
        <li><a href="#design-preparation">Design preparation</a></li>
        <li><a href="#synthesis">Synthesis</a></li>
      </ul>
    </li>    
  </ol>
</details>
  
<!-- ABOUT THE PROJECT -->
## About The Project

This project gives an interactive tutorial of OpenLANE Flow using the latest Google-SkyWater 130nm process node which is conducted by VSD-IAT.

OpenLANE is an automated RTL to GDSII flow based on several components including OpenROAD, Yosys, Magic, Netgen, Fault, OpenPhySyn, SPEF-Extractor and custom methodology scripts for design exploration and optimization. It is a tool started for true open source tape-out experience and comes with APACHE version 2.0 . The goal of OpenLANE is to produce clean GDSII without any human intervention. OpenLANE is tuned for Skywater 130nm open-source PDK and can be used to produce hard macros and chips.

<!-- Day 1 Introduction to Physical Design Flow and Open Source EDA -->
## Day 1 Introduction to Physical Design Flow and Open Source EDA

### RTL to GDSII Process

Very large-scale integration (VLSI) is the process of creating an integrated circuit (IC) by combining millions of MOS transistors onto a single chip. Very-large-scale integration (VLSI) is the process of creating an integrated circuit (IC) by combining millions of MOS transistors onto a single chip. There are many difficulties in creating the chip which now consists of billions of transistors. For creating a function-able chip, they do many design and verification process to analyse and create a function-able chip. 
These design and verification stages are broadly classified into two steps. One in Front End Design and another one is Back-end design. Front end Design starts with the design specification and ends in RTL Design and verification. Back end design starts with Synthesis and goes till Fabrication.

In this Project, we will cover a part of Back end design flow steps starting from Synthesis and goes till Routing.

One of two design methods may be employed while creating the HDL of a microarchitecture.
  - RTL Design
  - Behavioral Modeling

RTL (Register Transfer Level) is used to create high-level representations of a circuit using Verilog and/or VHDL.  EDA tools will use the HDL to perform mapping of higher-level components to the transistor level needed for physical implementation.
Behavioral Modeling – Allows the microarchitecture modeling to be performed with behavior-based modeling in HDL. This method bridges the gap between C and HDL allowing HDL design to be performed.

RTL Verification - Behavioral verification of design will be performed using testbenches.

Synthesis is a process which converts RTL to a circuit out of components from the cell library. Synthesis will do three important steps which are Translation, optimization and mapping. Post-Synthesis STA Analysis is performed on different path groups.

Partition process is converting the complex system into smaller sub-systems. For chip-level Implementation, Partition is needed and for block-level implementation, it is already performed and necessary data is given for the flow.

Floorplanning is the process of placing blocks/macros in the chip/core area. Dimensions, Pin locations and Rows definition are defined in this process. 
 
Power planning is the process of creating the power mesh which is used to connect power pins to all components in the circuit.

Placement is the process which will place the cells on the floorplan rows. 

Clock Tree Synthesis is the process of creating a clock distribution network to deliver the clock to all sequential elements.

Routing is the process which will create routing guides to implement the actual wiring.

