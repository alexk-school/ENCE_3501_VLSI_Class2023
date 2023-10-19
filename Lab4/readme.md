# Lab 4 Report
By Alex Kondracki
10/18/2023

## Table of Contents
- [Lab 4 Report](#lab-4-report)
  - [Table of Contents](#table-of-contents)
  - [Intro](#intro)
  - [Design](#design)
    - [Rules](#rules)
    - [ELECTRIC VLSI](#electric-vlsi)
    - [Validation](#validation)
  - [Simulation](#simulation)
  - [Conclusion](#conclusion)

## Intro

This lab involves creating and simulating two CMOS inverters using Electric VLSI and LTSpice. The first inverter uses a single NMOS and PMOS, and the second use 4 NMOS and PMOS in parallel. After the creation in Electric VLSI the switching point of the inverter will be observed in LTSPice with varying load capacitors.

## Design

### Rules

A copy of VLSI settings used can be found in  [/electricProject/electricPrefs.xml](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab4/electricProject/electricPrefs.xml) Keep in mind that this includes simulation settings. This lab was made using [sCMOS sub micron rules](http://bears.ece.ucsb.edu/class/ece224a/sCMOS/sCMOS-main.html) with a lambda of 300 nm.

### ELECTRIC VLSI

All mosfets have height of 6. PMOS will have a width of 12, and CMOS 6. The source of the PMOS will be connected to VDD, and the drain of the NMOS to GND.

![Inverter 1 Schematic](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab4/images/inverter_1_sch.png)
Fig 1. Schematic of Inverter 1. Uses a single PMOS and NMOS.

![Inverter 1 Layout](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab4/images/inverter_1_sch.png)
Fig 2. Layout of Inverter 1. In is a metal1 to poly connector. P well is tied to GND, N to VDD.

![Inverter 2 Schematic](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab4/images/inverter_2_sch.png)
Fig 3. Schematic of Inverter 2. While it shows a single PMOS and NMOS, there will be 4 in parallel on the layout.

![Inverter 2 Layout](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab4/images/inverter_2_sch.png)
Fig 4. Layout of Inverter 2. Note that some CMOS share sources and drains.

![Simulation 1 Schematic](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab4/images/sim_1_sch.png)
Fig 5. Schematic used for simulation 1. This will confirm the Inverter behavior.

![Simulation 2 Schematic](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab4/images/sim_2_sch.png)
Fig 6. Schematic used for simulation 2. This looks into how the load capacitance affects the switching point.

![Sidebar](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab4/images/sidebar.png)
Fig 7. Electric VLSI Sidebar.

### Validation

```
=================================7=================================
Checking schematic cell 'inverter_1{sch}'
   No errors found
Checking schematic cell 'inverter_2{sch}'
   No errors found
Checking schematic cell 'sim_2{sch}'
   No errors found
0 errors and 0 warnings found (took 0.004 secs)
=================================8=================================
Hierarchical NCC every cell in the design: cell 'inverter_2{sch}'  cell 'inverter_2{lay}'
Comparing: lab4:inverter_2{sch} with: lab4:inverter_2{lay}
  exports match, topologies match, sizes not checked in 0.004 seconds.
Summary for all cells: exports match, topologies match, sizes not checked
NCC command completed in: 0.008 seconds.
=================================9=================================
Hierarchical NCC every cell in the design: cell 'inverter_1{sch}'  cell 'inverter_1{lay}'
Comparing: lab4:inverter_1{sch} with: lab4:inverter_1{lay}
  exports match, topologies match, sizes not checked in 0.004 seconds.
Summary for all cells: exports match, topologies match, sizes not checked
NCC command completed in: 0.004 seconds.
```

Text 1. DRC and NCC results. Screenshot can be found in [/images/vlsi_log.png](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab4/images/vlsi_log.png)

## Simulation

These simulations use the NMOS and PMOS models from the file [/LTSPice/C5_models.txt](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab4/LTSPice/C5_models.txt)

![LTSpice Colors](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab4/images/ltspice_color.png)
Fig 9. Colors used in LTSpice. When there a step parameter is shown it will obey this scheme.

![Simulation 1 Result](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab4/images/sim_1_result.png)
Fig 10. Result of Simulation 1. Inverter 1 had a switching point of 2.42V and Inverter 2 was 2.25V.

Simulation 2 sends a DC Pulse with goes from 0 -> 5V -> 0 over 14 ns. The pulse takes 1 ns to rise and fall, and stays at the peak for 12 ns. This pulse gets sent to each inverter with a load capacitor. The load capacitor will be simulated at 100f, 1p, 10p, and 100p. The next two figures will NOT show Vin as LTSPice doesn't color parameters when multiple traces are loaded. Refer to Fig 9 to match each value to its respective color.

![Simulation 2 Result 1](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab4/images/sim_2_result_1.png)
Fig 11. Result of Inverter 1. From the bottom to top each curve represents a load capacitance of 100f, 1p, 10p, and 100p respectively.

![Simulation 2 Result 2](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab4/images/sim_2_result_2.png)
Fig 12. Result of Inverter 2. From the bottom to top each curve represents a load capacitance of 100f, 1p, 10p, and 100p respectively.

![Simulation 2 Results](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab4/images/sim_2_result.png)
Fig 13. Result of both Inverters and Vin.

## Conclusion
Both inverters where designed and simulated. The single mosfet inverter has a better switching time due to the having a smaller capacitance than inverter 2. In the simulation the higher the capacitance the worse the switching time and behavior. Even at 10p neither behave like a proper inverter. This shows how much unwanted capacitance can affect the behavior of cmos circuits.
