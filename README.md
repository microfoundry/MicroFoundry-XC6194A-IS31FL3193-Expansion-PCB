# MicroFoundry-XC6194A-IS31FL3193-Expansion-PCB
Information about the XC6194A Expansion PCB based on the IS31FL3193 IC to drive 3 LEDs and discrete logic to provide voltage translation

## Why?
I utilize the TOREX XC6194A in various projects and i2c is always available too. The IS31FL3193 RGB driver provides a unique set of features to redeuce MCU code making it an natural accessory to complement the XC6194 breakout.

## Description
The Micro Foundry XC6194A IS31FL3193 RGB Expansion PCB provides the ability to drive a RGB LED illuminated Momentary switch or up to 3 individual LED indicators (with common anode) in addition to offering voltage translation where the XC6194A switched VCC differs from MCU VCC. 

## IS31FL3193 Features
- One group RGB, single color LED breathing system-free pre-established pattern
- 3 independently controlled automatic and semiautomatic breathing system-free pre-established pattern
- 3 independently controlled outputs of 256 PWM steps 
- I2C interface, automatic address increment function 
- 2.7V to 5.5V supply voltage 
- 5 levels programmable output current (5mA~42mA)
- Over-temperature protection
- Operating temperature TA = −40°C ~ +85°C 
- 4x I2C addresses
- MCU controlled global shutdown in addition to software-based shutdown
- Breathing mark output signal for optional timed MCU control

**Please NOTE:** Color representation is totally dependent on the LEDs utilized. Therefore, there are no guarantees this LED driver will have the ability to produce the accurate color representation possible with 3x LEDs.

## Expansion PCB Features
- 3 Channels of LED switching with constant current control
- An additional "Power State" channel to provide a sink to LED channel 1 when XC6194 is in Off State (more details [below](/README.md#power-state-channel))
- Voltage translation on SW (Switch) output -> MCU input with Schmitt-Trigger input/inverted output
- Anode series resistor to provide global LED current control (more details [below](/README.md#anode-series-resistor))
- On-board micro switch for secondary XC6194A control
- Mount holes that will accept Wurth Electronics SMT Standoffs

## Pinouts
### Switch

| Pin | Function | Description | Voltage Potential |
| --- | -------- | ----------- | ---------- |
| 1 | SW | Momentary Switch Input (Active LOW) | XC6194A VIn |
| 2 | GND | Ground | |
| 3 | ANN |Common LED Anode | XC6194A VIn |
| 4 | LED1 | LED 1 Cathode | |
| 5 | LED2 | LED 2 Cathode | |
| 6 | LED3 | LED 3 Cathode | |

### IO (to MCU)

| Pin | Function | Description | MCU IO | Voltage Potential |
| --- | -------- | ----------- | ------ | ---------- |
| 1 | GND | Ground | | GND |
| 2 | SW | Switch Pressed | Input (Active HIGH) | MCU VCC |
| 3 | SHDN | Shutdown | Output (Active HIGH) | MCU VCC |
| 4 | PG | Power Good | Output (Active HIGH) **See NOTE-1** | XC6194A VIn |
| 5 | V_BM | Breathing Mark | Input | MCU VCC |
| 6 | SDB | IS31FL3193 Hardware Shutdown | Output (Active LOW) | MCU VCC |

**NOTE-1:** The Power Good Output is traditionally utilized to enable a downstream power supply, therefore the output operates at XC6194A VIn Potential. Please verify voltage compatibility before connecting.

### Expansion

| Pin | Function | Description | XC6194A IO | Voltage Potential |
| --- | -------- | ----------- | ---------- | ---------- |
| 1 | VIn | XC6194A Switched Voltage In | | XC6194A VIn |
| 2 | GND | Ground | | GND |
| 3 | VOut | XC6194A Switched Voltage Out | | XC6194A VOut |
| 4 | SW | XC6194A Momentary Switch | Input (Active LOW) | XC6194A VIn |
| 5 | PG | XC6194A Power Good | Output (Active HIGH) | XC6194A VIn |
| 6 | SHDN | XC6194A Shutdown | Input (Active HIGH) **See NOTE-2** | GND |

**NOTE-2:** Circuit is pulled to GND via pull-down resistor. XC6149A datasheet specifies a voltage level above 1.1v will trigger shutdown. Some MCUs may exhibit an output glitch on the SHDN during power-up and the XC6194 may immediately shutdown. If this is experienced, a user implemented RC filter could possibly eliminate the issue.

### STEMMA QT / Qwiic i2c 

| Pin | Function | Description | Voltage Potential |
| --- | -------- | ----------- | ---------- |
| 1 | GND | Ground | |
| 2 | VCC | Voltage In | MCU VCC |
| 3 | SDA | i2c Data | MCU VCC|
| 4 | SCL | i2c Clock | MCU VCC|

**NOTE-3:** i2c pull-up resistors are not populated. If this is the only i2c device on the bus, it is the manufacturer's recommendation is 4.74k Ohms. The location of the i2c pull-up resistors are noted in the following image:

**TODO:** Add image to indicate i2c pull-up location...

## Power State Channel
Channel 1 LED has a SPDT analog switch with its input referenced to VOut. When the XC6194A is in its off-state, the switch will connect the Channel 1 LED cathode to GND, therefore illuminating the LED. This can be useful to provide a visual indicator that the power is off. When the XC6194A is in its on-state, the switch will connect the Channel 1 LED cathode to the WS2811 which will be free to drive the LED. If there is no desire to have the Channel 1 LED illuminated when the power is off, this feature can be disabled by relocating the R1/R2 resistor as indicated in the following image:

**TODO:** Add image to indicate R1/R2 relocation...

## Anode Series Resistor
The resistor noted in the following image offers global current control via the common anode pin. The default value as manufactured is 0 Ohms (Zero) and can be replaced if necessary.

**TODO:** Add image to indicate R3 location...

## XC6194A Breakout PCB Variants
- [Micro Foundry XC6194A JST PH Style Breakout PCB](https://github.com/microfoundry/MicroFoundry-XC6194A-PH-Breakout-PCB)
- [Micro Foundry XC6194A Micro USB Breakout PCB](https://github.com/microfoundry/MicroFoundry-XC6194A-Micro-USB-Breakout-PCB)
- [Micro Foundry XC6194A USB-C Breakout PCB](https://github.com/microfoundry/MicroFoundry-XC6194A-USB-C-Breakout-PCB)

## XC6194A Expansion PCBs
- [Micro Foundry XC6194A Discrete Logic RGB Expansion PCB](https://github.com/microfoundry/MicroFoundry-XC6194A-Discrete-Logic-Expansion-PCB)
- [Micro Foundry XC6194A WS2811 RGB Expansion PCB](https://github.com/microfoundry/MicroFoundry-XC6194A-WS2811-Expansion-PCB)
- [Micro Foundry XC6194A IS31FL3193 RGB Expansion PCB](https://github.com/microfoundry/MicroFoundry-XC6194A-IS31FL3193-Expansion-PCB)
