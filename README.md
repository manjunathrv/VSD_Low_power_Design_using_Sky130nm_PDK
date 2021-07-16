# VSD Low power Design using Sky130nm PDK Workshop


Table of contents
=================
<!--ts-->
   * [Day 1](https://github.com/manjunathrv/VSD_Advanced_Physical_Design_with_sky130nmPDK#day-1)
      * [Introduction to Low Power Design](https://github.com/manjunathrv/VSD_Advanced_Physical_Design_with_sky130nmPDK#introduction-to-physical-design-flow)
      * [Background](https://github.com/manjunathrv/VSD_Advanced_Physical_Design_with_sky130nmPDK#introduction-to-openlane-flow)
      
   * [Day 2](https://github.com/manjunathrv/VSD_Advanced_Physical_Design_with_sky130nmPDK#day-2)
      * [Low Power fundamentals](https://github.com/manjunathrv/VSD_Advanced_Physical_Design_with_sky130nmPDK#design-prepartion-and-synthesis-flow)
      * [Voltage Control techniques](https://github.com/manjunathrv/VSD_Advanced_Physical_Design_with_sky130nmPDK#design-prepartion-and-synthesis-flow)
   
   * [Day 3](https://github.com/manjunathrv/VSD_Advanced_Physical_Design_with_sky130nmPDK#day-3)
      * [IO placement modification](https://github.com/manjunathrv/VSD_Advanced_Physical_Design_with_sky130nmPDK#vsd-cmos-inverter-cell)
      * [VSD CMOS Inverter Cell](https://github.com/manjunathrv/VSD_Advanced_Physical_Design_with_sky130nmPDK#vsd-cmos-inverter-cell)
      * [Spice simulation of the VSD CMOS Inverter Cell](https://github.com/manjunathrv/VSD_Advanced_Physical_Design_with_sky130nmPDK#spice-simulation-of-the-vsd-cmos-inverter-cell)
   	
   * [Day 4](https://github.com/manjunathrv/VSD_Advanced_Physical_Design_with_sky130nmPDK#day-4)
      * [Extracting LEF file from the VSD Standard inverter cell](https://github.com/manjunathrv/VSD_Advanced_Physical_Design_with_sky130nmPDK#extracting-lef-file-from-the-vsd-standard-inverter-cell)
      * [Floorplan with VSD Standard inverter cell](https://github.com/manjunathrv/VSD_Advanced_Physical_Design_with_sky130nmPDK#floorplan-with-vsd-standard-inverter-cell)
      * [Timing analysis using OPENSTA](https://github.com/manjunathrv/VSD_Advanced_Physical_Design_with_sky130nmPDK#timing-analysis-using-opensta)
      * [Clock Tree synthesis](https://github.com/manjunathrv/VSD_Advanced_Physical_Design_with_sky130nmPDK#clock-tree-synthesis)
 
   * [Day 5](https://github.com/manjunathrv/VSD_Advanced_Physical_Design_with_sky130nmPDK#day-5)
      * [Placement](https://github.com/manjunathrv/VSD_Advanced_Physical_Design_with_sky130nmPDK#placement)
      * [Routing](https://github.com/manjunathrv/VSD_Advanced_Physical_Design_with_sky130nmPDK#routing)
      * [GDS II generation](https://github.com/manjunathrv/VSD_Advanced_Physical_Design_with_sky130nmPDK#gds-ii-generation)
  
   * [Workshop Learning Outcomes](https://github.com/manjunathrv/VSD_Advanced_Physical_Design_with_sky130nmPDK#workshop-learning-outcomes)

   * [Acknowledgement](https://github.com/manjunathrv/VSD_Advanced_Physical_Design_with_sky130nmPDK#acknowledgements)

<!--te-->

# Day 1 

## Introduction to Low power Design
### Definitions 

| Power                          | Energy                |
|--------------------------------|-----------------------|
| Instantaneous draw - V* I                                  | Total power draw over time <a href="https://www.codecogs.com/eqnedit.php?latex=\sum&space;V*I*t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sum&space;V*I*t" title="\sum V*I*t" /></a>  |
| Requirement -  deliver I at V and $\Delta$I at V          | Depends on the available capacity of the power source  |
| Heat generated | Form factor and size of the battery  |

### Impact 
| Increasing Power Consumption   | Increasing Energy Consumption  |
|--------------------------------|-----------------------|
| Heat generated in the IC/system increases | Finite packed resource depletes faster |
| Requirement of better heat sink/fan       | Cost increases with energy consumption  |
| Frequency gets capped resulting in decrease in performance | Systemic Metric  |
| Material degradation ||

### Economics of Power/Energy 
The power and energy consumption in an IC or a system impacts the complete economics of the product. The factors affected are mentioned below, 

1. Performance
2. Cost 
3. Weight
4. Form factor
5. Overall functinality
6. Safety 
7. Usage of the system (Portable or mobile)


### Power vs Perfomance 
In the below example, a case study is done to know if the improvement of performance can lead to increase or decrease in power consumption. 


### Comparison between systems - Portable, Mobile and Mobility  
| Portable                          | Mobile                | Mobility |
|--------------------------------|-----------------------|----------------|
| Heat generated in the IC/system increases | Finite packed resource depletes faster | Finite packed resource depletes faster |
| Requirement of better heat sink/fan       | Cost increases with energy consumption  | Finite packed resource depletes faster |
| Frequency gets capped resulting in decrease in performance | Systemic Metric  | Finite packed resource depletes faster |                           

### Assignment 
1. Case study 1 


2. Case study 2 


3. Case study 3 


## Background
Basic concepts are refreshed 

| Parameter   | Definition                |
|--------------------------------|-----------------------|
| Voltage | Measure of the electric field or force  |
| Current | Rate of flow of charges under an electric field |
|R,L and C | That impedes the current or changes the state of Voltage |

### CMOS operational regions 
<img src="Images/Day_1_1a.png" width="600"> <br/> 

The different operating conditions in a CMOS combinational and sequential circuit based on the rise and fall time are mentioned below, 

| Parameter   | Combinational Logic | Sequential Logic |
|--------------------------------|-----------------------|
| Shutdown | OFF | OFF |
| Standby  | ON  | Reads are allowed no writes |
| Active  | ON | Read and write are allowed |

### 7 degrees of Voltage Control in a CMOS device
The below figure is an example of a CMOS inverter with nodes that can be used for a low power design 

<img src="Images/Day_1_1a.png" width="600"> <br/> 

| Name   | Nodes |
|--------------------------------|-----------------------|
| Power gating  | SLPP, SLPN |
| Voltage scaling  | VDD,VSS |
| Back Biasing  | VBBP,VBBN | 
| State Retention | VRET|

### Multi-Vdd Voltage control 

<img src="Images/Day_1_3.png" width="600"> <br/> 

| Name   | Nodes |
|--------------------------------|-----------------------|
| Power gating  | SLPP, SLPN |
| Voltage scaling  | VDD,VSS |
| Back Biasing  | VBBP,VBBN | 
| State Retention | VRET|

### Power design in some basic devices 

| Name   | Nodes |
|--------------------------------|-----------------------|
| Power gating  | SLPP, SLPN |
| Voltage scaling  | VDD,VSS |
| Back Biasing  | VBBP,VBBN | 
| State Retention | VRET|


# Day 2

## Introduction to Low power Design
### Definitions 



