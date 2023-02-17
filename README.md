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

## in progress

# AI 10 Post-layout simulation of CMOS inverter using ALIGN

## in progress

# AI 11 Comparing AI 10 and 4

## 11.1 Pre-schematic simulation of CMOS inverter(hierarchical approach) using xschem/ngspice 

### 3.1 Transient analysis of CMOS Inverter(hierarchical approach) using xschem and ngspice

1. Create the schematic for CMOS inverter schematic in Xschem as shown in fig 1

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/219781370-4b6b2825-d7a5-4c93-a718-ac4070216530.png">
</p> 
<p align="center">
Fig 1. CMOS inverter schematic inner
</p>








# AI 12 Enroll in FREE VSD-custom layout course

## Enrolled and completed



# AI 13 Pre-layout of function using xschem and ngspice using SKY130 PDKS

## Section 1

# AI 14 Post-layout of function using magic and ngspice using SKY130 PDKS

## Section 1 

# AI 15 Post-layout simulation of function using ALIGN

## in progress

# AI 16 Compare AI 14 and 15 

## in progress 

# AI 17 Update Week 1 findings

## in progress 


