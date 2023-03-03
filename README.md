# VSD Mixed-signal PD Research Program

## Week 0 AIs 

This repository discusses Week 0 work (4.2.23 to 11.2.23) as part of VSD Mixed-signal PD Research Program

- [AI 1 Ubuntu Installation ](#ai-1-ubuntu-installation)
- [AI 2 Magic and SKY130 PDKs installation ](#ai-2-magic-and-sky130-pdks-installation)
- [AI 3 Pre-layout simulation of CMOS inverter using xschem and ngspice](#AI-3-Pre-layout-simulation-of-CMOS-inverter-using-xschem-and-ngspice)
- [AI 4 Post-layout simulation of CMOS inverter using Magic](#AI-4-Post-layout-simulation-of-CMOS-inverter-using-Magic)
- [AI 5 Enroll in FREE VSD-custom layout course](#ai-5-enroll-in-free-vsd-custom-layout-course)
- [AI 6 Pre-layout simulation of a function Fn using ngspice](#AI-6-Pre-layout-simulation-of-a-function-Fn-using-ngspice)
- [AI 7 Post-layout simulation of a function Fn using Magic and ALIGN](#AI-7-Post-layout-simulation-of-a-function-Fn-using-Magic-and-ALIGN)
- [AI 8 Update Week 0 Findings](#AI-8-update-week-0-findings)


# AI 1 Ubuntu Installation 

With a windows machine, Oracle virtual box 7 is installed (fig 1) with latest version of Ubuntu 22.04.1 LTS, 64 bit OS with 8 GB RAM, with 12th Gen Intel Core i5-1235Ux4 and 2.2 TB of hard-disk space as shown in fig 2.  

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/218107293-26693c31-e9a6-4b92-becd-c90a36c12655.png">
</p> 
<p align="center">
Fig 1. Oracle VM Virtual Box 7 
</p>

1. Latest version of Virtual Box can be installed from: https://www.virtualbox.org/wiki/Downloads
2. Note: Click on Windows hosts for Windows machine. 

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/218108179-aef04619-8f6e-468a-9bbc-1e5dce5818eb.png">
</p> 
<p align="center">
Fig 2. Ubuntu 22.04.1 window running using Oracle VM VirtualBox
</p>


1. Latest version of Ubuntu can be installed from: https://ubuntu.com/download/desktop
2. Download the latest LTS version of Ubuntu


# AI 2 Magic and SKY130 PDKs installation 

Magic and related open source softwares like xschem, skywater130 pdks are installed next and their installation steps are provided for reference: 

1. Basic command's to install before installing opensource softwares: 
2. Git install: sudo apt install git 
3. Make install: sudo apt install make
4. Some dependencies required to run Magic and xschem do not come preinstalled. Enter enter the following command line in your terminal to install:

```
sudo apt update && sudo apt install m4 tcsh csh libx11-dev tcl-dev tk-dev libcairo2-dev libncurses-dev libglu1-mesa-dev freeglut3-dev mesa-common-dev
libX11-6 libx11-der libxrender-dev libx11-xcb-dev libcairo2-dev tcl8.6-dev tk8.6-dev flex bison libxpm4 libxpm-dev
```
Links for above commands:
```
https://lootr5858.wordpress.com/2020/10/06/magic-vlsi-skywater-pdk-local-installation-guide/
http://repo.hu/projects/xschem/xschem_man/install_xschem.html
```

## Magic installation 

1. Magic is an open-source VLSI layout tool. It is the software tool for drawing layout.
2. Magic version 8.3 is the official current released version of the program
3. It can be downloaded from terminal window in Ubuntu. 
4. Installation steps are given below:

```
git clone git://opencircuitdesign.com/magic
sudo cd magic
sudo ./configure
sudo make
sudo make install
```

More information can be found at http://opencircuitdesign.com/magic/index.html

## Netgen

1. Netgen is a tool for comparing netlists, a process known as LVS, which stands for "Layout vs. Schematic"
2. It can be downloaded from terminal window in Ubuntu. 
3. Installation steps are given below:

```
git clone git://opencircuitdesign.com/netgen
cd netgen
sudo ./configure
sudo make
sudo make install
```
More information can be found at http://opencircuitdesign.com/netgen/index.html

## Xschem

1. Xschem is a schematic capture tool. 
2. It can be downloaded from terminal window in Ubuntu. 
3. Installation steps are given below:

```
git clone https://github.com/StefanSchippers/xschem.git xschem_git
sudo ./configure
sudo make
sudo make install
```
More info can be found at http://repo.hu/projects/xschem/index.html

## Ngspice

1. Ngspice is the open-source spice simulator for electric and electronic circuits.
2. It can be downloaded from terminal window in Ubuntu. 
3. Download ngspice-39 tarball ngspice-39.tar.gzfrom https://ngspice.sourceforge.io/download.html into the work directory. Install ngspice and all its dependicies using the following commands.

```
tar -zxvf ngspice-39.tar.gz 
cd ngspice-38
mkdir release
cd release
sudo apt-get install libxaw7-dev
sudo ../configure  --with-x --with-readline=yes --disable-debug
sudo make
sudo make install
```

Please note that to view the simulation graphs of ngspice, xterm is required and can be installed using.

```
sudo apt-get update
sudo apt-get install xterm
```

## SKY130 PDKs
1. Open_PDKs is distributed with files that support the Google/SkyWater sky130 open process description https://github.com/google/skywater-pdk. 
2. Open_PDKs will set up an environment for using the SkyWater sky130 process with open-source EDA tools and tool flows such as magic, qflow, openlane, netgen, klayout, etc.
3. It can be downloaded from terminal window in Ubuntu. 
4. Installation steps are given below:

```
git clone git://opencircuitdesign.com/open_pdks
open_pdks
sudo ./configure --enable-sky130-pdk
sudo make
sudo make install
```

## Verifiying the open_pdk installation

1. An initial working directory naming lab1_inverter can be made by copying the required files as follows:
2. Type the following commands in terminal. 

```
mkdir Lab1_inverter
cd Lab1_inverter
mkdir mag
mkdir netgen
mkdir xschem
cd xschem
cp /usr/local/share/pdk/sky130A/libs.tech/xschem/xschemrc .
cp /usr/local/share/pdk/sky130A/libs.tech/ngspice/spinit .spiceinit
cd ../mag
cp /usr/local/share/pdk/sky130A/libs.tech/magic/sky130A.magicrc .magicrc
cd ../netgen
cp /usr/local/share/pdk/sky130A/libs.tech/netgen//sky130A_setup.tcl .
```

## Checking if Magic is working with SKY130A pdks with the following command: 

```
sudo magic -T sky130A.tech
```

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/218125899-cc637b82-30fb-477a-b6ea-cfd99d72bd9f.png">
</p> 
<p align="center">
Fig 3. Invoking Magic tool with SKY130A pdk
</p>

## Checking if xschem is working with SKY130A pdks with the following command: 


```
~/lab1_inverter/work$ xschem 
```

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/218129862-7cbfe99b-49db-4d04-b7b3-010b1a106dc4.png">
</p> 
<p align="center">
Fig 4. Invoking xschem 
</p>


## Checking if ngspice is working with the following command: 

```
~/lab1_inverter$ ngspice 
```

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/218130956-055925f5-39c3-44ad-999c-b1a1f5d9c6fd.png">
</p> 
<p align="center">
Fig 5. Invoking ngspice
</p>


# AI 3 Pre-layout simulation of CMOS inverter using xschem and ngspice

## 3.1 DC Analysis of CMOS Inverter using xschem and ngspice

1. Create the schematic for inverter in Xschem. 
2. The TT_MODELS contain the process corner details for PMOS and NMOS. The contents of TT_MODELS will be

```
name= TT_MODELS
only_toplevel=true
format="tcleval( @value )"
value="
** opencircuitdesign pdks install
.lib $::SKYWATER_MODELS/sky130.lib.spice tt
"
spice_ignore=false
```

3. DC analysis is done by using the .dc command using code_shown.sym from components.

```
.dc Vin 0 1.8 0.01
.save all
```

The CMOS inverter schematic in xschem is shown in fig 6 below

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/218146702-aec053a0-221f-45e0-aa37-ff56168291f5.png">
</p> 
<p align="center">
Fig 6. CMOS Inverter schematic in xschem(VTC) 
</p>

4. Go to Options> Spice netlist to set the netlist option. 
5. Click on Netlist from the menu to generate a spice file for the schematic created. 
6. Click on Simulate to run the simulation, ngspice window opens up
7. Type plot V(Vout) V(Vin) and press enter 
8. Voltage-transfer characteristic(VTC) appears for the inverter as shown in fig 7

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/218148710-1940997e-73f5-468a-8f26-714772f4d841.png">
</p> 
<p align="center">
Fig 7. Pre Layout CMOS VTC curve
</p>

9. From the VTC, we calculate the values VIH, VOL, VIL and VOH 
10. They can be used to calculate noise margins level ( NML and NMH) of CMOS inverter.  

## 3.2 Transient Analysis of CMOS inverter

1. The transient analysis of the CMOS inverter can be obtained by adding .tran in the code_shown.sym block.
2. The schematic for the CMOS inverter is shown in fig 8 below 


<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/218152568-0286cf44-3091-4a89-aab6-9e926494058b.png">
</p> 
<p align="center">
Fig 8. CMOS Inverter schematic in xschem(Transient) 
</p>

3. Go to Options> Spice netlist to set the netlist option. 
4. Click on Netlist from the menu to generate a spice file for the schematic created.
5. Click on Simulate to run the simulation, ngspice window opens up
7. Type plot V(Vout) V(Vin) and press enter 
8. Transient characteristics i.e Vout vs time and Vin vs time appears for the inverter as shown in fig 9 


<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/218154741-9320f00c-d5ce-4c79-b69e-a237ecf61581.png">
</p> 
<p align="center">
Fig 9. Pre Layout CMOS transient curve
</p>


8. For more accurate estimation of propagation delay, the following changes were made to the inverter_trans.spice file: 
Vin Vin GND pulse(0 1.8 100ps 10ps 10ps 200ps 500ps)
.tran 1ps 600ps

9. To measure rise, fall and propagation delay times, .meas statements were added in spice file as shown in fig 10 below 

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/218188595-1abb8921-e09f-412e-bc4a-23094103b668.png">
</p> 
<p align="center">
Fig 11. Pre Layout CMOS inverter spice file
</p>


10. Timing parameters of CMOS inverter can be calculated from the graph shown in fig 11 as follows: 

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/218188082-1c288d6a-15d0-4735-9bb8-fbfe71b308df.png">
</p> 
<p align="center">
Fig 11. Pre Layout CMOS transient curve(Accurate) 
</p>

Rise time = time(@90 % of Vout) - time(@10% of Vout)

Fall time = time(@10 % of Vout) - time(@90% of Vout)

Cell Rise Delay = (time taken by output to rise to its 50% value - time taken by the input to fall to its 50% value)

Cell Rise Delay = (time taken by output to fall to its 50% value - time taken by the input to rise to its 50% value)

The timing parameters obtained from pre-layout simulations is tabulated below.

| Parameter    | Value| 
|----------|-----|
|Rise Time|15.45 ps|
|Fall Time|4.83 ps|
|High to Low Propagation Delay|7.18 ps|
|Low to High Propagation Delay|13.12 ps|
|Average Propagation Delay|10.15 ps|

# AI 4 Post-layout simulation of CMOS inverter using Magic

## Covered in Week 1

# AI 5 Enroll in FREE VSD-custom layout course

## Enrolled and completed 

# AI 6 Pre-layout simulation of a function Fn using ngspice

1. The following circuit (fig 12) is implemented using CMOS logic design style
2. Fn= [(B+D).(A+C)+E.F]'

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/218190524-c7462796-0ca6-4c34-9501-4e0a376bbedb.png">
</p> 
<p align="center">
Fig 12. Schematic of 6 input CMOS circuit
</p>

3. The netlist `fn_prelayout.spice` for the function **Fn** given can be written as

```
***Netlist description for prelayout simulation***
M1 3 a vdd vdd pmos W=2.125u L=0.25u
M2 2 b vdd vdd pmos W=2.125u L=0.25u
M3 4 d 2 2 pmos W=2.125u L=0.25u
M4 4 c 3 3 pmos W=2.125u L=0.25u
M5 out e 4 4 pmos W=2.125u L=0.25u
M6 out f 4 4 pmos W=2.125u L=0.25u

M7 out a 6 6 nmos W=2.125u L=0.25u
M8 out c 6 6 nmos W=2.125u L=0.25u
M9 out e 7 7 nmos W=2.125u L=0.25u
M10 6 b 0 0 nmos W=2.125u L=0.25u
M11 6 d 0 0 nmos W=2.125u L=0.25u
M12 7 f 0 0 nmos W=2.125u L=0.25u

cload out 0 10f

Vdd vdd 0 2.5
V1 a 0 0 pulse 0 2.5 0.1n 10p 10p 1n 2n
V2 b 0 0 pulse 0 2.5 0.2n 10p 10p 1n 2n
V3 c 0 0 pulse 0 2.5 0.3n 10p 10p 1n 2n
V4 d 0 0 pulse 0 2.5 0.4n 10p 10p 1n 2n
V5 e 0 0 pulse 0 2.5 0.5n 10p 10p 1n 2n
V6 f 0 0 pulse 0 2.5 0.6n 10p 10p 1n 2n

***Simulation commands***
.op
.tran 10p 4n


*** .include model file ***
.include my_model_file.mod
.end
```

4. To measure Rise and Fall time of the output, following lines are added to the `fn_prelayout.spice` netlist
```
.MEAS TRAN rise_time TRIG V(out) VAL=0.25 RISE=1 TARG V(out) VAL=2.25 RISE=1
.MEAS TRAN FALL_time TRIG V(out) VAL=2.25 FALL=1 TARG V(out) VAL=0.25 FALL=1
.save all
```

5. Run the ngspice simulation using the following commands
```
    $ngspice fn_prelayout.spice
```

```
    ngspice 42 -> run
    ngspice 43 -> plot out
```

6. The pre-layout transient output of function Fn using Ngspice is shown in fig 13 and ngspice command window shows the rise and fall time of output waveform as shown in fig 14 

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/218194403-915ebbe2-e076-49dc-a7d3-eddbea209b2e.png">
</p> 
<p align="center">
Fig 13. Pre-layout transient output of function Fn 
</p>


<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/218194844-9e10a6d0-f57c-40a8-aff1-1515d4c1683c.png">
</p> 
<p align="center">
Fig 14. Ngspice window terminal showing rise and fall time
</p>

# AI 7 Post-layout simulation of a function Fn using Magic and ALIGN
 
 ## 7.1 Post-layout simulation of a function Fn using Magic
 
1. Layout of function Fn is created in Magic with the help of Euler path and stick diagrams implemented as shown in fig 15 

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/218196820-2cdf78be-5ce8-4793-aac8-801003e8c866.png">
</p> 
<p align="center">
Fig 15. Layout of function Fn using Magic 
</p>

2. Next, we extract the netlist from the from the magic layout by typing these commands in tkcon 2.3 Main console ash shown in fig 16 

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/218197983-c86a84bd-32ca-4bbb-b0fc-b27302f47362.png">
</p> 
<p align="center">
Fig 16. function Fn Tkcon terminal 
</p>

3. The netlist `fn_postlayout.spice` generated is as shown below. 
4. The netlist shows the parasitic capacitances added with post layout simulation. 
5. Model file is same as the one used for pre-layout simulation.

```
***Netlist description for post-layout simulation***
* SPICE3 file created from fn_postlayout.ext - technology: min2
.option scale=0.09u
M1000 a_46_38# d a_22_38# vdd pmos w=17 l=2
+  ad=102 pd=46 as=204 ps=92
M1001 out c a_14_9# gnd nmos w=17 l=2
+  ad=204 pd=92 as=204 ps=92
M1002 vdd b a_46_38# vdd pmos w=17 l=2
+  ad=204 pd=92 as=0 ps=0
M1003 gnd f a_30_9# gnd nmos w=17 l=2
+  ad=204 pd=92 as=102 ps=46
M1004 gnd b a_14_9# gnd nmos w=17 l=2
+  ad=0 pd=0 as=0 ps=0
M1005 out e a_22_38# vdd pmos w=17 l=2
+  ad=102 pd=46 as=0 ps=0
M1006 a_14_38# a vdd vdd pmos w=17 l=2
+  ad=102 pd=46 as=0 ps=0
M1007 a_14_9# a out gnd nmos w=17 l=2
+  ad=0 pd=0 as=0 ps=0
M1008 a_30_9# e out gnd nmos w=17 l=2
+  ad=0 pd=0 as=0 ps=0
M1009 a_22_38# f out vdd pmos w=17 l=2
+  ad=0 pd=0 as=0 ps=0
M1010 a_22_38# c a_14_38# vdd pmos w=17 l=2
+  ad=0 pd=0 as=0 ps=0
M1011 a_14_9# d gnd gnd nmos w=17 l=2
+  ad=0 pd=0 as=0 ps=0
C0 a_30_9# gnd 3.37fF
C1 a_14_9# gnd 6.82fF
C2 out gnd 8.40fF
C3 a_22_38# gnd 3.02fF
C4 vdd gnd 9.58fF

Vdd vdd 0 2.5
V1 a 0 0 pulse 0 2.5 0.1n 10p 10p 1n 2n
V2 b 0 0 pulse 0 2.5 0.2n 10p 10p 1n 2n
V3 c 0 0 pulse 0 2.5 0.3n 10p 10p 1n 2n
V4 d 0 0 pulse 0 2.5 0.4n 10p 10p 1n 2n
V5 e 0 0 pulse 0 2.5 0.5n 10p 10p 1n 2n
V6 f 0 0 pulse 0 2.5 0.6n 10p 10p 1n 2n

***Simulation commands***
.op
.tran 10p 4n

*** .include model file ***
.include  my_model_file.mod
.end
```
6. To measure Rise and Fall time of the output, following lines are added to the `fn_postlayout.spice` netlist
```
.MEAS TRAN rise_time TRIG V(out) VAL=0.25 RISE=1 TARG V(out) VAL=2.25 RISE=1
.MEAS TRAN FALL_time TRIG V(out) VAL=2.25 FALL=1 TARG V(out) VAL=0.25 FALL=1
.save all
```

7. Run the ngspice simulation using the following commands.
```
    $ngspice fn_postlayout.spice
```

```
    ngspice 44 -> run
    ngspice 45 -> plot out
```

8. The post-layout transient output of function Fn using Ngspice is shown in fig 17 and ngspice command window shows the rise and fall time of output waveform as shown in fig 18

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/218201312-59567d22-2203-49dd-8651-8b6d9ef8a203.png">
</p> 
<p align="center">
Fig 17. Post-layout transient output of function Fn Layout
</p>


<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/218201235-f05d6d8e-3a47-4b69-80d4-9c512c24cecf.png">
</p> 
<p align="center">
Fig 18. Ngspice window terminal showing rise and fall time(Post Layout) 
</p>

 ## 7.2 Comparison of Pre-layout and post-layout timing parameters of a function Fn 
 
| Parameter    | Value from Pre-layout Simulation| Value from Post-layout Simulation|
|----------|-----|-----|
|Rise Time|1.40 ns|0.11 ns|
|Fall Time|0.08 ns |0.17 ns|

## 7.3 LVS Check

1. The layout vs schematic compares the pre-layout netlist with the netlist extracted from the layout.
2.  The mismatch is due to the extra parasitic capacitances in the post-layout netlist. 
3.  The report `comp.out` is obtained using Netgen by typing the following command.

```
~/magic_experiments$ netgen -batch lvs fn_prelayout.spice fn_postlayout.spice
```
4. The content of the report is as shown in fig 19

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/218203927-42506bbc-e261-4c67-beb0-8f9c9d157d7b.png">
</p> 
<p align="center">
Fig 19. LVS for function Fn
</p>


# AI 8 Update Week 0 Findings

It can be seen that except for 4 extra devices(Capacitances) and corresponding nets, the pre-layout netlist and the post-layout of function using min2.tech extracted netlist are same.
 
 
# VSD Mixed-signal PD Research Program

## Week 1 AIs 

This repository discusses Week 1 work (12.2.23 to 19.2.23) as part of VSD Mixed-signal PD Research Program
 
- [AI 9 ALIGN Installation](#AI-9-ALIGN-Installation)
- [AI 10 Post-layout simulation of CMOS inverter using ALIGN](#AI-10-Post-layout-simulation-of-CMOS-inverter-using-ALIGN)
- [AI 11 Comparing AI 5 and 6](#AI-11-Comparing-AI-5-and-6)
- [AI 12 Enroll in FREE VSD-custom layout course](#AI-12-Enroll-in-FREE-VSD-custom-layout-course)
- [AI 13 Pre-layout of function using xschem and ngspice using SKY130 PDKS](#AI-13-Pre-layout-of-function-using-xschem-and-ngspice-using-SKY130-PDKS)
- [AI 14 Post-layout of function using magic and ngspice using SKY130 PDKS](#AI-14-Post-layout-of-function-using-magic-and-ngspice-using-SKY130-PDKS)
- [AI 15 Post-layout simulation of function using ALIGN](#AI-15-Post-layout-simulation-of-function-using-ALIGN)
- [AI 16 Compare AI 14 and 15](#AI-16-Compare-AI-14-and-15) 
- [AI 17 Update Week 1 findings](#AI-17-Update-Week-1-findings)

# AI 9 ALIGN Installation 

1. ALIGN is Analog Layout, Intelligently Generated from Netlists.
2. ALIGN is an open source automatic layout generator for analog circuits jointly developed under the DARPA IDEA program by the University of Minnesota, Texas A&M University, and Intel Corporation.
3. The goal of ALIGN (Analog Layout, Intelligently Generated from Netlists) is to automatically translate an unannotated (or partially annotated) SPICE netlist of an analog circuit to a GDSII layout.
4. ALIGN is installed next, with installation steps as given below: 

```
export CC=/usr/bin/gcc
export CXX=/usr/bin/g++

# Clone the ALIGN source
    git clone https://github.com/ALIGN-analoglayout/ALIGN-public
    cd ALIGN-public
# Install virtual environment for python
    sudo apt -y install python3.8-venv
# Install the latest pip
    sudo apt-get -y install python3-pip

# Create a Python virtualenv
    python -m venv general
    source general/bin/activate
    python -m pip install pip --upgrade

# Install ALIGN as a USER
    pip install -v .

# Install ALIGN as a DEVELOPER
    pip install -e .
    pip install setuptools wheel pybind11 scikit-build cmake ninja
    pip install -v -e .[test] --no-build-isolation
    pip install -v --no-build-isolation -e . --no-deps --install-option='-DBUILD_TESTING=ON'
```

Making ALIGN Portable to Sky130 tehnology. Clone the following Repository inside ALIGN-public directory
```
git clone https://github.com/ALIGN-analoglayout/ALIGN-pdk-sky130
```

Move SKY130_PDK folder to home/inderjit/ALIGN-public/pdks. Everytime we start the tool in new terminal, run the following commands.

```
# Running ALIGN TOOL
python3 -m venv general
source general/bin/activate
```
Commands to run ALIGN (goto ALIGN-public directory)
```
mkdir work
cd work
```

General syntax to give inputs

```
schematic2layout.py <NETLIST_DIR> -p <PDK_DIR> -c
EXAMPLE 1:
schematic2layout.py ../examples/telescopic_ota -p ../pdks/FinFET14nm_Mock_PDK/
EXAMPLE 2:
schematic2layout.py ../ALIGN-pdk-sky130/examples/five_transistor_ota -p ../pdks/SKY130_PDK/
```

## Inverter Post-layout From Align 

1. To make the layout using align tool
a) Create a work directory in ALIGN-public folder.
b) Make sure you have the inv_tb.spice file (created from lvs netlist in xschem) in that folder by copying that file and rename it to .sp as ALIGN only reads .sp files
c) Contents of inv_tb.spice is Shown below in figure 9.1

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/221291409-28ceec9f-fc4c-4627-a44f-f0746135cb86.png">
</p> 
<p align="center">
Fig 9.1 CMOS inverter lvs netlist in xschem
</p>

d) Contents of inv.sp is Shown below in figure 9.1

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/221292062-d32af21f-fa03-40f8-a1f5-ceec4a5d52a8.png">
</p> 
<p align="center">
Fig 9.2 inv.sp file within ALIGN-public folder
</p>

d) Next, use the following command to make it work

``` python3 ../bin/schematic2layout.py (your .spice file name here) -p ../pdks/SKY130_PDK/ ```

e) After running the command successfully you will see that a GDS file is created your terminal window would look as shown in Fig 9.3


<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/221296007-056fdde6-8ba8-4eb3-be38-60bbfe207721.png">
</p> 
<p align="center">
Fig 9.3 .GDS generated for Inverter using ALIGN  
 
f) We next can view ALIGN Generated .gdb and .lef in ``klayout`` as show in fig 9.4 and 9.5

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/221303884-557f7088-ffce-4e33-bb05-b3265ebc4e0e.png">
</p> 
<p align="center">
Fig 9.4 Inverter .gds file open in klayout
    
<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/221303921-69351666-2294-4aca-8b23-da25099b8b9f.png">
</p> 
<p align="center">
Fig 9.5 Inverter .lef file open in klayout

g) Next, we open GDS file. To open this .gds file you need to run magic first using the magic commands as 

``` magic -T sky130A.tech ```

h) Next go to file menu in Magic-> Click on read gds -> Select your .gds file

i) You will get box with black boundaries, do not panic just press s and then x your layout will be displayed like shown in fig 9.6

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/221298079-6cfabe3a-40ed-4aef-8000-9ac08812e2e8.png">
</p> 
<p align="center">
Fig 9.6 ALIGN Inverter layout
</p>

j) Next we need to run post layout spice simulation, so go to tkcon window and type the following command as shown in fig 9.7

```
extract do local
extract all
ext2spice cthresh 0 rthresh 0
ext2spice
```

<p align="center">
<img src="inverter align 5 tkcon" src="https://user-images.githubusercontent.com/99788755/221316225-c88d6148-0028-4ce7-b72b-a239095975f9.png">
</p> 
<p align="center">
Fig 9.7 Tkcon terminal for inverter
</p>



# AI 10 Post-layout simulation of CMOS inverter using ALIGN

1. Take the .spice file generated from ALIGN layout and paste it in our testbench spice file.

2. PostLayout extracted netlist is shown in fig 9.8 and postlayout netlist with control statements and sources is shown in fig 9.9

<p align="center">
<img src="inverter align 5 tkcon" src="https://user-images.githubusercontent.com/99788755/221314363-f3a9bddf-2142-4bee-a5fe-65ca6cdfe2a2.png">
</p> 
<p align="center">
Fig 9.8 PostLayout extracted netlist for inverter
</p>

<p align="center">
<img src="inverter align 8 netlist postlayout" src="https://user-images.githubusercontent.com/99788755/221314386-c34e8d35-82b2-4db7-bceb-5b3c4517ac73.png"">
</p> 
<p align="center">
Fig 9.9 Tkcon terminal for inverter
</p>

3. Next we, simulate it by invoking ngspice with command ```ngspice filename.spice``` . The following waveform are obtained as shown in fig 9.10

4. To measure rise, fall and propagation delay times, .meas statements were added in postlayout spice file. 

5. Timing parameters of CMOS inverter can be calculated from the graph shown in fig 9.10 as follows: 

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/221309852-dab7b0bb-047f-4956-a3bf-93cf07bf45fe.png">
</p> 
<p align="center">
Fig 9.10 Post Layout CMOS inverter output with delays measurement
</p>

6. The timing parameters obtained from post-layout simulations of CMOS inverter with ALIGN are tabulated below.

| Parameter    | Value| 
|----------|-----|
|Rise Time|0.0106 ns|
|Fall Time|0.052 ns|
|High to Low Propagation Delay|0.03 ns|
|Low to High Propagation Delay|0.067 ns|
|Average Propagation Delay|0.048 ns|


# AI 11 Comparing AI 10 and 4

## Pre-schematic simulation of CMOS inverter(hierarchical approach) using xschem/ngspice 

## 11.1 Transient analysis of CMOS Inverter(hierarchical approach) using xschem and ngspice

1. In week 0, schematic of CMOS inverter was tested in xschem, but for post layout simulation in magic, hierarchical approach was adopted. 
2. Create the schematic for CMOS inverter schematic in Xschem as shown in fig 1

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/219781370-4b6b2825-d7a5-4c93-a718-ac4070216530.png">
</p> 
<p align="center">
Fig 1. CMOS inverter schematic in xschem
</p>

3. Next, we create the symbol from schematic as shown in fig 2

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/219783337-305c6d52-170a-4197-bea5-4bb02b56412d.png">
</p> 
<p align="center">
Fig 2. CMOS inverter symbol in xschem
</p>

4. Next, we create the testbench for CMOS inverter with input signals, control signals, supply signals and transient parameters as shown in fig 3

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/219783770-01db51fe-ad77-4685-b188-f3149fa0bdb7.png">
</p> 
<p align="center">
Fig 3. CMOS inverter testbench in xschem
</p>

5. Next, we extract netlist. Go to Options> Spice netlist to set the netlist option. 
4. Click on Netlist from the menu to generate a spice file for the schematic created.
5. Click on Simulate to run the simulation, ngspice window opens up
7. Type plot V(Vout) V(Vin) and press enter 
8. Transient characteristics i.e Vout vs time and Vin vs time appears for the inverter as shown in fig 4 

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/219786306-591c561f-25da-4fdc-a735-0b1bc9029f92.png">
</p> 
<p align="center">
Fig 4. Pre Layout CMOS transient output
</p>


9. To measure rise, fall and propagation delay times, .meas statements were added in spice file. 

10. Timing parameters of CMOS inverter can be calculated from the graph shown in fig 5 as follows: 

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/219786444-9a2e3d27-41cb-405a-b721-a7f5d553f1ed.png">
</p> 
<p align="center">
Fig 5. Pre Layout CMOS inverter output with delays measurement
</p>

The timing parameters obtained from pre-layout simulations of CMOS inverter are tabulated below.

| Parameter    | Value| 
|----------|-----|
|Rise Time|17.75 ps|
|Fall Time|5.68 ps|
|High to Low Propagation Delay|7.13 ps|
|Low to High Propagation Delay|13.35 ps|
|Average Propagation Delay|10.32 ps|

## 11.2 Post Layout Transient analysis of CMOS Inverter(hierarchical approach) using magic and ngspice

1. After prelayout simulations, post-layout simulation is performed for the function using Magic tool. 

2. First, the spice file for the function is imported in magic by invoking the following lines 'magic -T sky130A.tech in terminal. 

3. This extract's nfet and pfet devices along with input, output and supply pins. 

4. Next we interconnects and create the layout for CMOs inverter as shown in fig 6 


<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/219796916-e36bd433-8783-493b-93a4-e8b964e2a0f4.png">
</p> 
<p align="center">
Fig 6. Layout of CMOS inverter in Magic
</p>

5. With layout done, next we have to extract post layout netlist of CMOS inverter by rntereing the following commands in tkcon terminal. 

```
extract do local
extract all 
```

6. This will extract the parasitic present in postlayout of CMOS inverter as shown in the screenshot below in fig 7


<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/219798678-dd8f2c4a-1a64-4dc2-a8e6-924cb9eeb480.png">
</p> 
<p align="center">
Fig 7. Postlayout CMOS inverter netlist
</p>


7. New spice file is generated by magic. In the new spice file, input pulse, control statements are added. 

8. Next we, simulate it using ngspice. The following waveform is obtained as shown in fig 8

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/219798285-c7c3f1a9-3e0d-4af1-8d2f-d2e69ae1e96f.png">
</p> 
<p align="center">
Fig 8. Postlayout CMOS inverter output waveforms
</p>

9. To measure rise, fall and propagation delay times, .meas statements were added in postlayout spice file. 

10. Timing parameters of CMOS inverter can be calculated from the graph shown in fig 9 as follows: 

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/219798566-00223d7b-0995-42ea-9cee-0de8b05e88f2.png">
</p> 
<p align="center">
Fig 9. Post Layout CMOS inverter output with delays measurement
</p>

The timing parameters obtained from post-layout simulations of CMOS inverter are tabulated below.

| Parameter    | Value| 
|----------|-----|
|Rise Time|25.53 ps|
|Fall Time|7.78 ps|
|High to Low Propagation Delay|9.05 ps|
|Low to High Propagation Delay|18.96 ps|
|Average Propagation Delay|14 ps|


## 11.3 Comparison of Pre-layout and post-layout timing parameters of CMOS Inverter
 
| Parameter    | Value from Pre-layout Simulation| Value from Post-layout Simulation|
|----------|-----|-----|
|Rise Time|17.75 ns|25.53 ns|
|Fall Time|5.68 ns |7.78 ns|
|High to Low Propagation Delay|7.13 ns|9.05 ns|
|Low to High Propagation Delay|13.35 ns |18.96 ns|
|Average Propagation Delay|10.32 ns |14.01 ns|

1. The waveforms in fig 8 is similar to that of pre-layout simulation. However, there is a small delay in the waveform that might be caused due to parasitics in the layout. 

2. From above comparison table, its clearly visible that Postlayout delays are more than prelayout due to parasitics in postlayout of CMOS Inverter. 


## 1.4 LVS Check

1. The layout vs schematic compares the pre-layout netlist with the netlist extracted from the layout.
2.  The mismatch is due to the extra parasitic capacitances in the post-layout netlist. 
3.  The report `comp.out` is obtained using Netgen by typing the following command.

```
~/mag_inverter$ netgen -batch lvs inv_isd_post_test.spice inv_isd_test.spice
```
4. The content of the report is as shown in fig 10

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/219800495-3a5b0703-396f-4a97-8242-3a13784870a1.png">
</p> 
<p align="center">
Fig 10. LVS for CMOS Inverter
</p>


# AI 12 Enroll in FREE VSD-custom layout course

## Enrolled and completed



# AI 13 Pre-layout of function using xschem and ngspice using SKY130 PDKS

<img width="960" alt="fn_prelayout_schm" src="https://user-images.githubusercontent.com/99788755/219800768-3e4a7b6f-bf84-4c73-b492-1b5aa2aac930.png">

<img width="960" alt="fn_prelayout_output" src="https://user-images.githubusercontent.com/99788755/219800795-d560968e-6ff9-46d2-b804-09c733167f26.png">

<img width="960" alt="fn_prelayout_output_with_delays" src="https://user-images.githubusercontent.com/99788755/219800814-2351979b-b0ac-4a43-bf21-10612b751c16.png">

<img width="960" alt="tkcon_window_pre" src="https://user-images.githubusercontent.com/99788755/219800850-946b26ae-bc76-4490-a0a8-5a6759e418e5.png">


# AI 14 Post-layout of function using magic and ngspice using SKY130 PDKS

## 14.1 Fail try at Layout

<img width="960" alt="post_layout_complete_with_labels" src="https://user-images.githubusercontent.com/99788755/219801049-982a0488-2eb3-4919-8c88-b0d781af6c27.png">


## 14.2 Correct Layout for function 

<img width="960" alt="post_layout_complete_with_labels_final" src="https://user-images.githubusercontent.com/99788755/219801150-93c63031-ebf3-4839-89b4-74b6c6d199f9.png">

<img width="960" alt="fn_postlayout_output" src="https://user-images.githubusercontent.com/99788755/219801203-85b033a6-583e-4cd6-807b-8e941f8107c4.png">

<img width="960" alt="fn_postlayout_output_with_delays" src="https://user-images.githubusercontent.com/99788755/219801222-6b8c287d-817f-4bc9-96ef-0b73d26e3f30.png">


<img width="960" alt="tkcon_window_post" src="https://user-images.githubusercontent.com/99788755/219801246-f10142bb-bf73-4219-bb29-4ef564a35c8e.png">


<img width="960" alt="lvs_function" src="https://user-images.githubusercontent.com/99788755/219801257-9ab51d96-3a7a-4cc1-a5de-ca9b4c6f8d8f.png">


## 14.3 Comparison of Pre-layout and post-layout timing parameters of Fn
 
| Parameter    | Value from Pre-layout Simulation| Value from Post-layout Simulation|
|----------|-----|-----|
|Rise Time|10.84 ns|1.37 ns|
|Fall Time|46.9 ns |48.74 ns|
|High to Low Propagation Delay|13.1 ns|13.75 ns|
|Low to High Propagation Delay|44.33 ns |47.54 ns|
|Average Propagation Delay|28.71 ns |30.64 ns|

1. The postlab waveforms is similar to that of pre-layout simulation. However, there is a small delay in the waveform that might be caused due to parasitics in the layout. 

2. From above comparison table, its clearly visible that Postlayout delays are more than prelayout due to parasitics in postlayout of CMOS Inverter. 


# AI 15 Post-layout simulation of function using ALIGN

## in progress

# AI 16 Compare AI 14 and 15 

## in progress 

# AI 17 Update Week 1 findings

## 11.3 Comparison of Pre-layout and post-layout timing parameters of CMOS Inverter
 
| Parameter    | Value from Pre-layout Simulation| Value from Post-layout Simulation (MAGIC)| Value from Post-layout Simulation (ALIGN)|
|----------|-----|-----|----------|
|Rise Time|17.75 ns|25.53 ns| 0.1 ns|
|Fall Time|5.68 ns |7.78 ns| 0.05 ns|
|High to Low Propagation Delay|7.13 ns|9.05 ns| 0.03 ns|
|Low to High Propagation Delay|13.35 ns |18.96 ns| 0.067 ns| 
|Average Propagation Delay|10.32 ns |14.01 ns| 0.048 ns|



# Week 2 AIs

This section discusses Week 2 work (18.2.23 to 25.2.23) as part of VSD Mixed-signal PD Research Program
                                                                                                       
# 1. KLAYOUT Installation

Download the ‘.deb’ file from the KLayout homepage and install it, as shown below.
```bash
## Install KLayout
mkdir -p ~/Work/vlsi/tools/KLayout && cd ~/Work/vlsi/tools/KLayout
wget https://www.klayout.org/downloads/Ubuntu-22/klayout_0.27.11-1_amd64.deb
sudo apt install -y ./klayout_0.27.11-1_amd64.deb                           
```                  
                                                                                                                    
# 2. OpenROAD Installation
OpenROAD is an integrated chip physical design tool that takes a design from synthesized Verilog to routed layout.

An outline of steps used to build a chip using OpenROAD is shown below:

1. Initialize floorplan - define the chip size and cell rows
2. Place pins (for designs without pads )
3. Place macro cells (RAMs, embedded macros)
4. Insert substrate tap cells
5. Insert power distribution network
6. Macro Placement of macro cells
7. Global placement of standard cells
8. Repair max slew, max capacitance, and max fanout violations and long wires
9. Clock tree synthesis
10. Optimize setup/hold timing
11. Insert fill cells
12. Global routing (route guides for detailed routing)
13. Antenna repair
14. Detailed routing
15. Parasitic extraction
16. Static timing analysis


### A.  Run the below commands step by step to install OpenROAD and OpenROAD-flow-scripts

### B. Before you can go any further, you need to install some prerequisite software packages:

```bash
## Packages needed by OpenROAD
sudo apt install -y cmake qtbase5-dev qtchooser qt5-qmake qtbase5-dev-tools \
    libmng2 qt5-image-formats-plugins tcl-tclreadline \
    swig libboost-all-dev libeigen3-dev libspdlog-dev
## Build 'lemon' from source
cd ~/home/inderjit mkdir lemon && cd lemon
wget http://lemon.cs.elte.hu/pub/sources/lemon-1.3.1.tar.gz
tar -zxf lemon-1.3.1.tar.gz && cd lemon-1.3.1
cmake -B build .
sudo cmake --build build -j $(nproc) --target install
```
### C. Start installtion of OpenROAD by Running the below commands step by step in terminal. 

```bash
cd
git clone --recursive https://github.com/The-OpenROAD-Project/OpenROAD.git
cd OpenROAD
sudo ./etc/DependencyInstaller.sh
```

### D. Build all the tools needed for OpenROAD:

```bash
cd OpenROAD-flow-scripts
sudo ./build_openroad.sh --local
## This step can take over 30 minutes

export OPENROAD=~/OpenROAD-flow-scripts/tools/OpenROAD
export PATH=~/OpenROAD-flow-scripts/tools/install/OpenROAD/bin:~/OpenROAD-flow-scripts/tools/install/yosys/bin:~/OpenROAD-flow-scripts/tools/install/LSOracle/bin:$PATH
```

#### Building OpenROAD Locally 
```bash
./build_openroad.sh --local
source setup_env.sh
```

- You will see the following message:
```bash
OPENROAD: <path>/OpenROAD-flow-scripts/tools/OpenROAD
```

### E. In OpenROAD, facing the following configuration error while installation process for OpenROAD
                                                                                                              
![image](https://user-images.githubusercontent.com/99788755/221319637-dc4956e6-52ec-4668-80c1-f42f543cea80.png)

### F. The above error got resolved by re-running the commands in a new terminal 

<img width="960" alt="openroad testing" src="https://user-images.githubusercontent.com/99788755/222798513-cf6f7807-d385-4adc-9294-d94e6adec0bb.png">
                                                                                                               
# 4. OpenFASOC Installation
                         
- OpenFASoC is a project focused on automated analog generation from user specification to GDSII with fully open-sourced tools. It is led by a team of researchers at the University of Michigan and is inspired from FASoC which sits on proprietary software.

- The tool is comprised of analog and mixed-signal circuit generators, which automatically create a physical design based on user specifications.
 
 - To install the OpenFASoC use the following commands:
```bash
cd
git clone https://github.com/idea-fasoc/openfasoc
cd openfasoc
sudo ./dependencies.sh  
```

- First, cd into a directory of your choice and clone the OpenFASoC repository:
```git clone https://github.com/idea-fasoc/openfasoc```

- Now go to the home location of this repository (where the README.rst file is located) and ```run sudo ./dependencies.sh.```         

# 5. OpenFASoC: Temperature Sensor Generator
## Temperature Sensor Auxiliary Cells
this section gives an overview of how the Temperature Sensor Generator (temp-sense-gen) works internally in OpenFASoC.

## Temperature Sensor Generator Circuit
- This generator creates a compact mixed-signal temperature sensor based on the topology from this paper. It consists of a ring oscillator whose frequency is controlled by the voltage drop over a MOSFET operating in subthreshold regime, where its dependency on temperature is exponential.

![tempsense_ckt](https://user-images.githubusercontent.com/83899035/221102960-1f5c8fdc-b63d-4392-9e59-b25b74a0abce.png)

- The physical implementation of the analog blocks in the circuit is done using two manually designed standard cells:

1. HEADER cell, containing the transistors in subthreshold operation;

2. SLC cell, containing the Split-Control Level Converter.

- The gds and lef files of HEADER and SLC cells are pre-created before the start of the Generator flow.
                                                                                                                 - The .gds files exist in ``` /.../openfasoc/openfasoc/generators/temp-sense-gen/blocks/sky130hd/gds ```

- The layout of the HEADER cell is shown below:

<img width="960" alt="HEADER gds klayout" src="https://user-images.githubusercontent.com/99788755/222802737-0f667cea-295d-4d4b-ab77-ddaaf2797c76.png">

- The layout of the SLC cell is shown below:

<img width="960" alt="SLC gds layout" src="https://user-images.githubusercontent.com/99788755/222803075-8a5a7f89-97d0-4763-b31d-ba00858c77ec.png">

              
# 6. OpenFASOC flow for Temperature Sensor Generation       
- The default circuit’s physical design generation can be divided into three parts:

1. Verilog generation

2. RTL-to-GDS flow (OpenROAD)

3. Post-layout verification (DRC and LVS)

## Verilog generation:
                                                                                                                                                 
- By using make sky130hd_temp_verilog in ```/.../openfasoc/openfasoc/generators/temp-sense-gen ``` the verilog code based on <b>.jason file</b> will get generated. In this file temperature is being varied from -20 C to 100 C, and the parameter toward which the circuit must be optimized is selected which is <b>"error"</b> here. 

- Based on the operating temperature range, generator calculates the number of header and inverters to minimize the error. 

- To configure circuit specifications, modify the test.json specfile in the ```openfasoc/generators/temp-sense-gen/``` folder.

- The test.json file shown in the below screenshot corresponds to the temp_sense_gen.

<img width="435" alt="test json file" src="https://user-images.githubusercontent.com/99788755/222806722-8724a09d-e4bf-4c1d-b881-f95d5f6a0ba4.png">

- To run verilog generation
```bash
 make sky130hd_temp_verilog
```      
                                                                                                                                                 
-  By running make sky130hd_temp_verilog, the result on the terminal is:

<img width="960" alt="temp_sensor verilog generated" src="https://user-images.githubusercontent.com/99788755/222808230-435c35ce-ef00-4550-8948-458ca55d8fb4.png">
                           
- - After running the ```make sky130hd_temp_verilog``` command, the verilog files of ```counter.v, TEMP_ANALOG_hv.nl.v, TEMP_ANALOG_lv.nl.v``` are created in the ```/.../openfasoc/openfasoc/generators/temp-sense-gen/src``` folder. 

- To run the default generator:
-  cd into ```~/openfasoc/generators/temp_sense``` and  enter ```make sky130hd_temp``` command.


<img width="960" alt="make sky130hd_temp working" src="https://user-images.githubusercontent.com/99788755/222823989-288b4398-8b67-44af-b27b-3de082bc938d.png">

 
- The generator references the model file in an iterative process until either meeting specifications or failing.

- The optimization is done based on "modelfile.csv" which exists at location ``` /.../openfasoc/openfasoc/generators/temp-sense-gen/models ```
                                                 

<img width="960" alt="model_file" src="https://user-images.githubusercontent.com/99788755/222812679-3331dd2b-845b-4472-8cd9-b99f9f7a47aa.png">
                                                                                                                                             
## Synthesis
                            
- The OpenROAD Flow starts with a flow configuration file config.mk, the chosen platform (sky130hd, for example) and the Verilog files are generated from the previous part.

- To Run the synthesis 
```bash
export PDK_ROOT=/usr/local/share/pdk
make sky130hd_temp
```
- If will get some OpenROAD path error: (Remember follow below commands if OpenROAD is installed in home directory.
                             
```bash
export OPENROAD=~/OpenROAD-flow-scripts/tools/OpenROAD
export PATH=~/home/inderjit/OpenROADflowscripts/tools/install/yosys/bin:~/home/inderjit/OpenROAD-flowscripts/tools/install/LSOracle/bin:$PATH
export PDK_ROOT=/home/inderjit/open_pdks/sky130
```
- This commands are initialised OpenROAD along with open_pdks path.

- The config.mk file is shown below:                            
                     
<img width="960" alt="temp sens config file image" src="https://user-images.githubusercontent.com/99788755/222816821-c7f75414-4805-44cc-86de-d6dc19ea859a.png">

- The systhesis verilog codes are found inside tempsense directory. In the following directory all the files corresponding to different stages of the RTL2GDS flow is saved.
```/openfasoc/openfasoc/generators/temp-sense-gen/flow/results/sky130hd/tempsense```

<img width="960" alt="synthesis verilog code location" src="https://user-images.githubusercontent.com/99788755/222818061-70be9327-e2bd-4f3e-8e11-beb464d47707.png">


## Floorplan

- The floorplan for the physical design is generated with OpenROAD, which requires a description of the power delivery network in pdn.cfg.

- The floorplan final power report is shown below:

<img width="960" alt="floor plan final power report" src="https://user-images.githubusercontent.com/99788755/222820583-a1d3d985-bf4a-48db-be4e-3f245edaa387.png">


- This temperature sensor design implements two voltage domains: one for the VDD that powers most of the circuit, and another for the VIN that powers the ring oscillator and is an output of the HEADER cells. 

- Such voltage domains are created within the floorplan.tcl script, with the following lines of code:
                                                                                                       
<img width="960" alt="floor plan final script" src="https://user-images.githubusercontent.com/99788755/222819876-28ad55e2-d0cc-4ba6-a6f6-81b4854383d8.png">


## Placement
Placement takes place after the floorplan is ready and has two phases: global placement and detailed placement. The output of this phase will have all instances placed in their corresponding voltage domain, ready for routing.


##  Routing
Routing is also divided into two phases: global routing and detailed routing. Right before global routing, OpenFASoC calls ```/openfasoc/openfasoc/generators/temp-sense-gen/flow/scripts/openfasoc/pre_global_route.tcl```:

<img width="534" alt="routing working" src="https://user-images.githubusercontent.com/99788755/222821426-5f4618fe-3658-442a-8ea0-97fcfe369000.png">
                                                                                                                                                  
- Power Delivery Network is shown below:

<img width="960" alt="power delivery network" src="https://user-images.githubusercontent.com/99788755/222822498-589c2638-ad91-4c87-9c2f-efd2bb062eeb.png">

## Final Layout after Routing
- Viewing the GDS view of the temperature generator using klayout in result folder.```klayout 6_final.gds```  

<img width="960" alt="final gds" src="https://user-images.githubusercontent.com/99788755/222823025-fe80540a-d150-4919-8cd2-8b81702d0f2f.png">
                                                                                                                                            
                                                                                                        
# Week 3 AIs

This section discusses Week 3 work (25.2.23 to 5.3.23) as part of VSD Mixed-signal PD Research Program                                                                                                           # 1. Background on Ring oscillator 
- Ring Oscillator is very desirable in the VLSI environment because of its integration ability. It is easy to design and easily integrated. Without the need for inductors, the ring oscillator occupies far less die area than a harmonic LC oscillator. It is simple and can be operated at Low-DC level. Unfortunately, the jitter performance of the ring oscillator falls short of the jitter performance of an LC oscillator. CMOS oscillators in today’s technology are typically implemented as ring oscillators or LCOscillators. It is a self-toggling circuit that generates clock-like pulses without any external input, other than the power that it needs. This is created by cascading inverters back to back in odd numbers (so that the next output is different than the previous).                                                                                                                                        
# 2. Prelayout simulation of Three-stage ring oscillator in Xschem
                     
- First, we build the schematic of ring oscillator in xschem
                                                                                                         <img width="960" alt="ring_osc_sys" src="https://user-images.githubusercontent.com/99788755/222826910-8cd65833-ca26-4fc0-aed6-467148c98952.png">
                                                                                                         
- Create symbol by going to the symbol menu and click on "Make symbol from schematic"
                                                                                                         
<img width="960" alt="ring_osc_sym" src="https://user-images.githubusercontent.com/99788755/222827406-1c7a248f-13a2-4e23-9490-aecd5b04143a.png">
                                                                                                         - Next, we create testbench by bringing the symbol of ring oscillator into the new schematic and add   voltage sources, gnd terminal and ipins/opins.                                   
                                                                                                          <img width="960" alt="ring_osc_tb" src="https://user-images.githubusercontent.com/99788755/222827771-38d18776-9bda-4442-a8fd-df6c402f3131.png">
                                                                                                         
- Then, we simulate the ring oscillator testbench in ngspice anf obtain the following results: 
                                                                    
<img width="960" alt="ring_osc_xschem_output" src="https://user-images.githubusercontent.com/99788755/222828074-49ba3837-b4e8-498f-afa4-1fe57e310346.png">

- This completes the prelayout simulation of Ring oscillator. 

- The prelayout netlist generated from xschem is shown for reference. 

```bash
** sch_path: /home/inderjit/lab_inverter/xschem/ring_osc_tb.sch
.subckt ring_osc_tb gnd vdd out
*.PININFO gnd:B vdd:B out:O
x1 vdd out gnd ring_osc
V1 vdd gnd 1.8
.save i(v1)
**** begin user architecture code

** opencircuitdesign pdks install
.lib /home/inderjit/open_pdks/sky130/sky130A/libs.tech/ngspice/sky130.lib.spice tt

.tran 20ps 4n
.save all

**** end user architecture code
.ends

* expanding   symbol:  ring_osc.sym # of pins=3
** sym_path: /home/inderjit/lab_inverter/xschem/ring_osc.sym
** sch_path: /home/inderjit/lab_inverter/xschem/ring_osc.sch
.subckt ring_osc vdd out gnd
*.PININFO vdd:B gnd:B out:O
XM1 net1 out gnd gnd sky130_fd_pr__nfet_01v8 L=0.15 W=1 nf=1 m=1
XM2 net2 net1 gnd gnd sky130_fd_pr__nfet_01v8 L=0.15 W=1 nf=1 m=1
XM3 out net2 gnd gnd sky130_fd_pr__nfet_01v8 L=0.15 W=1 nf=1 m=1
XM4 net1 out vdd vdd sky130_fd_pr__pfet_01v8 L=0.15 W=1 nf=1 m=1
XM5 net2 net1 vdd vdd sky130_fd_pr__pfet_01v8 L=0.15 W=1 nf=1 m=1
XM6 out net2 vdd vdd sky130_fd_pr__pfet_01v8 L=0.15 W=1 nf=1 m=1
.ends

.GLOBAL gnd
.GLOBAL vdd
.end
```

# 2. Post-layout simulation of Three-stage ring oscillator in Magic

- From the testbench for ring oscilator, from the files menu and go to suimulation menu and select "LVS netlist: top lvl is a subsckt" and then tap on the netlist and close xschem.
- Next import the netlist to magic to create the layout. 
- Open magic by moving to the mag directory and using ```magic -T sky130A.tech```
- Go to file --> Import SPICE and select our netlist from the .xschem simulation folder.

<img width="960" alt="ring_osc_layout" src="https://user-images.githubusercontent.com/99788755/222829731-7ec3e7a1-bebc-446a-849a-a308ec77a86a.png">
        
- go to File --> save and select autowrite
- Go to the command window and type the following:
```bash
extract do local
extract all
ext2spice cthresh 0 rthresh 0
ext2spice
```                                                                                                     - Extracted Netlist generated from magic is shown below: 
```bash 
.subckt ring_osc vdd out gnd
X0 m1_1658_712# out gnd VSUBS sky130_fd_pr__nfet_01v8 ad=0.29 pd=2.58 as=0.29 ps=2.58 w=1 l=0.15
X1 m1_2418_712# m1_1658_712# gnd VSUBS sky130_fd_pr__nfet_01v8 ad=0.29 pd=2.58 as=0.87 ps=7.74 w=1 l=0.15
X2 out m1_2418_712# gnd VSUBS sky130_fd_pr__nfet_01v8 ad=0.29 pd=2.58 as=0 ps=0 w=1 l=0.15
X3 m1_1658_712# out vdd XM4/w_n211_n319# sky130_fd_pr__pfet_01v8 ad=0.29 pd=2.58 as=0.29 ps=2.58 w=1 l=0.15
X4 m1_2418_712# m1_1658_712# vdd XM5/w_n211_n319# sky130_fd_pr__pfet_01v8 ad=0.29 pd=2.58 as=0.87 ps=7.74 w=1 l=0.15
X5 out m1_2418_712# vdd XM6/w_n211_n319# sky130_fd_pr__pfet_01v8 ad=0.29 pd=2.58 as=0 ps=0 w=1 l=0.15
C0 gnd m1_1658_712# 0.29fF
C1 out XM6/w_n211_n319# 0.18fF
C2 out m1_2418_712# 0.62fF
C3 vdd gnd 0.01fF
C4 XM4/w_n211_n319# m1_2418_712# 0.00fF
C5 m1_1658_712# XM6/w_n211_n319# 0.00fF
C6 m1_1658_712# m1_2418_712# 0.25fF
C7 vdd XM6/w_n211_n319# 0.16fF
C8 vdd m1_2418_712# 0.29fF
C9 out XM5/w_n211_n319# 0.04fF
C10 XM5/w_n211_n319# XM4/w_n211_n319# 0.04fF
C11 m1_1658_712# XM5/w_n211_n319# 0.34fF
C12 gnd m1_2418_712# 0.27fF
C13 vdd XM5/w_n211_n319# 0.24fF
C14 out XM4/w_n211_n319# 0.33fF
C15 out m1_1658_712# 0.65fF
C16 m1_2418_712# XM6/w_n211_n319# 0.36fF
C17 vdd out 0.24fF
C18 m1_1658_712# XM4/w_n211_n319# 0.20fF
C19 vdd XM4/w_n211_n319# 0.26fF
C20 vdd m1_1658_712# 0.30fF
C21 out gnd 0.22fF
C22 XM5/w_n211_n319# XM6/w_n211_n319# 0.04fF
C23 XM5/w_n211_n319# m1_2418_712# 0.17fF
C24 gnd XM4/w_n211_n319# 0.00fF
C25 m1_2418_712# VSUBS 0.62fF 
**FLOATING
C26 m1_1658_712# VSUBS 0.59fF 
**FLOATING
C27 out VSUBS 1.83fF
C28 vdd VSUBS 1.13fF
C29 XM6/w_n211_n319# VSUBS 1.09fF 
**FLOATING
C30 XM5/w_n211_n319# VSUBS 1.08fF 
**FLOATING
C31 XM4/w_n211_n319# VSUBS 1.09fF 
**FLOATING
C32 gnd VSUBS 1.70fF
.ends
```                                                                                                                                            
<img width="960" alt="ring_osc_layout_extracted_parasitics" src="https://user-images.githubusercontent.com/99788755/222830590-a2ee6fff-5c83-4856-b796-b10136d473a6.png">

- Postlayout netlist with extracted parasitics is shown below:

```bash
* SPICE3 file created from ring_osc.ext - technology: sky130A
** sch_path: /home/inderjit/lab_inverter/xschem/ring_osc_tb.sch
*.PININFO gnd:B vdd:B out:O
x1 vdd out gnd ring_osc
V1 vdd gnd 1.8
.save i(v1)
**** begin user architecture code

** opencircuitdesign pdks install
.lib /home/inderjit/open_pdks/sky130/sky130A/libs.tech/ngspice/sky130.lib.spice tt

.tran 20ps 4n
.save all

**** end user architecture code

.subckt ring_osc vdd out gnd
X0 m1_1658_712# out gnd VSUBS sky130_fd_pr__nfet_01v8 ad=0.29 pd=2.58 as=0.29 ps=2.58 w=1 l=0.15
X1 m1_2418_712# m1_1658_712# gnd VSUBS sky130_fd_pr__nfet_01v8 ad=0.29 pd=2.58 as=0.87 ps=7.74 w=1 l=0.15
X2 out m1_2418_712# gnd VSUBS sky130_fd_pr__nfet_01v8 ad=0.29 pd=2.58 as=0 ps=0 w=1 l=0.15
X3 m1_1658_712# out vdd XM4/w_n211_n319# sky130_fd_pr__pfet_01v8 ad=0.29 pd=2.58 as=0.29 ps=2.58 w=1 l=0.15
X4 m1_2418_712# m1_1658_712# vdd XM5/w_n211_n319# sky130_fd_pr__pfet_01v8 ad=0.29 pd=2.58 as=0.87 ps=7.74 w=1 l=0.15
X5 out m1_2418_712# vdd XM6/w_n211_n319# sky130_fd_pr__pfet_01v8 ad=0.29 pd=2.58 as=0 ps=0 w=1 l=0.15
C0 gnd m1_1658_712# 0.29fF
C1 out XM6/w_n211_n319# 0.18fF
C2 out m1_2418_712# 0.62fF
C3 vdd gnd 0.01fF
C4 XM4/w_n211_n319# m1_2418_712# 0.00fF
C5 m1_1658_712# XM6/w_n211_n319# 0.00fF
C6 m1_1658_712# m1_2418_712# 0.25fF
C7 vdd XM6/w_n211_n319# 0.16fF
C8 vdd m1_2418_712# 0.29fF
C9 out XM5/w_n211_n319# 0.04fF
C10 XM5/w_n211_n319# XM4/w_n211_n319# 0.04fF
C11 m1_1658_712# XM5/w_n211_n319# 0.34fF
C12 gnd m1_2418_712# 0.27fF
C13 vdd XM5/w_n211_n319# 0.24fF
C14 out XM4/w_n211_n319# 0.33fF
C15 out m1_1658_712# 0.65fF
C16 m1_2418_712# XM6/w_n211_n319# 0.36fF
C17 vdd out 0.24fF
C18 m1_1658_712# XM4/w_n211_n319# 0.20fF
C19 vdd XM4/w_n211_n319# 0.26fF
C20 vdd m1_1658_712# 0.30fF
C21 out gnd 0.22fF
C22 XM5/w_n211_n319# XM6/w_n211_n319# 0.04fF
C23 XM5/w_n211_n319# m1_2418_712# 0.17fF
C24 gnd XM4/w_n211_n319# 0.00fF
C25 m1_2418_712# VSUBS 0.62fF 
**FLOATING
C26 m1_1658_712# VSUBS 0.59fF 
**FLOATING
C27 out VSUBS 1.83fF
C28 vdd VSUBS 1.13fF
C29 XM6/w_n211_n319# VSUBS 1.09fF 
**FLOATING
C30 XM5/w_n211_n319# VSUBS 1.08fF 
**FLOATING
C31 XM4/w_n211_n319# VSUBS 1.09fF 
**FLOATING
C32 gnd VSUBS 1.70fF
.ends
```

- Simulate the spice file extracted from magic after modifications.

<img width="960" alt="ring_osc_layout_output" src="https://user-images.githubusercontent.com/99788755/222831314-7294f8c4-b0d5-49e2-817a-000cb6595428.png">

- Quite evident from above output, prelayout and postlayout outputs of Ring oscillator are very closely matching and are genrating oscillation, hene proving its functionality. 

# 3. Post-layout simulation of Ring oscillator using ALIGN

- Go to ALIGN-publicdolder and Create a python virtualenv by typing the following commands in the terminal

```bash
python -m venv general
source general/bin/activate
```

- To make the layout using align tools, first create a work directory in ALIGN-public folder.
- Make sure you have the ring_osc_tb.spice file (created from lvs netlist in xschem) in that folder by copying that file and rename it to .sp as ALIGN only reads .sp files
- Contents of inv.sp is Shown below

<img width="960" alt="ring_osc_sp file" src="https://user-images.githubusercontent.com/99788755/222833706-988326b0-7973-4f95-a254-39fd1f343d14.png">

```bash
.subckt ring_osc vdd out gnd
XM1 net1 out gnd gnd sky130_fd_pr__nfet_01v8 L=150e-09 W=420n nf=10 m=1
XM2 net2 net1 gnd gnd sky130_fd_pr__nfet_01v8 L=150e-09 W=420n nf=10 m=1
XM3 out net2 gnd gnd sky130_fd_pr__nfet_01v8 L=150e-09 W=420n nf=10 m=1
XM4 net1 out vdd vdd sky130_fd_pr__pfet_01v8 L=150e-09 W=840n nf=10 m=1
XM5 net2 net1 vdd vdd sky130_fd_pr__pfet_01v8 L=150e-09 W=840n nf=10 m=1
XM6 out net2 vdd vdd sky130_fd_pr__pfet_01v8 L=150e-09 W=840n nf=10 m=1
.ends
```

- Next, use the following command to make it work

``` python3 ../bin/schematic2layout.py (your .spice file name here) -p ../pdks/SKY130_PDK/ ```

- After running the command successfully you will see that a GDS file is created your terminal window would look as shown in Fig 9.3
                                                                                                                                                   
<img width="960" alt="ring_osc_align_gds_created" src="https://user-images.githubusercontent.com/99788755/222833935-b50c3727-6446-468a-a655-0d15b0b19207.png">

 
- We next can view ALIGN Generated .gds and .lef using ``klayout`` of Ring oscillator

<img width="960" alt="ring_osc_klayout_gds 2" src="https://user-images.githubusercontent.com/99788755/222834084-02da10c7-5142-49a3-b2bc-5dcdd676b534.png">

<img width="960" alt="ring_osc_klayout_lef 2" src="https://user-images.githubusercontent.com/99788755/222834100-a342905e-3959-414d-b143-6577c8ce1a2e.png">


- Next, we open GDS file. To open this .gds file you need to run magic first using the magic commands as 

``` magic -T sky130A.tech ```

- Next go to file menu in Magic-> Click on read gds -> Select your .gds file

- You will get box with black boundaries, do not panic just press s and then x your layout will be displayed like shown below

<img width="960" alt="ring_osc_align_layout_tkcon 2" src="https://user-images.githubusercontent.com/99788755/222834189-c819063f-938d-4a18-916c-caaa9ab3aa6f.png">


- Next we need to run post layout spice simulation, so go to tkcon window and type the following command as shown below

```bash
extract do local
extract all
ext2spice cthresh 0 rthresh 0
ext2spice
```
## Post-layout simulation of Ring oscillator using ALIGN

1. Take the .spice file generated from ALIGN layout and paste it in our testbench spice file.

2. PostLayout extracted netlist is shown below: 

```bash
* SPICE3 file created from RING_OSC_0.ext - technology: sky130A

X0 VDD STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# m1_828_1568# VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X1 m1_828_1568# STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# VDD VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X2 m1_828_1568# STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# VDD VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X3 VDD STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# m1_828_1568# VDD sky130_fd_pr__pfet_01v8 ad=0.2226 pd=2.21 as=0.1176 ps=1.12 w=0.84 l=0.15
X4 m1_828_1568# STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# VDD VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.2226 ps=2.21 w=0.84 l=0.15
X5 VDD STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# m1_828_1568# VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X6 VDD STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# m1_828_1568# VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X7 m1_828_1568# STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# VDD VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X8 m1_828_1568# STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# VDD VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X9 VDD STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# m1_828_1568# VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X10 VDD OUT STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# VDD sky130_fd_pr__pfet_01v8 ad=4.158 pd=40.14 as=1.176 ps=11.2 w=0.84 l=0.15
X11 STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# OUT VDD VDD sky130_fd_pr__pfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.84 l=0.15
X12 STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# OUT VDD VDD sky130_fd_pr__pfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.84 l=0.15
X13 VDD OUT STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# VDD sky130_fd_pr__pfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.84 l=0.15
X14 STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# OUT VDD VDD sky130_fd_pr__pfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.84 l=0.15
X15 VDD OUT STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# VDD sky130_fd_pr__pfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.84 l=0.15
X16 VDD OUT STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# VDD sky130_fd_pr__pfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.84 l=0.15
X17 STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# OUT VDD VDD sky130_fd_pr__pfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.84 l=0.15
X18 STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# OUT VDD VDD sky130_fd_pr__pfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.84 l=0.15
X19 VDD OUT STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# VDD sky130_fd_pr__pfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.84 l=0.15
X20 m1_828_1568# STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# GND GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X21 m1_828_1568# STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# GND GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X22 GND STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# m1_828_1568# GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X23 GND STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# m1_828_1568# GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X24 m1_828_1568# STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# GND GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X25 m1_828_1568# STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# GND GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X26 GND STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# m1_828_1568# GND sky130_fd_pr__nfet_01v8 ad=0.1113 pd=1.37 as=0.0588 ps=0.7 w=0.42 l=0.15
X27 m1_828_1568# STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# GND GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.1113 ps=1.37 w=0.42 l=0.15
X28 GND STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# m1_828_1568# GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X29 GND STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# m1_828_1568# GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X30 STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# OUT GND GND sky130_fd_pr__nfet_01v8 ad=0.588 pd=7 as=2.079 ps=25.02 w=0.42 l=0.15
X31 STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# OUT GND GND sky130_fd_pr__nfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.42 l=0.15
X32 GND OUT STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# GND sky130_fd_pr__nfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.42 l=0.15
X33 GND OUT STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# GND sky130_fd_pr__nfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.42 l=0.15
X34 STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# OUT GND GND sky130_fd_pr__nfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.42 l=0.15
X35 STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# OUT GND GND sky130_fd_pr__nfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.42 l=0.15
X36 GND OUT STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# GND sky130_fd_pr__nfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.42 l=0.15
X37 STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# OUT GND GND sky130_fd_pr__nfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.42 l=0.15
X38 GND OUT STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# GND sky130_fd_pr__nfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.42 l=0.15
X39 GND OUT STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# GND sky130_fd_pr__nfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.42 l=0.15
X40 VDD m1_828_1568# OUT VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X41 OUT m1_828_1568# VDD VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X42 OUT m1_828_1568# VDD VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X43 VDD m1_828_1568# OUT VDD sky130_fd_pr__pfet_01v8 ad=0.2226 pd=2.21 as=0.1176 ps=1.12 w=0.84 l=0.15
X44 OUT m1_828_1568# VDD VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.2226 ps=2.21 w=0.84 l=0.15
X45 VDD m1_828_1568# OUT VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X46 VDD m1_828_1568# OUT VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X47 OUT m1_828_1568# VDD VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X48 OUT m1_828_1568# VDD VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X49 VDD m1_828_1568# OUT VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X50 OUT m1_828_1568# GND GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X51 OUT m1_828_1568# GND GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X52 GND m1_828_1568# OUT GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X53 GND m1_828_1568# OUT GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X54 OUT m1_828_1568# GND GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X55 OUT m1_828_1568# GND GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X56 GND m1_828_1568# OUT GND sky130_fd_pr__nfet_01v8 ad=0.1113 pd=1.37 as=0.0588 ps=0.7 w=0.42 l=0.15
X57 OUT m1_828_1568# GND GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.1113 ps=1.37 w=0.42 l=0.15
X58 GND m1_828_1568# OUT GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X59 GND m1_828_1568# OUT GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
C0 OUT VDD 8.69fF
C1 OUT STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# 1.59fF
C2 VDD STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# 8.65fF
C3 OUT m1_828_1568# 1.93fF
C4 VDD m1_828_1568# 8.01fF
C5 m1_828_1568# STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# 1.92fF
C6 OUT GND 6.76fF **FLOATING
C7 m1_828_1568# GND 6.89fF **FLOATING
C8 STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# GND 5.69fF **FLOATING
C9 VDD GND 17.11fF **FLOATING
```

- Postlayout netlist with control statements and sources is shown below:
```bash
* SPICE3 file created from ring_osc.ext - technology: sky130A
** sch_path: /home/inderjit/lab_inverter/xschem/ring_osc_tb.sch
*.PININFO gnd:B vdd:B out:O
x1 vdd out gnd ring_osc
V1 vdd gnd 1.8
.save i(v1)
**** begin user architecture code

** opencircuitdesign pdks install
.lib /home/inderjit/open_pdks/sky130/sky130A/libs.tech/ngspice/sky130.lib.spice tt

.tran 20ps 4n
.save all

**** end user architecture code

.subckt ring_osc vdd out gnd
X0 VDD STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# m1_828_1568# VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X1 m1_828_1568# STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# VDD VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X2 m1_828_1568# STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# VDD VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X3 VDD STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# m1_828_1568# VDD sky130_fd_pr__pfet_01v8 ad=0.2226 pd=2.21 as=0.1176 ps=1.12 w=0.84 l=0.15
X4 m1_828_1568# STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# VDD VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.2226 ps=2.21 w=0.84 l=0.15
X5 VDD STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# m1_828_1568# VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X6 VDD STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# m1_828_1568# VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X7 m1_828_1568# STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# VDD VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X8 m1_828_1568# STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# VDD VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X9 VDD STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# m1_828_1568# VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X10 VDD OUT STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# VDD sky130_fd_pr__pfet_01v8 ad=4.158 pd=40.14 as=1.176 ps=11.2 w=0.84 l=0.15
X11 STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# OUT VDD VDD sky130_fd_pr__pfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.84 l=0.15
X12 STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# OUT VDD VDD sky130_fd_pr__pfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.84 l=0.15
X13 VDD OUT STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# VDD sky130_fd_pr__pfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.84 l=0.15
X14 STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# OUT VDD VDD sky130_fd_pr__pfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.84 l=0.15
X15 VDD OUT STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# VDD sky130_fd_pr__pfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.84 l=0.15
X16 VDD OUT STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# VDD sky130_fd_pr__pfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.84 l=0.15
X17 STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# OUT VDD VDD sky130_fd_pr__pfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.84 l=0.15
X18 STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# OUT VDD VDD sky130_fd_pr__pfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.84 l=0.15
X19 VDD OUT STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# VDD sky130_fd_pr__pfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.84 l=0.15
X20 m1_828_1568# STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# GND GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X21 m1_828_1568# STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# GND GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X22 GND STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# m1_828_1568# GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X23 GND STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# m1_828_1568# GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X24 m1_828_1568# STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# GND GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X25 m1_828_1568# STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# GND GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X26 GND STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# m1_828_1568# GND sky130_fd_pr__nfet_01v8 ad=0.1113 pd=1.37 as=0.0588 ps=0.7 w=0.42 l=0.15
X27 m1_828_1568# STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# GND GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.1113 ps=1.37 w=0.42 l=0.15
X28 GND STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# m1_828_1568# GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X29 GND STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# m1_828_1568# GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X30 STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# OUT GND GND sky130_fd_pr__nfet_01v8 ad=0.588 pd=7 as=2.079 ps=25.02 w=0.42 l=0.15
X31 STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# OUT GND GND sky130_fd_pr__nfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.42 l=0.15
X32 GND OUT STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# GND sky130_fd_pr__nfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.42 l=0.15
X33 GND OUT STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# GND sky130_fd_pr__nfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.42 l=0.15
X34 STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# OUT GND GND sky130_fd_pr__nfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.42 l=0.15
X35 STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# OUT GND GND sky130_fd_pr__nfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.42 l=0.15
X36 GND OUT STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# GND sky130_fd_pr__nfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.42 l=0.15
X37 STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# OUT GND GND sky130_fd_pr__nfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.42 l=0.15
X38 GND OUT STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# GND sky130_fd_pr__nfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.42 l=0.15
X39 GND OUT STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# GND sky130_fd_pr__nfet_01v8 ad=0 pd=0 as=0 ps=0 w=0.42 l=0.15
X40 VDD m1_828_1568# OUT VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X41 OUT m1_828_1568# VDD VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X42 OUT m1_828_1568# VDD VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X43 VDD m1_828_1568# OUT VDD sky130_fd_pr__pfet_01v8 ad=0.2226 pd=2.21 as=0.1176 ps=1.12 w=0.84 l=0.15
X44 OUT m1_828_1568# VDD VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.2226 ps=2.21 w=0.84 l=0.15
X45 VDD m1_828_1568# OUT VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X46 VDD m1_828_1568# OUT VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X47 OUT m1_828_1568# VDD VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X48 OUT m1_828_1568# VDD VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X49 VDD m1_828_1568# OUT VDD sky130_fd_pr__pfet_01v8 ad=0.1176 pd=1.12 as=0.1176 ps=1.12 w=0.84 l=0.15
X50 OUT m1_828_1568# GND GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X51 OUT m1_828_1568# GND GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X52 GND m1_828_1568# OUT GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X53 GND m1_828_1568# OUT GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X54 OUT m1_828_1568# GND GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X55 OUT m1_828_1568# GND GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X56 GND m1_828_1568# OUT GND sky130_fd_pr__nfet_01v8 ad=0.1113 pd=1.37 as=0.0588 ps=0.7 w=0.42 l=0.15
X57 OUT m1_828_1568# GND GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.1113 ps=1.37 w=0.42 l=0.15
X58 GND m1_828_1568# OUT GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
X59 GND m1_828_1568# OUT GND sky130_fd_pr__nfet_01v8 ad=0.0588 pd=0.7 as=0.0588 ps=0.7 w=0.42 l=0.15
C0 OUT VDD 8.69fF
C1 OUT STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# 1.59fF
C2 VDD STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# 8.65fF
C3 OUT m1_828_1568# 1.93fF
C4 VDD m1_828_1568# 8.01fF
C5 m1_828_1568# STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# 1.92fF
C6 OUT GND 6.76fF 
**FLOATING
C7 m1_828_1568# GND 6.89fF 
**FLOATING
C8 STAGE2_INV_56461923_0_0_1677862843_0/li_1179_1495# GND 5.69fF 
**FLOATING
C9 VDD GND 17.11fF 
**FLOATING
.ends
```


3. Next we, simulate it by invoking ngspice with command ```ngspice filename.spice``` . The following waveform are obtained as shown

<img width="960" alt="ring_osc_align_layout_output" src="https://user-images.githubusercontent.com/99788755/222834743-f82c346b-9e9a-4312-a455-17f95cd12548.png">


