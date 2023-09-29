# Lap 1 Report
By Alex Kondracki
9/29/2023

## Table of Contents
- [Intro](#intro)
- [Design](#design)
   * [Schematic](#schematic)
   * [Rules](#rules)
   * [ELECTRIC VLSI](#electric-vlsi)
   * [Validation](#validation)
- [Hand Calculations](#hand-calculations)
- [Simulations](#simulations)
- [Conclusion](#conclusion)

## Intro
This lab involved calculating, designing, and simulating an 5-bit R-2R Ladder DAC in Electric VLSI. For this lab an R value of 10k ohms was used. A schematic of the DAC can be found below.

## Design

### Schematic
![Schematic](https://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab1/images/schematic_dac.png "Schematic") 

Fig 1. Basic schematic with **B4** as the MSB and **B0** as LSB. It does not use an op-amp. For this, R,RL are 10k ohms and CL is 10pF.

The design used in VLSI will be made by piecing icons (cells) together.

![Cell Schematic ](https://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab1/images/schematic_cell.png "Cell Schematic ") 

Fig 2. Cell to be used in VLSI. For **B0**, **bot** will be put in series with an R resistor.

### Rules

A copy of VLSI setings used can be found in  [/electricProject/electricPrefs.xml](https://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab1/electricProject/electricPrefs.xml) Keep in mind that this includes simulation settings. This lab was made using [scmos sub micron rules](https://bears.ece.ucsb.edu/class/ece224a/scmos/scmos-main.html) with a lambda of 300 nm. .

### ELECTRIC VLSI

The DAC will be made of cells using 10k ohm N-Well Resistors. They have a width of 15 and length of 175.44. Wires and VIAs have a width of 4.

![Cell VLSI](https://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab1/images/cell_sch.png "Cell VLSI")

Fig 3. Cell schematic in VLSI

![Cell Layout](https://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab1/images/cell_lay.png "Cell Layout")

Fig 4. Cell Layout in VLSI.

![DAC VLSI](https://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab1/images/dac_sch.png "DAC VLSI")

Fig 5. DAC schematic in VLSI.

![DAC Layout](https://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab1/images/dac_lay.png "DAC Layout")

Fig 6. DAC Layout in VLSI.

![Sidebar](https://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab1/images/sidebar.png)

Fig 7. Electric VLSI Sidebar.

### Validation

```
=================================8=================================
Running DRC with area bit on, extension bit on, Mosis bit
Checking again hierarchy .... (0.002 secs)
Found 13 networks
0 errors and 0 warnings found (took 0.014 secs)
=================================9=================================
Hierarchical NCC every cell in the design: cell 'dac{sch}'  cell 'dac{lay}'
Comparing: lab1_dac:div{sch} with: lab1_dac:div{lay}
  exports match, topologies match, sizes not checked in 0.023 seconds.
Comparing: lab1_dac:dac{sch} with: lab1_dac:dac{lay}
  exports match, topologies match, sizes not checked in 0.001 seconds.
Summary for all cells: exports match, topologies match, sizes not checked
NCC command completed in: 0.03 seconds.
```

Text 1. DRC and NCC results. Screenshot can be found in [/images/vlsi_log.png](https://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab1/images/vlsi_log.png)


## Hand Calculations

```
Rsquare = 855 ohms, Width = 15 
R = Rsquare * L / W => 10 k = 855 * L / 15 => 15 * 10k / 855 = 175.44

Length = 175.44
```
Text 2. Resistor length calculation

```
R = 20k, C = 10p,
10k * 10p * .7 = 70 ns

TR = 70 ns
```
Text 3. Time Delay Calculation for voltage source at **B4**. Note R is resistance from **B4** to **out**.

```
Vout = x * Vdd / 2^N; B0, B1 are high; Value is 00011 = 3; Vdd = 5V; N = 5 (bits)
Vout = 3 * 5 / 2^5 = 0.4785
```
Text 3. Time Delay Calculation for voltage source at **B4**. Note R is resistance from **B4** to **out**.

```
R@O4 = 20k // (10k + O3) = 10k 
R@O3 = 20k // (10k + O2) = 10.1k
R@O2 = 20k // (10k + O1) = 10.47k
R@O1 = 20k // (10k + O0) = 12k
R@O0 = 20k // (10k + 10k) = 10k

RL = 10k
```
Text 4. 10k ohm load calculation. Done by calculating the resistance from Vout.

## Simulations

![DAC TR Setup](https://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab1/images/lab_setup.png "DAC TR Setup")

Fig 8. Setup for the TR simulation of the DAC.

![DAC TR Simulation](https://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab1/images/lab_sim.png "DAC TR Simulation")

Fig 9. TR simulation of DAC. TR = 69.4 ns

![DAC Voltage Simulation](https://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab1/images/dac_sim.png "DAC Voltage Simulation")

Fig 10. Voltage Simulation of the DAC. Setup can be seen in Fig 5. **B0**,**B1** are high. Vout = 0.46875 V

## Conclusion

A R-2R ladder DAC was designed and simulated in Electric VLSI. The simulations, and hand calculations match. The output resistance of the DAC is 10k. The delay was 69.4 ns which is 0.6 ns off. Turning bits 0,1 to high the DAC corretly outputted 0.46875 V. When the DAC drives a 10k load the output voltage will be halved due to matching the resistance of the DAC. This means a voltage of 0.4685 would be ~ 0.234 V.
