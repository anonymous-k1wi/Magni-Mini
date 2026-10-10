# Magni-Mini
Magni Mini is an ELRS-compatible dual brushed ESC and PWM breakout board built for combat robotics.  This repository serves as the documentation and manual for the Magni Mini.

## Disclaimer and Liability
Combat robotics have the potential to be dangerous.  It is your responsibility to follow best safety practices and take the proper steps to protect yourself and the people and property around you.

The manufacturers and distributors of this product are not responsible for your safety and not liable for any damage or harm caused by the use, proper or improper, of this device.  By using this device, you acknowledge this and accept the full responsibilities for the setup, use, and operation of this device.

## Table of Contents
- Overview
- Quick Start Guide
- In-Depth Setup
- Settings
- [FAQ](https://github.com/anonymous-k1wi/Magni-Mini/blob/main/README.md#FAQ)

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
The Quick Start Guide is intended to get you up and running, well, quick.  This means that some information is passed over or skipped here.  For a full explanation of features and settings, review the in-depth documentation following this section and in the FAQ. 

### Wiring
A [BetaFPV ELRS Lite receiver](https://betafpv.com/products/elrs-lite-receiver) (flat antenna) can be attached to the Magni Mini board via the castellated pins between the support forks.  With the Magni Mini board facing upwards (LED up), the BetaFPV ELRS Lite receiver should be facing downwards (red antenna down).  Verify that the castellated pin markings are correct, where: 
- GND -> GND
- 5V -> 5V
- RX -> TX
- TX -> RX 
(for UART connections, RX and TX should swap between devices)

Solder the receiver on laying flat, starting with a single pin.  When satisfied with the alignment, proceed to the remaining pins, ensuring each has a solid connection between the receiver and the Magni Mini on both sides.

Alternatively, the ELRS receiver can also be mounted on the backside of the Magni Mini, allowing for a smaller but thicker form factor.  This can be done by using flush cutters to remove the support wings, then attaching the receiver to the back with the same process.

Attach the remaining power and peripheral device wires to the Magni Mini, using the following wire diagram for reference.

After attaching all wires, cover the ELRS receiver and the Magni Mini with heat shrink to protect the receiver from bending forces.  For additional protection, the ELRS receiver can be epoxied to the Magni Mini support wings to better support it.

### Transmitter Setup
Mixing can be done either on the controller (recommended for EdgeTX) or by the Magni Mini.  If mixing on the controller the channel outputs should match the following:
- CH1: Weapon
- CH2-CH3: Drive motor outputs
- CH4-CH5: Additional Weapon/Servo

If mixing is enable on the Magni Mini (see [Hardware Settings](https://github.com/anonymous-k1wi/Magni-Mini/blob/main/README.md#hardware-settings) for instructions), the controller channel outputs should match the following:
- CH1: Weapon
- CH2: Forward/backwards drive channel input 
- CH3: Left/right drive channel input
- CH4-CH5: Additional Weapon/Servo

### Hardware Settings
There are 4 settings that can be changed exclusively via solder bridges.  Each is marked below on the diagram.

The "E" pads next to the PWM 4 and 5 output pads can be used to enable extended PWM (500-2500) on the respective channels.  This is intended for use with compatible servos.  By default (when unbridged), this feature is disabled.

The "Coasting" pad disables motor breaking and enables motor coasting when bridged.  This is not recommended based on personal experience and the motor driver manufacturer's recommendation, but is available as a feature if desired.

The "Mixing" pad enables on-board mixing when bridged, removing the need to program the model mix on your transmitter.  For any transmitters running EdgeTX, this is not recommended due to the lack of flexibility and adjustment.  This feature is intended for use with budget ELRS controllers that do not have the ability to properly create mixes due to a lack of software.

### Software Settings
To access software settings, assign a button to the CH6 output on your transmitter.  Holding this button high for 5 seconds will enter settings mode (blue LED).  To toggle settings, tap the CH6 button the number of times for the desired setting, then wait for 2.5s.  The LED will flash green the same number of times the button was pressed to confirm.  To exit settings mode, hold the CH6 button for 5 seconds until the LED turns purple, then release.

Button Presses:
- (1) LED Brightness (Low/Medium/High) - Default High
- (2) Invert Motor 1 (True/False) - Default False
- (3) Invert Motor 2 (True/False) - Default False
- (4) Invert Steering (True/False) - Default False
- (5) Toggle Steering Power (Low/High) - Default Low
- (6) Invert PWM4 (True/False) - Default False
- (7) Invert PWM5 (True/False) - Default False

## In-Depth Setup
### ELRS Receiver Setup
The Magni Mini is designed to interface with any unmodified UART/CRSF output ELRS receiver.  That means no custom firmware, special setup parameters, or PWM modification is necessary.  While any receiver can work with it, it is specifically designed to accept a [BetaFPV ELRS Lite Receiver](https://betafpv.com/products/elrs-lite-receiver) (flat antenna) for optimal mounting.  The HappyModel EP1/EP2 receivers have also been tested, which both fit but have less ideal antenna situations.  Other receivers of similar form factors will likely also fit, but have not been verified at this time.

When setting up the ELRS receiver, the configuration process should be done "normally" through the ELRS configurator.

## FAQ
### My ELRS receiver isn't connecting to the Magni Mini!  How do I fix it?
Check the following likely configuration issues:
- The receiver/transmitter are running ELRS V4.  The Magni Mini may work with other versions, but it has not been designed to do so or tested with them.  Compatibility with future versions of ELRS will be considered when they release.
- The receiver's buadrate is set to the default value (420000) in the ELRS wifi configuration menu.  This is unlikely to have been changed, but can cause issues if it has been.
- The wiring is correct.  Ensure that RX/TX swap between the receiver and the Magni Mini.

### PWM Output 5 is jumping between low and high values!  How do I fix it?
By ELRS defaults, only channels 1-4 are sent at a full resolution, which is common for drones.  This can be changed.  In the ELRS Lua script, set the [packet rate and switch mode](https://www.expresslrs.org/software/switch-config/#channel-update-rate-versus-packet-rate) to one compatible with full resolution signals on channel 5.   Recommended settings are 333 and full resolution.
