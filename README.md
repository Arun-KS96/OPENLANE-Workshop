# Advanced Physical Design Workshop Using OPENLANE/SKY130

<!-- Workshop Logo -->
<br />
<p align="center">

  ![](/Figures/logo.png)

  <h3 align="left">Advanced Physical Design Workshop - OPENLANE/SKY130</h3>
</p>




<!-- INDEX -->
<details open="open">
  <summary>INDEX</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
    </li>
    <li>
      <a href="#day-1-commencement-of-open-source-eda">Day-1 Commencement of Open Source EDA</a>
      <ul>
        <li><a href="#invoking-openlane">Invoking OpenLANE</a></li>
        <li><a href="#package-importing">Package Importing</a></li>
        <li><a href="#design-folder">Design Folder</a></li>
        <li><a href="#design-folder-hierarchy">Design Folder Hierarchy</a></li>
        <li><a href="#prepare-design">Prepare Design</a></li>
        <li><a href="#synthesis">Synthesis</a></li>
      </ul>
    </li>
    <li>
    <a href="#day-2-chip-floorplanning-and-placement">Day-2 Chip Floorplanning and Placement</a>
      <ul>
        <li><a href="#utilization-factor-and-aspect-ratio">Utilization Factor and Aspect Ratio</a></li>
        <li><a href="#preplaced-cells">Preplaced Cells</a></li>
        <li><a href="#decoupling-capacitors">Decouping Capacitors</a></li>
        <li><a href="#power-planning">Power Planning</a></li>
        <li><a href="#pin-placement-and-logical-cell-placement-blockage">Pin Placement and Logical Cell Placement Blockage</a></li>
        <li><a href="#floorplanning-with-openlane">Floorplanning with OpenLane</a></li>
        <li><a href="#viewing-floorplan-in-magic">Viewing Floorplan in Magic</a></li>
        <li><a href="#placement">Placement</a></li>
        <li><a href="#viewing-placement-in-magic">Viewing Placement in Magic</a></li>
        <li><a href="#standard-cell-design-flow">Standard Cell Design Flow</a></li>
      </ul>
    </li>
    <li>
      <a href="#day-3-design-library-cell">Day-3 Design Library Cell</a>
      <ul>
        <li><a href="#layout-of-an-inverter-using-magic">Layout of an Inverter using Magic</a></li>
        <li><a href="#device-conjecture">Device Conjecture</a></li>
        <li><a href="#parasitics-extraction-with-magic">Parasitics Extraction with Magic</a></li>
        <li><a href="#spice-simulation-using-ngspice">Spice Simulation using ngspice</a></li>
      </ul>
    </li>  
    <li>
      <a href="#day-4-layout-sta-and-clock-tree-synthesis">Day-4 Layout STA and Clock Tree Synthesis</a>
      <ul>
        <li><a href="#lef-files-introduction">LEF Files Introduction</a></li>
        <li><a href="#standard-cell-pin-placement">Standard Cell Pin Placement</a></li>
        <li><a href="#writing-lef-in-magic">Writing LEF in Magic</a></li>
        <li><a href="#including-custom-cells-in-openlane">Including Custom Cells in OpenLane</a></li>
        <li><a href="#fixing-slack-violations">Fixing Slack Violations</a></li>
        <li><a href="#clock-tree-synthesis">Clock Tree Synthesis</a></li>
        <li><a href="#replace-the-cell-example">Replace the Cell Example</a></li>
        <li><a href="#post-cts-sta-analysis">Post-CTS STA Analysis</a></li>
      </ul>
    </li>
    <li>
      <a href="#day-5-final-steps-routing-and-spef-extraction">Day-5 Final Steps Routing and SPEF Extraction</a>
      <ul>
        <li><a href="#routing">Routing</a></li>
        <li><a href="#generate-power-distribution-network">Generate Power Distribution Network</a></li>
        <li><a href="#spef-extraction">SPEF Extraction</a></li>
      </ul>
    </li>
    <li><a href="#acknowledgements">Acknowledgements</a></li>
  </ol>
</details>



<!-- About the Project -->
## About The Project

This project is mainly focuses on the RTL2GDS flow using the open source EDA tool OpenLANE/Sky130. In this project, we go through each and every step of a physical design flow i.e. synthesis, floorplanning, placement, clock tree synthesis, routing, static timing analysis anf SPEF extraction.

OpenLANE is a fully-automated RTL2GDS flow which includes several components i.e. OpenRoad, Magic, Yosys, Fault, Netgen etc. This tool is started for true open source tape-out experience with the goal to produce clean GDSII without any human intervention. 



<!-- Day-1 Commencement of Open Source EDA -->
## Day-1 Commencement of Open Source EDA

### Invoking OpenLANE

![](/Figures/1.1.png)
  - Open terminal and change directory to _work/tools/openlane_working_dir/openLANE_flow_
  - List the contents of the openLANE_flow folder by using _ls -ltr_
  - Then type _./flow.tcl -interactive_ which runs the OPENLANE flow
  - There are two modes to run OpenLANE i.e. interactively and autonomous mode
  - _-interactive_ is used here to run the flow.tcl script in interactive mode 
   
