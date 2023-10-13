# Lab 3 Report
By Alex Kondracki
10/13/2023

## Table of Contents
- [Lab 3 Report](#lab-3-report)
  - [Table of Contents](#table-of-contents)
  - [Intro](#intro)
  - [Design](#design)
    - [Rules](#rules)
    - [ELECTRIC VLSI](#electric-vlsi)
    - [Validation](#validation)
  - [Conclusion](#conclusion)

## Intro
This lab involved adding electrostatic discharge (ESD) protection to an 8-pad frame, and placing a NMOS mosefet in the center. This was done with clamping ESD where the pad is clamped by two diodes. The first goes from ground to pad and then from the pad to VDD, which allows spikes to either flow to ground or VDD disapating most of the energy. In this lab only 1 clamp with 2 diodes will be used making the ESD protection minimal. A template for this lab was used, which is provided by [gfm16617](http://github.com/gfm16617) and also found in the [electricProject folder](http://www.github.com/alexk-school/ENCE_3501_VLSI_Class2023/tree/main/Lab3/electricProject)

## Design

### Rules

A copy of VLSI setings used can be found in  [/electricProject/electricPrefs.xml](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab3/electricProject/electricPrefs.xml) Keep in mind that this includes simulation settings. This lab was made using [scmos sub micron rules](http://bears.ece.ucsb.edu/class/ece224a/scmos/scmos-main.html) with a lambda of 300 nm.

### ELECTRIC VLSI

This was started using the template found in the electricProject folder.

![nActive_pWell Schematic](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab3/images/nActive_pWell_sch.png)

Fig 1. nActive diode schematic. This will connect PAD to VDD.

![nActive_pWell Layout](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab3/images/nActive_pWell_lay.png)

Fig 2. nActive diode layout. This will connect PAD to VDD.

![pActive_nWell Schematic](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab3/images/pActive_nWell_sch.png)

Fig 3. pActive diode schematic. This will connect GND to PAD.

![pActive_nWell Layout](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab3/images/pActive_nWell_lay.png)

Fig 4. pActive diode layout. This will connect GND to PAD.

![pad_esd Schematic](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab3/images/pad_esd_sch.png)

Fig 5. Schematic of the pad with ESD protection.

![pad_esd Layout](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab3/images/pad_esd_lay.png)

Fig 6. Layout of the pad with ESD protection. The pad (Smaller Red Square) is hidden to show how the everything connects.

![padframe_esd Schematic](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab3/images/padframe_esd_sch.png)

Fig 7. Schematic of the padframe with ESD protection. 

![padframe_esd Layout](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab3/images/padframe_esd_lay.png)

Fig 8. Layout of the padframe with ESD protection. The inner ring is ground and the outer is VDD.

![final_ic_esd Schematic](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab3/images/fiinal_ic_esd_sch.png)

Fig 9. Schematic of the NMOS mosfet connected to padframe_esd. Note that pin 7 is wired to both the mosfet and frame as Electric VLSI does not support having two exports with the same name. 

![final_ic_esd Layout](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab3/images/fiinal_ic_esd_lay.png)

Fig 10. Layout of the of the NMOS mosfet connected to padframe_esd. Pin 7 is GND and pin 2 is VDD. Metal-1 to metal-2 connectors are used to connect the pads to the mosfet inside the circuit.

![Sidebar](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab3/images/sidebar.png)

Fig 11. Electric VLSI Sidebar.

### Validation

```
=================================2=================================
Running DRC with area bit on, extension bit on, Mosis bit
Checking again hierarchy .... (0.003 secs)
Found 9 networks
0 errors and 0 warnings found (took 0.02 secs)
=================================3=================================
Checking schematic cell 'NMOS_IV{sch}'
   No errors found
Checking schematic cell 'nActive_pWell{sch}'
   No errors found
Checking schematic cell 'pActive_nWell{sch}'
   No errors found
Checking schematic cell 'pad_esd{sch}'
   No errors found
Checking schematic cell 'padframe_esd{sch}'
   No errors found
Checking schematic cell 'final_ic_esd{sch}'
   No errors found
0 errors and 0 warnings found (took 0.012 secs)
=================================4=================================
Hierarchical NCC every cell in the design: cell 'final_ic_esd{sch}'  cell 'final_ic_esd{lay}'
Comparing: lab_3_nmos_esd:NMOS_IV{sch} with: lab_3_nmos_esd:NMOS_IV{lay}
  exports match, topologies match, sizes not checked in 0.022 seconds.
Comparing: lab_3_nmos_esd:nActive_pWell{sch} with: lab_3_nmos_esd:nActive_pWell{lay}
  exports match, topologies match, sizes not checked in 0.001 seconds.
Comparing: lab_3_nmos_esd:pActive_nWell{sch} with: lab_3_nmos_esd:pActive_nWell{lay}
  exports match, topologies match, sizes not checked in 0.0 seconds.
Comparing: lab_3_nmos_esd:pad_esd{sch} with: lab_3_nmos_esd:pad_esd{lay}
  exports match, topologies match, sizes not checked in 0.001 seconds.
Comparing: lab_3_nmos_esd:padframe_esd{sch} with: lab_3_nmos_esd:padframe_esd{lay}
  exports match, topologies match, sizes not checked in 0.003 seconds.
Comparing: lab_3_nmos_esd:final_ic_esd{sch} with: lab_3_nmos_esd:final_ic_esd{lay}
  exports match, topologies match, sizes not checked in 0.001 seconds.
Summary for all cells: exports match, topologies match, sizes not checked
NCC command completed in: 0.037 seconds.
```

Text 1. DRC and NCC results. Screenshot can be found in [/images/vlsi_log.png](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab3/images/vlsi_log.png)

## Conclusion

The pad was created and turned into a padframe. The dac was given a ground flag to interface with the IC. For the IC schematic pins were chosen based on layout location. The dac was placed to the side of the padframe and was wired to metal 3-2 connectors that would be near each pad. The dac setup was then dragged over into the middle of the frame and was connected to each pin on the padframe. After using exports on each connect (including the unused pin 3) there were no errors and the lab was complete.
