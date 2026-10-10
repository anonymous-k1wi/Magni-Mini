# Magni-Mini
The Magni Mini is an ELRS-compatible dual brushed ESC and PWM breakout board built for combat robotics, similar to the [Malenki Nano](https://github.com/MarkR42/malenki-nano).  This repository serves as the documentation and manual for the Magni Mini.

## Disclaimer and Liability
Combat robotics, by their nature, are dangerous.  It is your responsibility to follow best safety practices and protect yourself and the people and property around you.


## Table of Contents
- Overview
- Quick Start Guide
- In-Depth Setup
- Settings
- FAQ

## Overview
The Magni Mini is an ELRS-compatible dual brushed ESC with additional PWM outputs, built from the ground up with combat robotics in mind.  It adopts the same form factor as the popular [Malenki Nano](https://github.com/MarkR42/malenki-nano), making it a drop-in upgrade for those wishing for better motor drivers, extended PWM signals, and compatibility with the popular [ELRS ecosystem](https://github.com/ExpressLRS/ExpressLRS).

### Features:
- ELRS V4 UART/CRSF receiver compatibility
- 2-6S battery voltage input
- Dual DRV8231 3.7A motor drivers
- Optional extended PWM outputs (servo stretching)
- RGB LED for user feedback
- Optional on-board configurable mixing
- Configuration mode

## Quick Start Guide
### Wiring
A [BetaFPV ELRS Lite receiver](https://betafpv.com/products/elrs-lite-receiver) (flat antenna) can be attached to the Magni Mini board via the castellated pins between the support forks.  With the Magni Mini board facing upwards (LED up), the BetaFPV ELRS Lite receiver should be facing downwards (red antenna down).  Verify that the castellated pin markings are correct, where: 
- GND -> GND
- 5V -> 5V
- RX -> TX
- TX -> RX 
(for UART connections, RX and TX should swap between devices)

Solder the receiver on laying flat, starting with a single pin.  When satisfied with the alignment, proceed to the remaining pins, ensuring each has a solid connection between the receiver and the Magni Mini on both sides.

Attach the remaining power and peripheral device wires to the Magni Mini, using the following wire diagram for reference.

### Mixing
If mixing on the controller (recommended) the channel outputs should match the following:
- CH1: Weapon
- CH2-CH3: Drive motor outputs
- CH4-CH5: Additional Weapon/Servo 

If us

### Hardware Settings
There are 4 settings that can be changed exclusively via solder bridges.  Each is marked below on the diagram.

The "E" pads next to the PWM 4 and 5 output pads can be used to enable extended PWM (500-2500) on the respective channels.  This is intended for use with compatible servos.  By default (when unbridged), this feature is disabled.

The "Coasting" pad disables motor breaking and enables motor coasting when bridged.  This is not recommended based on personal experience and the motor driver manufacturer's recommendation, but is available as a feature if desired.

The "Mixing" pad enables on-board mixing when bridged, removing the need to program the model mix on your transmitter.  For any transmitters running EdgeTX, this is not recommended due to the lack of flexibility and adjustment.  This feature is intended for use with budget ELRS controllers that do not have the ability to properly create mixes due to a lack of software.

### Software Settings
To access software settings, assign a button to the CH6 output on your transmitter.  Holding this button high for 5 seconds will enter settings mode (blue LED).  To toggle settings, tap the CH6 button the number of times for the desired setting, then wait for 2.5s.  The LED will flash green the same number of times the button was pressed to confirm.  To exit settings mode, hold the CH6 button for 5 seconds until the LED turns purple, then release.

Button Presses:
1 - LED Brightness (Low/Medium/High) - Default High
2 - 
3 - 
4 -
5 - 
6 - 
7 - 


## In-Depth Setup
### Receiver Mounting
The Magni Mini is designed to interface with any unmodified UART/CRSF output ELRS receiver.  That means no custom firmware, special setup parameters, or PWM modification is necessary.  While any 


to accept a [BetaFPV ELRS Lite Receiver](https://betafpv.com/products/elrs-lite-receiver) (flat antenna) for optimal mounting.
