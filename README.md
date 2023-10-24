<p align="center">
 <img src=https://github.com/Syedhasan7/pes_asic_class/assets/109273742/48e086c4-f9dc-4999-a642-022b538860c5)
</p>

                                                                                                

# PULSE WIDTH MODULATION (PWM) GENERATOR
## Introduction 
 In power electronics, pulse width modulation is a proven effective technique that is used to control semiconductor devices. Pulse width modulation or PWM is a commonly used control technique that generates analog signals from digital devices such as microcontrollers. The signal thus produced will have a train of pulses, and these pulses will be in the form of square waves. Thus, at any given time, the wave will either be high or low.
 
  Pulse width modulation reduces the average power delivered by an electrical signal by converting the signal into discrete parts. In the PWM technique, the signal’s energy is distributed through a series of pulses rather than a continuously varying (analog) signal.

## How is a PWM Signal Generated?
+ A pulse width modulating signal is generated using a comparator. The modulating signal forms one part of the input to the comparator, while the non-sinusoidal wave or sawtooth wave forms the other part of the input. The comparator compares two signals and generates a PWM signal as its output waveform.
   
+ If the sawtooth signal is more than the modulating signal, then the output signal is in a “High” state. The value of the magnitude determines the comparator output which defines the width of the pulse generated at the output.

<p align="center">
<img width="497" alt="image" src="https://github.com/Veda1809/pes_pwm/assets/142098395/392b9d15-4708-4608-a780-3d552ad8f41c">
</p>

## Duty Cycle of PWM
+ As we know, a PWM signal stays **ON** for a given time and stays **OFF** for a certain time. The percentage of time for which the signal remains **ON** is known as the duty cycle. If the signal is always **ON**,  then the signal must have a 100 % duty cycle. The formula to calculate the duty cycle is given as follows:

<p align="center">
<img width="245" alt="image" src="https://github.com/Veda1809/pes_pwm/assets/142098395/51885dab-c5a3-42d9-9eca-5e0edacd9a76">
</p>

+ The average value of the voltage depends on the duty cycle. As a result, the average value can be varied by controlling the width of the **ON** of a pulse.

## Frequency of PWM

<p align="center">
<img width="444" alt="image" src="https://github.com/Veda1809/pes_pwm/assets/142098395/41eb8f1e-599f-4df5-be9e-81064587db6e">
</p>

+ This PWM generator generates 10Mhz signal. We can control duty cycles in steps of 10%. The default duty cycle is 50%. Along with clock signal we provide another two external signals to increase and decrease the duty cycle.

<p align="center">
<img width="500" alt="image" src="https://github.com/Veda1809/pes_pwm/assets/142098395/2907a4a6-ee83-41e9-a97f-c1f534377548">
</p>

+ The key components we need for this particular circuit are an n-bit counter and comparator. The duty passed to the comparator is compared to the counter's current value. If the counter's current value is less than the required value, the comparator produces a high output. Similar to this, if the counter's current value is higher than its duty, the comparator's output will be low. Since the counter starts at zero, the comparator initially produces a large output, which decreases as the counter approaches its duty. Therefore, we can manage duty cycle by managing duty.

+ Since the counter is sequential and the comparator is a combinational circuit, there may be an intermediate state like 111 that is higher or lower than duty when counting from 011 to 100 as a result of inappropriate delays. A glitch might result from this. The output of the comparator is routed through a D flipflop in order to prevent these errors.

## Advantages
+ It prevents overheating of LED while maintaining its brightness.
+ It is accurate and has a fast response time.
+ It provides a high input power factor.
+ It helps motors generate maximum torque even when they run at lower speeds.

## Disadvantages
+ As the PWM frequency is high, switching losses are considerably high.
+ It induces Radio Frequency Interference (RFI).

## Applications
+ Used in telecommunication for encoding purposes.
+ Helps in voltage regulation and therefore is used to control the speed of motors.
+ Controls the fan inside a CPU of the computer, thereby successfully dissipating the heat.
+ Used in Audio/Video Amplifiers.

## Installation
For installation and more details regarding iverilog, yosys and gtkwave, refer to :

https://github.com/Syedhasan7/pes_asic_class
## Simulation

+ `iverilog pes_pwm.v pes_pwm_tb.v`
+ `./a.out`
+ `gtkwave pwm.vcd`

![Screenshot from 2023-10-19 14-04-27](https://github.com/Syedhasan7/pes_pwm/assets/109273742/b30ce95f-9972-4c45-b16d-81d8e68d7504)
![Screenshot from 2023-10-19 14-05-04](https://github.com/Syedhasan7/pes_pwm/assets/109273742/f49336c5-b918-4680-a60b-9fd8bdd30be8)

## Synthesis
+ Invoke `yosys`
+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog pes_pwm.v`
+ `synth -top pes_pwm`
+ `dfflibmap -liberty lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
+ `abc -liberty lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `flatten`
+ `write_verilog pes_pwm_netlist.v`
+ `show pes_pwm`

![Screenshot from 2023-10-19 14-42-18](https://github.com/Syedhasan7/pes_pwm/assets/109273742/d0ccde08-1470-4d38-80e8-12d5eac88d31)

![Screenshot from 2023-10-19 14-42-40](https://github.com/Syedhasan7/pes_pwm/assets/109273742/9c0c2684-7a90-4c13-9eeb-c84ad1ded332)

![Screenshot from 2023-10-19 14-45-18](https://github.com/Syedhasan7/pes_pwm/assets/109273742/e3ad1b36-e397-4932-bd3d-528a2cf4b83d)


## Gate-Level Simulation

+ `iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v pes_pwm_netlist.v pes_pwm_tb.v`
+ `./a.out`
+ `gtkwave pwm.vcd`
![Screenshot from 2023-10-19 14-53-05](https://github.com/Syedhasan7/pes_pwm/assets/109273742/1534e620-1f6d-412f-b40b-08d977ed9ffc)

![Screenshot from 2023-10-19 14-54-02](https://github.com/Syedhasan7/pes_pwm/assets/109273742/8a81b642-7d5b-4c1b-bb18-21ed1d37426d)


We can observe that output of functional simulation is matching with the output of gate level simulation, this means that the netlist generated by yosys is correct.
