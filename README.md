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

### OpenLANE ASIC FLOW

OpenLANE flow performs full ASIC implementation steps from RTL all the way down to GDSII.OpenLANE flow consists of several stages which again consists of multiple sub-stages. 
It is started as an Open-source flow for a true open source tape-out experiment. It has two modes of Operation Interactive and Autonomous. It has Design Space Exploration which will find the best set of flow configuration from a large number of designs. Design exploration Utility is also used for regression testing. DFT is used for Scan insertion, Test pattern compaction, ATPG, etc.,. Physical Implementation is also called Automated PnR. Logic Equivalence Check is used to formally confirm that the function didn't change after modifying the netlist.

![](images/102.png)

The tools and flow which are used in the openlane Flow for the process is mentioned below.

1. Synthesis
  - yosys - Performs RTL synthesis
  - abc - Performs technology mapping
  - OpenSTA - Pefroms static timing analysis on the resulting netlist to generate timing reports
  
2. Floorplan and PDN
  - init_fp - Defines the core area for the macro as well as the rows (used for placement) and the tracks (used for routing)
  - ioplacer - Places the macro input and output ports
  - pdn - Generates the power distribution network
  - tapcell - Inserts welltap and decap cells in the floorplan
  
3. Placement
  - RePLace - Performs global placement
  - Resizer - Performs optional optimizations on the design
  - OpenPhySyn - Performs timing optimizations on the design
  - OpenDP - Perfroms detailed placement to legalize the globally placed components
  
4. CTS
  - TritonCTS - Synthesizes the clock distribution network (clock tree)
  
5. Routing 
  - FastRoute - Performs global routing to generate a guide file for the detailed router
  - TritonRoute - Performs detailed routing
  - SPEF-Extractor - Performs SPEF extraction
  
6. GDSII Generation
  - Magic - Streams out the final GDSII layout file from the routed def
  
7. Checks
  - Magic - Performs DRC Checks & Antenna Checks
  - Netgen - Performs LVS Checks


### Skywater Files

The SkyWater Open Source PDK is a collaboration between Google and SkyWater Technology Foundry to provide a fully open source Process Design Kit and related resources, which can be used to create manufacturable designs at SkyWater’s facility.
Process Design Kit (PDK) which is a collection of files used to model a fabrication process for the EDA tools to produce an IP.

The Skywater PDK files we are working with are described under ~/PDKS. There are three subdirectories needed for the workshop:
  -  Skywater-pdk – PDK which are related to foundary.
  -  Open_pdks – Contains scripts that are used to bridge the gap between closed-source and open-source PDK to EDA tool compatibility
  -  Sky130A – PDK files which are open-source compatible.
  
 ![](images/107.png) 
  
Inside Sky130A there will be two files which are related to process specific files and tool specific files

![](images/103.png)

libs.ref Contains process specific files 
  - (EX:) sky130_fd_sc_hd ; sky130 represent process name, fd represent foundary name (skywater) , sc represent for standard cell, hd represent for high density.
  
![](images/104.png)

libs.tech Contains files specific to tools such as Magic, ngspice etc.,.


![](images/106.png)

### Design preparation

Before starting the flow we have to check required inputs are placed in the respective folder to run properly. All the designs are placed under ~/openlane_flow_designs/. We have to check the /designs folder to get the required block for our flow. Within the Chosen design we can see the source files and configuration files.

![](images/109.png)

Source files (/src folder) will contain verilog files and sdc constraint files. Configuration files contain design's configuration file for running the flow. 

![](images/108.png)
<h3 align="center">config.tcl</h3>

