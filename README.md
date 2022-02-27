# Table of contents
▫️[Abstract](https://github.com/arpit306/Implementation-of-CMOS-Schmitt-Trigger/blob/main/README.md#abstract)  
▫️[Tools used](https://github.com/arpit306/Implementation-of-CMOS-Schmitt-Trigger/blob/main/README.md#tool-used)  
▫️[Circuit Description](https://github.com/arpit306/Implementation-of-CMOS-Schmitt-Trigger/blob/main/README.md#circuit-description)  
▫️[Circuit Design](https://github.com/arpit306/Implementation-of-CMOS-Schmitt-Trigger/blob/main/README.md#circuit-design)  
▫️[Waveform](https://github.com/arpit306/Implementation-of-CMOS-Schmitt-Trigger/blob/main/README.md#waveform)  
▫️[Spice Netist](https://github.com/arpit306/Implementation-of-CMOS-Schmitt-Trigger/blob/main/README.md#spice-netlist)  
▫️[Acknowledgement](https://github.com/arpit306/Implementation-of-CMOS-Schmitt-Trigger/blob/main/README.md#acknowledgements)  
▫️[References](https://github.com/arpit306/Implementation-of-CMOS-Schmitt-Trigger/blob/main/README.md#references)  
# Abstract
This repository presents the analog IC design and implementation of a CMOS Schmitt Trigger circuit. This implementation is done on Sysnopsys Custom Compiler tool and libraries available on cloud platform using 28nm technology. The Schmitt Trigger is a comparator circuit that incorporates positive feedback, are extensively used in digital as well as analog systems to filter out any noise present in a signal line and produce a clean digital signal. The working of design is verified using Circuit Schematic and Waveforms.
# Tools used
The Synopsys Custom Compiler™ design environment is a modern solution for full-custom analog, custom digital, and mixed-signal IC design. As the heart of the Synopsys Custom Design Platform, Custom Compiler provides design entry, simulation management and analysis, and custom layout editing features. It delivers industry-leading productivity, performance, and ease-of-use while remaining easy to adopt for users of legacy tools. The Custom Compiler design environment includes features for mixed-signal design entry, design debug, simulation management, analysis and reporting.

![155880341-35eceee8-282e-433a-9b72-63bee758ffb1](https://user-images.githubusercontent.com/68592620/155882760-832f2e1b-67cf-4f46-9309-bac0c4960290.png)  
# Circuit Description
Schmitt Trigger is a very important circuit as far as both analog & digital electronics is concerned. It has got a wide range of applications in mixed signal circuits also. Schmitt Trigger is basically a voltage comparator, but with positive feedback employed in the circuit. Schmitt Trigger’s circuit can be made from an Op-Amp, 555 timer IC and at transistor level as well. It is also called as bistable multivibrator because it has two stable states and the transition from one state to another requires an external stimulus. This concept gives rise to flip flops in digital electronics.

![image](https://user-images.githubusercontent.com/68592620/155884086-e95bd774-3d90-4971-b1d4-54729fadf00a.png)

Since the circuit has positive feedback, the output of the circuit can only be upper or lower saturation voltage levels of the circuit. Due to positive feedback, the transfer function of the circuit has different forward and backward paths i.e., Hysteresis curve is obtained. There are upper and lower threshold voltage levels in input, depending on which the output level is determined. So, if an alternating, periodic sinusoidal or triangular input signal is given to the circuit, a square waveform is obtained at the output.
When a transmitted signal is received at a receiver, the signal is generally affected by noise during transmission, so at the end of receiver, a Schmitt trigger is used to remove noise from the received signal and produce a clean digital signal at the output, due to its hysteresis shaped transfer characteristics. So, it takes noisy signals & produces signal with clean and ripple free transitions.

__Reference Waveform:__

![image](https://user-images.githubusercontent.com/68592620/155884536-068faa2c-0081-47d9-a8b9-af3cf728d736.png)

In general, it works as an inverter which consists of two PMOS transistors, two NMOS transistors, one feedback PMOS transistor and one feedback NMOS transistor. The output is high when the input is below the negative threshold voltage, while the output is low if the input exceeds the positive threshold voltage. By calibrating the transistor’s performances and dimensions, the threshold voltages can be adjusted and controlled (PMOS and NMOS).
# Circuit Design
The schematic of the circuit design is shown below.  
![image](https://user-images.githubusercontent.com/68592620/155879444-6a8a5372-9e19-4bef-8dc5-2c24899f2ace.png)  
After creating the symbol of this design, a testbench file was created in which proper sources were added to the design as shown below.
![tb](https://user-images.githubusercontent.com/68592620/155878327-c9ef74f8-5cf5-434e-9c81-d0d568a050ff.png)

# Waveform 
▫️ When Sine Wave is given as input  
![image](https://user-images.githubusercontent.com/68592620/155883745-61456391-c1d3-460f-a317-f925cd4b9fdd.png)  
▫️ When Traingular wave is given as input  
![image](https://user-images.githubusercontent.com/68592620/155883848-f492d37d-7020-46ff-be92-5fa5113b9df7.png)  
# Spice Netlist
```
*  Generated for: PrimeSim
*  Design library name: arpit_lib
*  Design cell name: Schmitt_trigger_tb
*  Design view name: schematic
.lib 'hspice/saed32nm.lib' TT

*Custom Compiler Version S-2021.09
*Sun Feb 27 09:16:53 2022

.global gnd!
********************************************************************************
* Library          : arpit_lib
* Cell             : Schmitt_trigger
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
.subckt schmitt_trigger gnd_1 vdd vin vout
xm15 gnd_1 vout net11 net11 p105 w=0.9u l=2.4u nf=1 m=1
xm1 vout vin net6 net6 p105 w=1.5u l=0.03u nf=1 m=1
xm0 net11 vin vdd vdd p105 w=1.5u l=0.03u nf=1 m=1
xm14 vdd vout net29 net29 n105 w=0.8u l=2.1u nf=1 m=1
xm5 net29 vin gnd_1 gnd_1 n105 w=3.5u l=0.03u nf=1 m=1
xm7 vout vin net29 net29 n105 w=3.5u l=30n nf=1 m=1
.ends schmitt_trigger

********************************************************************************
* Library          : arpit_lib
* Cell             : Schmitt_trigger_tb
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
xi10 gnd! net2 vin vout schmitt_trigger
v3 net2 gnd! dc=1.8
v9 vin gnd! dc=0 sin ( 0 0.15 30 0 0 0 )

.tran '0.001*(20m-0)' '20m' name=tran
.option primesim_remove_probe_prefix = 0
.probe v(*) i(*) level=1
.probe tran v(vin) v(vout)
.temp 25
.option primesim_output=wdf
.option parhier = LOCAL
```
# Acknowledgement
▫️ [Cloud Based Analog IC Design Hackathon](https://hackathoniith.in/')  
▫️ [Kunal Ghosh, Co-founder, VSD Corp. Pvt. Ltd.](https://www.linkedin.com/in/kunal-ghosh-vlsisystemdesign-com-28084836/?originalSubdomain=in/')  
▫️ [Synopsys India](https://www.synopsys.com/')  
▫️ [VLSI System Design (VSD) Corp. Pvt. Ltd India](https://www.vlsisystemdesign.com/')  
▫️ Sumanto Kar, IIT Bombay  
▫️ Chinmay Panda, IIT Hyderabad  
▫️ Shafali Jagga, IPEC Ghaziabad
# References
1. Konjeti V K V L Pavan Kumar, K L University "Design and Analysis of CMOS Schmitt Trigger"
2. Pranay Kumar Rahi, Shashi Dewangan, Tanuj Yadav, Md Muzaherul Haque, “Design and Simulation of CMOS Schmitt Trigger” IJISET - International Journal of Innovative Science, Engineering & Technology, Vol. 3 Issue 8, August 2016.
3. Nahid A Jahan, Mohammad Fairuz Bin Amir, Md. Ashraful Islam, M Mofazzal Hossain, Mamun Bin Ibne Reaz, “Design and Performance Analysis of Low Voltage and Low Power Schmitt Trigger for 0.18 μm CMOS Process” IOSR Journal of VLSI and Signal Processing (IOSR-JVSP) Volume 11, Issue 3, Ser. I (May. - June. 2021), PP 01-17.
