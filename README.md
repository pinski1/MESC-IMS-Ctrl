# MESC IMS ESC
A derivative of the Molony ESC. STM32F303 based BLDC logic board designed to interface to an IMS power stage.

Please see https://github.com/davidmolony/MESC_FOC_ESC for further details.

## MESC_IMS_ESC.sch

* Using STM32F303 like MESC_FOC_ESC
* Using USB 2.0 type C connector for future compatibility
* Using VESC-style connectors for control & hall effect sensors
* Has facility to monitor a thermistor mounted to the power stage PCB
* Can monitor the battery voltage
* Can be powered via USB for configuration on the desk

## psu.sch
This sheet contains the power supplies for the ESC. It's designed to accept +40-50V input but won't activate at voltages less than +25V. The LM5-017 is a popular and robust SMPS buck convertor. To minimise supply rail noise but supply the requisite ripple for the feedback circuitry the Texas Instruments application note here: https://www.ti.com/lit/an/snva166a/snva166a.pdf was consulted.

By using a coupled inductor it is possible to get a 2nd, unregulated, output that can be 'stacked' on top of the regulated output. This provides a ~10V supply for the gate drivers. This method of using a coupled inductor to generate a 2nd output is detailed in this Texas Instruments application note here: https://www.ti.com/lit/pdf/snva674.

The +3V3 rail for the microcontroller and current amplifiers comes from a standard SOT23-5 LDO. This minimises noise artefacts and is a simple, low cost, low complexity way of generating this rail.

## phase.sch
As this board will plug into the separate power stage PCB it was decided to use isolated gate driver chips. As the gate signals are treated as differential signals this should hopefully allow for fast control while minimising noise, minimising ripple and self-turn-on. The UCC21520 is another well regarded chip. 

The INA240 is used for high speed current sensing, it will take the differential phase current sense signals at the phase voltage and convert them to a single ended current signal with 0A being around 1.65V. There is no additional filtering as this will affect the response of the current amplifier.