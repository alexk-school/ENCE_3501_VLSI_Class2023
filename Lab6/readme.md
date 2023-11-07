# Lab 6 Report
By Alex Kondracki
11/7/2023

## Table of Contents
- [Lab 6 Report](#lab-6-report)
  - [Table of Contents](#table-of-contents)
  - [Intro](#intro)
  - [ELECTRIC VLSI](#electric-vlsi)
    - [Rules](#rules)
    - [Gates](#gates)
    - [Charge Pump](#charge-pump)
    - [Ring Oscillator](#ring-oscillator)
    - [Regulator](#regulator)
    - [DC-DC Converter](#dc-dc-converter)
    - [Validation](#validation)
  - [Simulation](#simulation)
    - [Charge Pump](#charge-pump-1)
    - [Ring Oscillator](#ring-oscillator-1)
    - [Regulator](#regulator-1)
    - [DC-DC Converter](#dc-dc-converter-1)
  - [Conclusion](#conclusion)

## Intro

This lab involved making a DC-DC converter that converts 1v to ~1.8v using Electric VLSI. The converter uses a 3 stage charge pump driven by a ring oscillator and a regulator to disable the ring oscillator when the output is above ~1.8 V. The full converter will only be assembled in a schematic.

On top of CMOS, this lab uses diodes, resistors and capacitors. Diodes in this lab will be NMOS with a shorted gate and source, this is done as it is simpler to model. Resistors will not be done to scale in the layout, this is because the labs use MegΩ which would need around 1k if not more squares. Capacitors will be only used symbolically in schematics, this is for two reasons. Electric will bridge both sides in the layout and consider them one network which in turn makes the NCC throw errors. Additionally, capacitors such as poly1-poly2 would require a size almost up to cm^2 assuming a sheet resistance in 10 fF/um^2. 

## ELECTRIC VLSI

### Rules

A copy of VLSI settings used can be found in [/electricProject/electricPrefs.xml](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab6/electricProject/electricPrefs.xml) Keep in mind that this includes simulation settings. This lab was made using [sCMOS sub micron rules](http://bears.ece.ucsb.edu/class/ece224a/sCMOS/sCMOS-main.html) with a λ of 300 nm.

All mosfets have length of 2 and be simulated as short channel. PMOS will be named P_50n, and NMOS will be named N_50n, this is done for LTSpice.

### Gates

NAND and NOT (inverter) gates.

![INV1 Schematic](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab6/images/inv1_sch.png)

Figure 1. INV1 schematic.

![INV1 Layout](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab6/images/inv1_lay.png)

Figure 2. INV1 layout. Middle gap is 13λ to have the same height as the NAND layout.

![NAND Schematic](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab6/images/nand2_sch.png)

Figure 3. NAND2 schematic.

![NAND Layout](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab6/images/nand2_lay.png)

Figure 4. NAND2 layout. Routing of **A** is done to avoid using metal2.

### Charge Pump

3 stage charge pump using 100uF capacitors and a 2MegΩ resistor.

![Charge Pump Schematic](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab6/images/chargepump_sch.png)

Figure 5. Charge pump schematic. NMOS is are as diodes. Capacitors will not be present in the layout.

![Charge Pump Layout](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab6/images/chargepump_lay.png)

Figure 6. Charge pump layout. Capacitor locations shown as drawings. Resistor size not to scale.

### Ring Oscillator

~40 Hz ring oscillator using 1uF capacitors. While number of INV1 gates is even the total number of gates is odd making the circuit astable.

![Ring Osc Schematic](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab6/images/ringosc_sch.png)

Figure 7. Ring oscillator schematic. Capacitors will not be present in the layout.

![Ring Osc Layout](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab6/images/ringosc_lay.png)

Figure 8. Ring oscillator layout. Capacitor locations shown as drawings.

![Ring Osc Decluttered Layout](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab6/images/ringosc_lay_alt.png)

Figure 9. Decluttered ring oscillator layout. Capacitor locations shown as drawings.

### Regulator

Simple voltage regulator using resistors and a diode. When input is below ~1.8V sends an **EN** signal. Resistor values were picked through simulations.

![Regulator Schematic](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab6/images/regulator_sch.png)

Figure 10. Regulator schematic.

![Regulator Osc Layout](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab6/images/regulator_lay.png)

Figure 11. Regulator layout. Resistor size not to scale.

![Regulator Osc Decluttered Layout](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab6/images/regulator_lay_alt.png)

Figure 12. Decluttered regulator layout. Resistor size not to scale.

### DC-DC Converter

DC Converter. Converts 1V to ~1.8V

![DC Converter Schematic](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab6/images/dcconverter_sch.png)

Figure 13. DC converter schematic. **OUT** is the output voltage. **OUT** is fed into the regulator which produces **EN**. **EN** controls the ring oscillator.

### Validation

![Sidebar](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab6/images/sidebar.png)

Fig 14. Electric VLSI sidebar.

```
=================================2=================================
Checking schematic cell 'ChargePump{sch}'
   No errors found
Checking schematic cell 'INV1{sch}'
   No errors found
Checking schematic cell 'Regulator{sch}'
   No errors found
Checking schematic cell 'NAND2{sch}'
   No errors found
Checking schematic cell 'RingOsc{sch}'
   No errors found
Checking schematic cell 'DC_Converter{sch}'
   No errors found
0 errors and 0 warnings found (took 0.033 secs)
=================================3=================================
Hierarchical NCC every cell in the design: cell 'ChargePump{sch}'  cell 'ChargePump{lay}'
Comparing: lab6:ChargePump{sch} with: lab6:ChargePump{lay}
  exports match, topologies match, sizes not checked in 0.111 seconds.
Summary for all cells: exports match, topologies match, sizes not checked
NCC command completed in: 0.118 seconds.
=================================4=================================
Hierarchical NCC every cell in the design: cell 'Regulator{sch}'  cell 'Regulator{lay}'
Comparing: lab6:INV1{sch} with: lab6:INV1{lay}
  exports match, topologies match, sizes not checked in 0.002 seconds.
Comparing: lab6:Regulator{sch} with: lab6:Regulator{lay}
  exports match, topologies match, sizes not checked in 0.002 seconds.
Summary for all cells: exports match, topologies match, sizes not checked
NCC command completed in: 0.004 seconds.
=================================5=================================
Hierarchical NCC every cell in the design: cell 'RingOsc{sch}'  cell 'RingOsc{lay}'
Comparing: lab6:INV1{sch} with: lab6:INV1{lay}
  exports match, topologies match, sizes not checked in 0.001 seconds.
Comparing: lab6:NAND2{sch} with: lab6:NAND2{lay}
  exports match, topologies match, sizes not checked in 0.002 seconds.
Comparing: lab6:RingOsc{sch} with: lab6:RingOsc{lay}
  exports match, topologies match, sizes not checked in 0.003 seconds.
Summary for all cells: exports match, topologies match, sizes not checked
NCC command completed in: 0.009 seconds.
```

Text 1. DRC and NCC results. Screenshot can be found in [/images/vlsi_log.png](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab6/images/vlsi_log.png)

## Simulation

These simulations are using short channel (50nm) models. They use the 50nm CMOS models from the file [/LTSPice/cmosedu_models.txt](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab6/LTSpice/cmosedu_models.txt)

### Charge Pump

![Charge Pump Simulation](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab6/images/chargepump_sim.png)

Figure 15. Simulation of 3 stage charge pump with 40Hz oscillating signals. Voltage stabilizes at ~1.79V after ~90 seconds.

### Ring Oscillator

![Ring Osc Simulation](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab6/images/ringosc_sim.png)

Figure 16. Simulation of ring oscillator.

![Ring Osc Decluttered Simulation](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab6/images/ringosc_sim_alt.png)

Figure 17. Decluttered simulation of ring oscillator. Period is ~25ms which is about ~40Hz.

### Regulator

![Regulator Simulation](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab6/images/regulator_sim.png)

Figure 18. Regulator Simulation. **A** is input. **Y** is the output of INV1.

### DC-DC Converter

![DC Converter Simulation](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab6/images/dcconverter_sim.png)

Figure 19. DC converter simulation. After ~80 seconds, **OUT** stabilizes at ~1.78V and **EN** at ~0.47V

## Conclusion

The DC-DC converter was able to convert a signal of 1V into ~1.8V. The value of 1.8V was picked as the time taken for **OUT** as the change in **OUT** decreases as **OUT** increases. The output voltage could be increased further by adding more stages to the charge pump.

