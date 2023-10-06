# Lap 2 Report
By Alex Kondracki
10/6/2023

## Table of Contents
- [Lap 2 Report](#lap-2-report)
  - [Table of Contents](#table-of-contents)
  - [Intro](#intro)
  - [Design](#design)
    - [Schematics](#schematics)
    - [Rules](#rules)
    - [ELECTRIC VLSI](#electric-vlsi)
    - [Validation](#validation)
  - [Conclusion](#conclusion)

## Intro
This lab involved creating a 8 pad frame around the 5 bit dac made in ![Lab 1](github.com/alexk-school/ENCE_3501_VLSI_Class2023/tree/main/Lab1)

## Design

### Schematics

![DAC Schematic](raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab2/images/schematic_dac.png) 

Fig 1. Schematic of the 5 bit dac designed in lab 1.

![Pad Schematic](raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab2/images/schematic_pad.png) 

Fig 2. Schematic of the pad layout. Black is occupied space. Purple is a the connecter between metals 2 and 3. Gray is the passivization node

### Rules

A copy of VLSI setings used can be found in  [/electricProject/electricPrefs.xml](raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab2/electricProject/electricPrefs.xml) Keep in mind that this includes simulation settings. This lab was made using [scmos sub micron rules](bears.ece.ucsb.edu/class/ece224a/scmos/scmos-main.html) with a lambda of 300 nm.

### ELECTRIC VLSI

The 5 bit dac was imported from Lab 1. The ground was altered to be a tag in the dac schematic.

![DAC VLSI](raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab2/images/dac_sch.png) 

Fig 3. VLSI Schematic of DAC

A pad was created it will be chained together to make the frame.

![Pad VLSI](raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab2/images/pad_sch.png) 

Fig 4. VLSI Schematic of PAD. 

![Pad Layout](raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab2/images/pad_lay.png) 

Fig 5. VLSI Layout of PAD. Note the outside square is a drawing to provide spacing. Made from Fig 2.

The padframe is made from the pads. In schematics it is represented using a bus in Electric VLSI.

![Padframe VLSI](raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab2/images/padframe_sch.png) 

Fig 6. VLSI Schematic of padframe. Uses a bus.

![Padframe Layout](raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab2/images/padframe_lay.png) 

Fig 7. VLSI Layout of padframe.

The dac and padframe and combined into a single IC. 

![IC VLSI](raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab2/images/ic_sch.png) 

Fig 8. Dac and Padframe linked in Electric VLSI. The pins are set up for the layout.

![IC Layout](raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab2/images/ic_lay.png) 

Fig 9. Dac and Padframe layout. Wires/vias/connectors have a width of 4 lambda. There is a hidden export on pin 3 to prevent Electric VLSI errors.

![Sidebar](raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab2/images/sidebar.png)

Fig 10. Electric VLSI Sidebar.

### Validation

```
=================================2=================================
Checking schematic cell 'div{sch}'
   No errors found
Checking schematic cell 'dac{sch}'
   No errors found
Checking schematic cell 'pad{sch}'
   No errors found
Checking schematic cell 'padframe{sch}'
   No errors found
Checking schematic cell '0_ic{sch}'
   No errors found
0 errors and 0 warnings found (took 0.017 secs)
=================================3=================================
Hierarchical NCC every cell in the design: cell '0_ic{sch}'  cell '0_ic{lay}'
Comparing: lab2_dacframe:div{sch} with: lab2_dacframe:div{lay}
  exports match, topologies match, sizes not checked in 0.021 seconds.
Comparing: lab2_dacframe:dac{sch} with: lab2_dacframe:dac{lay}
  exports match, topologies match, sizes not checked in 0.002 seconds.
Comparing: lab2_dacframe:pad{sch} with: lab2_dacframe:pad{lay}
  exports match, topologies match, sizes not checked in 0.0 seconds.
Comparing: lab2_dacframe:padframe{sch} with: lab2_dacframe:padframe{lay}
  exports match, topologies match, sizes not checked in 0.002 seconds.
Comparing: lab2_dacframe:0_ic{sch} with: lab2_dacframe:0_ic{lay}
  exports match, topologies match, sizes not checked in 0.001 seconds.
Summary for all cells: exports match, topologies match, sizes not checked
NCC command completed in: 0.035 seconds.
```

Text 1. DRC and NCC results. Screenshot can be found in [/images/vlsi_log.png](raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab2/images/vlsi_log.png)

## Conclusion

The pad was created and turned into a padframe. The dac was given a ground flag to interface with the IC. For the IC schematic pins were chosen based on layout location. The dac was placed to the side of the padframe and was wired to metal 3-2 connectors that would be near each pad. The dac setup was then dragged over into the middle of the frame and was connected to each pin on the padframe. After using exports on each connect (including the unused pin 3) there were no errors and the lab was complete.