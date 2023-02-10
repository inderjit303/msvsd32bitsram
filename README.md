# VSD Mixed-signal PD Research Program

## Week 0 AIs 

### 1. AI 1 Ubuntu Installation 

This repository discusses Week 0 work (4.2.23 to 11.2.23) 

- [AI 1](#ai-1)
- 
- [Sense amplifier circuit](#Sense-amplifier-circuit)
- [AI 3](#Open-Source-Tools-Used)
  * [eSim](#esim)
  * [NgSpice](#ngspice)
  * [Makerchip](#makerchip)
  * [Verilator](#verilator)


# AI 1

**Ubuntu Installation **


The components required for building 32 Bit SRAM cell are:
1. 5x32 SRAM Address Decoder and 3x8 SRAM Address Decoder implemented in digital domain using NgVeri feature in eSim. 
2. 1-bit SRAM cell as shown in fig 2 which further consists of
3. Data writer circuit implemented in digital domain using NgVeri
4. 6T SRAM cell and 
5. Sense amplifier circuit implemented in analog domain using eSim. 

The project is about building a 32-bit SRAM memory array, using 130nm CMOS technology and modular design approach. The functional block diagram of 32 bit SRAM is shown in fig 1. 

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/194718005-4117a875-6010-48e6-9486-85eff340662a.png">
</p> 
<p align="center">
Fig 1. Functional block for 32 bit SRAM cell
</p>
