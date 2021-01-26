# Advanced Physical Design Workshop Using OPENLANE/SKY130

<!-- Workshop Logo -->
<br />
<p align="center">

  ![](/images/advanced_physical_design.png)

  <h3 align="left">Advanced Physical Design Workshop - OPENLANE/SKY130</h3>
</p>



<!-- INDEX -->
<details open="open">
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-workshop">About The Workshop</a>
    </li>
    <li>
      <a href="#day-1-commencement-of-open-source-eda">Day-1 Commencement of Open Source EDA</a>
      <ul>
        <li><a href="#calling-openlane">Calling OpenLANE</a></li>
        <li><a href="#package-importing">Package Importing</a></li>
        <li><a href="#design-folder">Design Folder</a></li>
        <li><a href="#design-folder-hierarchy">Design Folder Hierarchy</a></li>
        <li><a href="#prepare-design">Prepare Design</a></li>
        <li><a href="#synthesis">Synthesis</a></li>
      </ul>
    </li>


<!-- About the Workshop -->
## About The Workshop

This is the advanced physical design workshop which mainly focuses on the RTL2GDS flow using OpenLane/Sky130. In this workshop, we go through each and every step of a physical design flow i.e. synthesis, floorplanning, placement, clock tree synthesis, routing and static timing analysis.

OpenLane is a fully-automated RTL2GDS flow which includes several components i.e. OpenRoad, Magic, Yosys, Fault, Netgen etc. This tool is started for true open source tape-out experience with the goal to produce clean GDSII without any human intervention. 


<!-- Day-1 Commencement of Open Source EDA -->
## Day-1 Commencement of Open Source EDA

### Invoking OpenLane

![](/images/2.png)
  - Open terminal and change directory to work/tools/openlane_working_dir/openLANE_flow
  - List the contents of the openLANE_flow folder by using 'ls -ltr'
  - Then type './flow.tcl -interactive' which runs the OPENLANE flow
  - There are two modes to run OpenLane i.e. interactively and autonomous mode
  - '-interactive' is used here to run the flow.tcl script in interactive mode 
   

### Package Importing
To import the packages into the OpenLane tool we run the following command: 

![](/images/3.png)

### Design Folder
There are lots of design available in the OpenLane which are extracted from the openlane_flow/designs folder:

![](/images/4.png)

### Design Folder Hierarchy

![](/images/5.png)

Each design hierarchy contains two different components i.e. src folder and config.tcl files. Src folder consists of verilog files and SDC constraints files whereas config.tcl file contains the design configuration switches which is used by OpenLane. 

An example of a configuration file is given:

  ![](/images/6.png)

### Prepare Design
Now, we prepare our design. So, to prepare our design we used the command called as "prep". It is used to make the file structure for our design. We also build a tag with the prep command shown below:

  ![](/images/7.png)

Once the preparation is complete, go to the openlane_flow/design/picorv32a folder and you'll see one more directory called as trial_run1 is created under the runs folder, shown below:

  ![](/images/8.png)


### Synthesis

To run synthesis just type "run_synthesis" command inside the OpenLane tool:

  ![](/images/10.png)
  
  
<!-- Day 2 Chip Floorplanning and Standard Cells-->
##  Day 2 Chip Floorplanning and Standard Cells

### Aspect Ratio and Utilization Factor

Utilization factor is defined as the ratio of total area occupied by the netlist and total area of the core. If the utilization factor comes out to be 1, then the utilization of the core is 100% and no area left out for the placement of other cells or buffers. So, we usually go for 50% or 60% utilization because if there is some need of buffering the clock tree then there would be enough space to place some buffres on the chip.

Aspect ratio is defined as the height of the core divided by the width of the core. Aspect ratio signifies that the chip is of square shape or of rectange shape. If aspect ratio comes out to be 1, then the chip is of square shape and if the aspect ratio is other than 1, then the chip is of rectangle shape.

### Preplaced Cells

