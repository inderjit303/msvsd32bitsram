# VSD Mixed-signal PD Research Program

## Week 0 AIs 

This repository discusses Week 0 work (4.2.23 to 11.2.23) as part of VSD Mixed-signal PD Research Program

- [AI 1 Ubuntu Installation ](#ai-1-ubuntu-installation)
- 
- [AI 2 Magic and SKY130 PDKs installation ](#ai-2-magic-and-sky130-pdks-installation )
- [AI 3](#Open-Source-Tools-Used)
 


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

# AI 3 ALIGN tool installation 

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

# AI 4 Pre-layout simulation of CMOS inverter using xschem and ngspice

## 4.1 DC Analysis of CMOS Inverter using xschem and ngspice

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
Fig 6. CMOS Inverter schematic in xschem 
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





 

