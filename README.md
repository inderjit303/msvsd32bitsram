# VSD Mixed-signal PD Research Program

## Week 0 AIs 

This repository discusses Week 0 work (4.2.23 to 11.2.23) as part of VSD Mixed-signal PD Research Program

- [AI 1 Ubuntu Installation ](#ai-1-ubuntu-installation)
- 
- [Sense amplifier circuit](#Sense-amplifier-circuit)
- [AI 3](#Open-Source-Tools-Used)
  * [eSim](#esim)
  * [NgSpice](#ngspice)
  * [Makerchip](#makerchip)
  * [Verilator](#verilator)


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
a. https://lootr5858.wordpress.com/2020/10/06/magic-vlsi-skywater-pdk-local-installation-guide/
b. http://repo.hu/projects/xschem/xschem_man/install_xschem.html

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

Install steps:

```
git clone https://github.com/StefanSchippers/xschem.git xschem_git
sudo ./configure
sudo make
sudo make install
```
More info can be found at http://repo.hu/projects/xschem/index.html