Preplaced cells are nothing but the macros or IP's which is a piece of complex logic that can be reused mutiple times onto a chip. Some examples of preplaced cells are memory, clock-gating cells, comparator, multiplexer etc. We placed the preplaced cells onto a floorplan ensuring that no standard cells are mapped where the preplaced cells are located.

### Decoupling Capacitors

Decoupling capacitor is a huge capacitor which is completely filled with charge and this capacitor take their charge from the main power supply. So, if the power supply is of 5V, then the decoupling capacitor charged till 5V. So, when the circuit switches, it gets its power supply or it gets its current from the decoupling capacitor. It basically decouples the circuit from the main power supply.   

### Power Planning

Power planning is a step in which we create multiple sources of power supply. For example, if we have a 8-bit bus whose values are 11001010 and this 8-bit bus is connected to an inverter. So, when all the logic 1 discharged to logic 0 through a simple ground tap point, then this will cause a ground bounce. In the other case, when all the logic 0 charged to logic 1 through a simple Vdd tap point, then this will cause a voltage droop. All this happened because of the single Vdd and ground. So, instead of a single power supply, we will have multiple power supplies i.e. we have multiple Vdd and Vss lines.

### Pin Placement and Logical Cell Placement Blockage

Pin placement is a step in which we place the IO pins in the area between core and die. Pin placement uses the netlist information to find the appropriate location for a pin to be placed between core and die. After pin placement we place a blockage in the area between core and a die which ensures that there will be no logic cells accidently placed in this area. 

### Floorplanning with OpenLANE

To run floorplan in OpenLANE:

  ![](/images/11.png)

As with all other stages, the floorplanning will be run according to configuration settings in the design specific config.tcl file. The output the the floorplanning phase is a DEF file which describes core area and placement of standard cell SITES:

  ![](/images/12.png)

### Viewing Floorplan in Magic
To view our floorplan in Magic we need to provide three files as input:

  1. Magic technology file (sky130A.tech)
  2. Def file of floorplan
  3. Merged LEF file

  ![](/images/13.png)
    
  ![](/images/14.png)


### Placement

The next step after floorplanning is placement. In this step, we place the logical cells i.e. flip-flop, AND gate etc. on the chip where we find the appropriate location. After running floorplanning in the OpenLane, we run the placement using "run_placement" command.

To do placement in OpenLANE:

  ![](/images/15.png)


### Viewing Placement in Magic

To view placement in Magic the command mirrors viewing floorplanning:

  ![](/images/17.png)
  
  ![](/images/18.png)

### Standard Cell Design Flow

Cell design flow is done in 3 parts:

  A. Inputs - PDKs (Process design kits), DRC & LVS rules, SPICE models, library & user-defined specs.
  B. Design Steps - Circuit Design, Layout Design, Characterization
  C. Outputs - CDL (Circuit Description Language), GDSII, LEF, extracted Spice netlist (.cir), timing, noise, power.libs, function.


<!-- Day 3 Design Library Cell -->
## Day 3 Design Library Cell

### Layout of an Inverter using Magic

To invoke the Magic we use the following command:

  ![](/images/20.png)

Below we'll see the layout of an inverter in magic:

  ![](/images/21.png)

### Device Conjecture

To know the layer/device onto the layout you just need to hover over the object and press s until you select the object which you want to select and then run the what command in the tkcon window.

![](/images/22.png)

### Parasitics Extraction with Magic

To extract the parasitics with magic first you need to run the below command in the tkcon window:

![](/images/27.png)

Once the extracted file is generated we need to run the below command to output the .ext file to a spice file:

![](/images/28.png)

![](/images/29.png)

### Spice Simulation using ngspice

SPICE file created from sky130_inv.ext - technology:

![](/images/30.png)

Now, we have to run the simulation with ngspice and to do so we have to invoke the ngspice tool with a spice file as an input:

![](/images/31.png)

We are the plotting the output i.e. y vs time while sweeping the input i.e. a:

![](/images/32.png)

