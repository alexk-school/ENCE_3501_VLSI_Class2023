# Final Project  Report
By Alex Kondracki
11/13/2023

## Table of Contents
- [Final Project  Report](#final-project--report)
  - [Table of Contents](#table-of-contents)
  - [Intro](#intro)
  - [ELECTRIC VLSI](#electric-vlsi)
    - [Rules](#rules)
    - [MuddLib07](#muddlib07)
    - [Ring Counter](#ring-counter)
    - [Validation](#validation)
  - [Simulation](#simulation)
  - [Conclusion](#conclusion)

## Intro

This lab focuses on using a library called muddLib07 to make a 4 bit ring counter in electric vlsi. A ring counter has only 1 bit high and cycles that position each clock cycle. The ring counter will be made using Inverters, XOR gates, and D flip flops. The ring counter for this lab will feature a falling edge input and an active low clear.

## ELECTRIC VLSI

### Rules

A copy of VLSI settings used can be found in [/electricProject/electricPrefs.xml](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/FinalProject/electricProject/electricPrefs.xml) Keep in mind that this includes simulation settings. This lab was made using [sCMOS sub micron rules](http://bears.ece.ucsb.edu/class/ece224a/sCMOS/sCMOS-main.html) with a λ of 300 nm.

All mosfets will be simulated as long channel.

### MuddLib07

This lab will be done using a library called [muddLib07.jelib](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/FinalProject/electricProject/muddLib07.jelib) Modifications will be shown below.

This lab will use **xor2_1x**, **inv_1x**, and **flopr_c_1x** from muddlib07. **flopr_c_1x** is an active low reset D flip flop. All of these files have been modified to include a text file for compiling into LTSpice, along with assigning each cmos to a model name (See [Simulation](#simulation)). **flopr_c_1x** has been modified to include a **!q** output. This was placed before the inverter that creates **q**.

The flips flops in muddLib07 have two clock inputs **ph1** and **ph2**. When both are high **d** will be connected to **q**. For rising edge behavior the the clock for **ph2** should be the inverse of **ph1**. To achieve falling edge, invert the **ph1** signal and then invert **ph1** for **ph2**.

### Ring Counter

![Ring Counter Overview](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/FinalProject/images/ringcounter4_logi.png)

Figure 1. Overview of ring counter in Logisim Evolution. Has falling edge behavior and active low clear. 

![Ring Counter Schematic](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/FinalProject/images/ringcounter4_sch.png)

Figure 2. Schematic of ring counter. The inverter on **Phase_Count** provides falling edge behavior.

![Ring Counter Layout](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/FinalProject/images/ringcounter4_lay.png)

Figure 3. Layout of ring counter. **Clear**, **ph1**, **ph2**, **!q3** are routed along the bottom. Bottom left gates are inverters.

![Ring Counter Layout Decluttered ](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/FinalProject/images/ringcounter4_lay_alt.png)

Figure 4. Decluttered layout of ring counter. **Clear**, **ph1**, **ph2**, **!q3** are routed along the bottom. Bottom left gates are inverters.

### Validation

![Sidebar](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/FinalProject/images/sidebar.png)

Fig 5. Electric VLSI sidebar.

```
=================================47=================================
Checking schematic cell 'flopr_c_1x{sch}'
   No errors found
Checking schematic cell 'inv_1x{sch}'
   No errors found
Checking schematic cell 'xor2_1x{sch}'
   No errors found
Checking schematic cell 'ringcounter4{sch}'
   No errors found
Checking schematic cell 'ringcounter4_sim{sch}'
   No errors found
0 errors and 0 warnings found (took 0.008 secs)
=================================48=================================
Hierarchical NCC every cell in the design: cell 'ringcounter4_sim{sch}'  cell 'ringcounter4_sim{lay}'
Comparing: ringcounter4:flopr_c_1x{sch} with: ringcounter4:flopr_c_1x{lay}
  exports match, topologies match, sizes not checked in 0.032 seconds.
Comparing: ringcounter4:inv_1x{sch} with: ringcounter4:inv_1x{lay}
  exports match, topologies match, sizes not checked in 0.001 seconds.
Comparing: ringcounter4:xor2_1x{sch} with: ringcounter4:xor2_1x{lay}
  exports match, topologies match, sizes not checked in 0.002 seconds.
Comparing: ringcounter4:ringcounter4{sch} with: ringcounter4:ringcounter4{lay}
  exports match, topologies match, sizes not checked in 0.002 seconds.
Comparing: ringcounter4:ringcounter4_sim{sch} with: ringcounter4:ringcounter4_sim{lay}
  exports match, topologies match, sizes not checked in 0.001 seconds.
Summary for all cells: exports match, topologies match, sizes not checked
NCC command completed in: 0.047 seconds.
```

Text 1. DRC and NCC results. Screenshot can be found in [/images/vlsi_log.png](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/FinalProject/images/vlsi_log.png)

## Simulation

The simulations is using 5V long channel models. This is done using the 1 um CMOS models from the file [/LTSpice/cmosedu_models.txt](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/FinalProject/LTSpice/cmosedu_models.txt)

![D Flip Flop Timing](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/FinalProject/images/flopr_c_1x_sim.png)

Figure 6. D flip flop timing.

![Ring Counter Simulation Schematic](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/FinalProject/images/ringcounter4_sim_sch.png)

Figure 7. Schematic of ring counter. 

![Ring Counter Simulation Phase](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/FinalProject/images/ringcounter4_sim_phase.png)

Figure 8. Schematic of ring counter falling edge phase behavior.

![Ring Counter Simulation Clear](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/FinalProject/images/ringcounter4_sim_clear.png)

Figure 9. Schematic of ring counter active low clear behavior. 

## Conclusion

The 4 bit ring counter was successfully made in Electric VLSI. The simulations confirm that the ring counter has falling edge behavior and and an active low clear. 


