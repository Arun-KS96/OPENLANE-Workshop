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

### Calling OpenLane

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