### Package Importing
To import the packages into the OpenLANE tool we run the following command: 

![](/Figures/1.2.png)

### Design Folder
There are lots of design available in the OpenLANE which are extracted from the _openlane_flow/designs_ folder:

![](/Figures/1.3.png)

### Design Folder Hierarchy

![](/Figures/1.4.png)

Each design hierarchy contains two different components i.e. **src folder** and **config.tcl** files. Src folder consists of verilog files and SDC constraints files whereas config.tcl file contains the design configuration switches which is used by OpenLANE. 

An example of a configuration file is given below:

  ![](/Figures/1.5.png)

### Prepare Design
Now, we have to prepare our design. So, to prepare our design we used the command called as _prep_. It is used to make the file structure for our design. We also build a tag with the _prep_ command shown below:

  ![](/Figures/1.6.png)
  
Preparation is completed:

  ![](/Figures/1.8.png)

Once the preparation is complete, go to the _openlane_flow/design/picorv32a_ folder and you'll see one more directory called as _trial_run1_ is created under the runs folder, shown below:

  ![](/Figures/1.7.png)

### Synthesis

To run synthesis just type _run_synthesis_ command inside the OpenLANE tool:
  
  ![](/Figures/1.9.png)
  
Synthesis was successful:
  
  ![](/Figures/1.10.png)



<!-- Day-2 Chip Floorplanning and Placement-->
##  Day-2 Chip Floorplanning and Placement

Floorplanning is basically the process of placing the logical blocks or IP's on a silicon chip. We basically place the logical blocks inside the core area which is enclosed by a die and a die is nothing but a small semiconductor material sample on which the circuit is fabricated. Floorplanning consists of various steps:
1. Define width and height of a core and a die.
2. Define locations of pre-placed cells.
3. Surround pre-placed cells with the decoupling capacitors.
4. Power Planning
5. Pin Placement
6. Logical Cell Placement Blockage

### Utilization Factor and Aspect Ratio

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

  ![](/Figures/2.1.png)

In the figure below you see _picorv32a.floorplan.def_ file which describes the die area and placement of standard cell sites.

  ![](/Figures/2.2.png)
  
Floorplanning runs successfully:

  ![](/Figures/2.3.png)

### Viewing Floorplan in Magic

To view our floorplan in Magic we need to provide three files as input:

  * _Magic technology file (sky130A.tech)_
  * _Def file of floorplan_
  * _Merged LEF file_
  
Below we can see the floorplan layout in the MAGIC: 
    
  ![](/Figures/2.4.png)

### Placement

The next step after floorplanning is placement. In this step, we place the logical cells i.e. flip-flop, AND gate etc. on the chip where we find the appropriate location. After running floorplanning in the OpenLANE, we run the placement using **"run_placement"** command.

To do placement in OpenLANE:

  ![](/Figures/2.5.png)
  
Placement runs successfully:

  ![](/Figures/2.6.png)

### Viewing Placement in Magic

To view placement in Magic we use the following command:

  ![](/Figures/2.7.png)
  
This is _picorv32a_ placement layout in MAGIC:
  
  ![](/Figures/2.8.png)

### Standard Cell Design Flow

Cell design flow is done in 3 parts:

  * _Inputs - PDKs (Process design kits), DRC & LVS rules, SPICE models, library & user-defined specs._
  * _Design Steps - Circuit Design, Layout Design, Characterization_
  * _Outputs - CDL (Circuit Description Language), GDSII, LEF, extracted Spice netlist (.cir), timing, noise, power.libs, function._



<!-- Day-3 Design Library Cell -->
## Day-3 Design Library Cell

### Layout of an Inverter using Magic

To invoke the Magic we use the following command:

  ![](/Figures/3.1.png)

Below we'll see the layout of an inverter in magic:

  ![](/Figures/3.2.png)

### Device Conjecture

To know the layer/device onto the layout you just need to hover over the object and press **s** until you select the object which you want to select and then run the _what_ command in the tkcon window.

![](/Figures/3.3.png)

### Parasitics Extraction with Magic

To extract the parasitics with magic first you need to run the below command in the tkcon window:

![](/Figures/3.4.png)

Once the extracted file is generated we need to run the below command to output the .ext file to a spice file:

![](/Figures/3.5.png)

SPICE file created from *sky130_inv.ext* - technology:

![](/Figures/3.6.png)

### Spice Simulation using ngspice

Here, we do some modification in the sky130_inv.spice file by adding Vdd, Vss etc.

![](/Figures/3.7.png)

Now, we have to run the simulation with ngspice and to do so we have to invoke the ngspice tool with a spice file as an input:

![](/Figures/3.8.png)

We are the plotting the output i.e. y vs time while sweeping the input i.e. a:

![](/Figures/3.9.png)

**OUTPUT:**

