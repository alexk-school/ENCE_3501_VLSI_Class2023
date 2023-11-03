# Lab 5 Report
By Alex Kondracki
11/2/2023

## Table of Contents
- [Lab 5 Report](#lab-5-report)
  - [Table of Contents](#table-of-contents)
  - [Intro](#intro)
  - [ELECTRIC VLSI](#electric-vlsi)
    - [Rules](#rules)
    - [NAND2](#nand2)
    - [XOR2](#xor2)
    - [Full Adder](#full-adder)
    - [Validation](#validation)
  - [Simulation](#simulation)
    - [NAND2 Simulation](#nand2-simulation)
    - [XOR2 Simulation](#xor2-simulation)
    - [Full Adder Simulation](#full-adder-simulation)
  - [Conclusion](#conclusion)

## Intro

This lab involved making a CMOS full adder using Electric VLSI and confirming the logical behavior using LTSpice. The full adder is composed of 2 XOR gates and 3 NAND gates. The XOR gates will contain an INV gate for each respective input.

## ELECTRIC VLSI

### Rules

A copy of VLSI settings used can be found in  [/electricProject/electricPrefs.xml](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab5/electricProject/electricPrefs.xml) Keep in mind that this includes simulation settings. This lab was made using [sCMOS sub micron rules](http://bears.ece.ucsb.edu/class/ece224a/sCMOS/sCMOS-main.html) with a lambda of 300 nm.

All mosfets have height of 2 and width of 6. PMOS will be named P_1u, and NMOS will be named N_1u, this is done for LTSpice. LTSpice will view them as having a 1 micron channel.

### NAND2

![NAND2 Schematic](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab5/images/nand2_sch.png)

Fig 1. Schematic of the NAND2 gate.

![NAND2 Stick](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab5/images/nand2_stick.png)

Fig 2. Stick Diagram of the NAND2 gate.

![NAND2 Layout](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab5/images/nand2_lay.png)

Fig 3. Layout of the NAND2 gate.

### XOR2

![XOR2 Schematic](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab5/images/nand2_sch.png)

Fig 4. Schematic of the XOR2 gate. 2 Inverters will be used to provide **!A** and **!B**.

![INV1 Stick](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab5/images/nand2_stick.png)

Fig 5. Stick Diagram of INV1.

![XOR2 Stick](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab5/images/nand2_stick.png)

Fig 6. Stick Diagram of XOR2 gate without the two inverters.

![XOR2 Layout](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab5/images/nand2_lay.png)

Fig 7. Layout of the 2 input NAND gate. Note the gap between the NMOS and PMOS is wider for routing.

### Full Adder

![Full Adder Schematic](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab5/images/fulladder_sch.png)

Fig 8. Schematic of the Full Adder.

![Full Adder Layout](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab5/images/fulladder_lay.png)

Fig 8. Layout of the Full Adder.

![Full Adder Layout (ALT)](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab5/images/fulladder_lay_alt.png)

Fig 8. Layout of the Full Adder with sub components hidden.

![Sidebar](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab5/images/sidebar.png)

Fig 9. Electric VLSI Sidebar.

### Validation

```
=================================2=================================
Checking schematic cell 'NAND2{sch}'
   No errors found
Checking schematic cell 'XOR2{sch}'
   No errors found
Checking schematic cell 'FULLADDER{sch}'
   No errors found
0 errors and 0 warnings found (took 0.02 secs)
=================================3=================================
Running DRC with area bit on, extension bit on, Mosis bit
=================================4=================================
Checking again hierarchy .... (0.002 secs)
Found 11 networks
0 errors and 0 warnings found (took 0.027 secs)
=================================5=================================
Hierarchical NCC every cell in the design: cell 'FULLADDER{sch}'  cell 'FULLADDER{lay}'
Comparing: lab5:NAND2{sch} with: lab5:NAND2{lay}
  exports match, topologies match, sizes not checked in 0.027 seconds.
Comparing: lab5:XOR2{sch} with: lab5:XOR2{lay}
  exports match, topologies match, sizes not checked in 0.002 seconds.
Comparing: lab5:FULLADDER{sch} with: lab5:FULLADDER{lay}
  exports match, topologies match, sizes not checked in 0.002 seconds.
Summary for all cells: exports match, topologies match, sizes not checked
NCC command completed in: 0.073 seconds.
```

Text 1. DRC and NCC results. Screenshot can be found in [/images/vlsi_log.png](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab5/images/vlsi_log.png)

## Simulation

These simulations confirm the expected behavior for each logic device in the lab by cycling all inputs between ***GND*** and **VDD** with a staggered delay. The goal is to view the outputs of all possible logic inputs. IE **00 01 11 10** for a two input device.

These simulations use the NMOS and PMOS models from the file [/LTSPice/cmosedu_models.txt](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab5/LTSpice/cmosedu_models.txt)

### NAND2 Simulation

![NAND2 Schematic](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab5/images/nand2_sim_sch.png)

Fig 10. NAND2 Simulation Schematic. A and B will be 5ns out of sync.

![NAND2 Result](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab5/images/nand2_sim_result.png)

Fig 11. NAND2 Simulation Results.

### XOR2 Simulation

![XOR2 Schematic](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab5/images/xor2_sim_sch.png)

Fig 12. XOR2 Simulation Schematic. A and B will be 5ns out of sync.

![XOR2 Result](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab5/images/xor2_sim_result.png)

Fig 13. XOR2 Simulation Results.

### Full Adder Simulation

![Full Adder Schematic](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab5/images/fulladder_sim_sch.png)

Fig 14. Full Adder Simulation Schematic. A and be will be 5ns out of sync. Cin will be 2.5ns out of sync with A and B.

![Full Adder Result](http://raw.githubusercontent.com/alexk-school/ENCE_3501_VLSI_Class2023/main/Lab5/images/fulladder_sim_result.png)

Fig 15. Full Adder Simulation Results.

## Conclusion

The NAND2 and XOR2 were bundled together into a Full Adder. The Full Adder behaved as expected. For the timing a signal needs to sequentially activate/deactivate a number of MOSFETS (that are in series) to affect the output of a logic device. 

For the [XOR2](#xor2) if **A** or **B** were flipped, first the inverter MOSFETS would flip followed by the output flipping the MOSFETS in the main part of the Gate before the output is correct. That would be a total delay of 2.

For the [NAND2](#nand2) if **A** or **B** were flipped the only one set of MOSFETS needs to flip before the output is correct. That would be a total delay of 1 .

For the [Full Adder](#full-adder) if **A**, **B** or **Cin** flip there are now two different outputs. **Cin** affects **S** and **Cout** with a delay of 2. **A** needs a delay of 2 for **S** and 4 for **Cout**, however it starts to affect **Cout** at 2. **B** is the same as **A**. This means that flipping anything requires waiting for a delay of 4 before the output is correct.

Note that this assumes the delay of NMOS and PMOS are the same. This also assumes that Low to High and High to Low take the same time which is untrue due to holes moving slower than electrons. One solution would be to take the worst case delay for all possibilities and use it as the "delay per MOSFET".