![](/Figures/3.10.png)



<!-- Day-4 Layout STA and Clock Tree Synthesis -->
##  Day-4 Layout STA and Clock Tree Synthesis

Placement and Routing (PnR) is featured using an essence view of the GDS files generated by Magic. Metal and pin information are included in the abstract information.

### LEF Files Introduction

There are two types of LEF files, one is the **technology lef** and the other one is the **cell lef**:
  * _Technology LEF - It contains layer information, via information, and restricted DRC rules_
  * _Cell LEF - It contains the abstract information of standard cells_

![](/Figures/4.1.png)

Above you see a _tracks.info_ file which contains the offset and pitch information of different layers. In the fig. above you see, the metal1 layer the x or horizontal layer is at an offset of 0.17 and a pitch of 0.34. The metal2 layer the x is at an offset of 0.23 and a pitch of 0.46 and so on. 

### Standard Cell Pin Placement

Standard cell is cluster of transistors and interconnect structures that provides a storage function. Standard cell pin placement is necessary for the DRC free PnR flow.

To display the grid in magic we use the *grid* command:

![](/Figures/4.2.png)

You can see the grid boxes in the layout below:

![](/Figures/4.3.png)

### Writing LEF in Magic

To write the lef file we used the *write* command which generate the LEF output sky130_vsdinv.lef for cell_sky130_vsdinv:

![](/Figures/4.4.png)

sky130_vsdinv.lef file:

![](/Figures/4.5.png)

### Including Custom Cells in OpenLane

To include the new cells in OpenLANE we need to do some configuration:
  * _Characterize new cell for specified corners_
  * _Include cell level library file in top level library file_
  * _Now we configure the config.tcl file:_

  ![](/Figures/4.6.png)


  * _Overwrite trial_run1 to include new configuration switches:_
  
  ![](/Figures/4.7.png)

  * _Now we run two additional commands to include extra cell LEFs:_
  
  ![](/Figures/4.8.png)

### Fixing Slack Violations

Static timing analysis is a step which ensures that whether there is any timing violations in the ciruit or not. We check for the timing violations at each and every step of the physical design flow because if we don't and if there is any timing violations in the circuit, then it is very difficult for a STA engineer to solve that violation. There is a term called as slack in the STA which tells us that whether there is a violation in the circuit or not. If the slack comes out to be positive then we are good to go but if the slack comes out to be negative then there might be something wrong with our design.

Run the OpenSTA tool with the configuration file:

![](/Figures/4.9.png)

### Replace the Cell Example:

To improve the slack value we use the technique of upsizing the cell. To do the same we replace the downsize cells with the upsize cells:

![](/Figures/4.10.png)

After this we run the _report_checks_ command to check the slack value:

![](/Figures/4.11.png)

### Clock Tree Synthesis

After completing floorplan and standard cell placement in OpenLANE we are ready to run the clock tree synthesis.To run clock tree synthesis (CTS) in OpenLANE:

![](/Figures/4.12.png)

CTS runs successfully:

![](/Figures/4.13.png)

### Post-CTS STA Analysis

OpenLANE contains the OpenRoad application unified into its flow and the OpenRoad has OpenSTA unified into its flow. Therefore, we run the STA within OpenLANE by calling OpenRoad:

To call OpenRoad from OpenLANE you just run the below command inside the OpenLANE:

![](/Figures/4.14.png)

Now we have to read the .lef file and the .def file:

![](/Figures/4.15.png)

![](/Figures/4.16.png)

Now, we have to create .db file i.e. pico_cts.db and after that we have to read that .db file:

![](/Figures/4.17.png)

Now we have to read the verilog file, min and max library files, and the sdc file:

![](/Figures/4.18.png)



<!-- Day-5 Final Steps Routing and SPEF Extraction -->
##  Day-5 Final Steps Routing and SPEF Extraction

### Routing

After completing the clock tree synthesis and the static timing analysis we go for the routing. First we have the check the CURRENT_DEF:

![](/Figures/5.1.png)

Then, we run the routing in the OpenLANE:

![](/Figures/5.2.png)

Routing runs successfully:

![](/Figures/5.3.png)

### Generate Power Distribution Network

To generate the power distribution network (PDN) in OpenLANE:

![](/Figures/5.4.png)

PDN is generated:

![](/Figures/5.5.png)

### SPEF Extraction

SPEF stands for Standard Parasitics Exchange Format. Its an IEEE 1481-1999 format that's being used across tool vendors. So, once the routing stage is done and the power distritibution network is generated we will do the parasitics extraction to perform sign-off post-route STA analysis.

To run the SPEF extraction we use the following command:

![](/Figures/5.6.png)

Writing SPEF file is done:

![](/Figures/5.7.png)



<!-- ACKNOWLEDGEMENTS -->
## Acknowledgements
* Kunal Ghosh - Co-founder (VSD Corp. Pvt. Ltd)
* Nickson Jose - VSD VLSI Engineer
* Akurathi Radhika
* Praharsha 
