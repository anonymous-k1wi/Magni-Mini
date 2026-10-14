# Magni-Mini
Magni Mini is an ELRS-compatible dual brushed ESC and PWM breakout board built for combat robotics.  This repository serves as the documentation and manual for the Magni Mini.

## Disclaimer and Liability
Combat robots have the potential to be dangerous.  It is your responsibility to follow best safety practices and take the proper steps to protect yourself and the people and property around you.

The manufacturers and distributors of this product are not responsible for your safety and not liable for any damage or harm caused by the use, proper or improper, of this device.  By using this device, you acknowledge this and accept the full responsibilities for the setup, use, and operation of this device.

## Table of Contents
- [Overview](https://github.com/anonymous-k1wi/Magni-Mini/blob/main/README.md#overview)
- [Quick Start Guide](https://github.com/anonymous-k1wi/Magni-Mini/blob/main/README.md#quick-start-guide)
- [In-Depth Setup](https://github.com/anonymous-k1wi/Magni-Mini/blob/main/README.md#in-depth-setup)
- [Settings](https://github.com/anonymous-k1wi/Magni-Mini/blob/main/README.md#settings)
- [FAQ](https://github.com/anonymous-k1wi/Magni-Mini/blob/main/README.md#troubleshooting--faq)

## Overview
The Magni Mini is an ELRS-compatible dual brushed ESC with additional PWM outputs, built from the ground up with combat robotics in mind.  It adopts the same form factor as the popular [Malenki Nano](https://github.com/MarkR42/malenki-nano), making it a drop-in upgrade for those wishing for better motor drivers, extended PWM signals, and compatibility with the popular [ELRS ecosystem](https://github.com/ExpressLRS/ExpressLRS).

<img width="710" height="500" alt="IMG_2994" src="https://github.com/user-attachments/assets/1db4ff31-0d2e-44ba-8fa5-b63d1ecb9a92" />  

<sup> *Board comparison with Magni Mini (left), Malenki Nano (right)* </sup>

<img width="500" height="500" alt="magni_front_scale_downscaled" src="https://github.com/user-attachments/assets/f01ec282-2920-4835-8c56-082ed9d47f0c" />

<sup> *Magni Mini Board with dimensions* </sup>

### Features:
- ELRS V4 UART/CRSF receiver compatibility
- 2-6S battery voltage input
- Dual DRV8231 3.7A motor drivers
- 3 PWM outputs
- Optional extended PWM outputs (servo stretching)
- RGB LED for user feedback
- Optional on-board mixing
- Configuration mode

## Quick Start Guide
The Quick Start Guide is intended to get you up and running, well, quick.  This means that some information is passed over or skipped here.  For a full explanation of features and settings, review the information in the in-depth [documentation](https://github.com/anonymous-k1wi/Magni-Mini/blob/main/README.md#in-depth-setup) following this section and in the [FAQ](https://github.com/anonymous-k1wi/Magni-Mini/blob/main/README.md#troubleshooting--faq). 

### Wiring
A [BetaFPV ELRS Lite receiver](https://betafpv.com/products/elrs-lite-receiver) (not included) can be attached to the Magni Mini board via the castellated pins between the support forks.  With the Magni Mini board facing upwards (LED up), the BetaFPV ELRS Lite receiver should be facing downwards (red antenna down).  Verify that the castellated pin markings are correct, where: 
- GND -> GND
- 5V -> 5V
- RX -> TX
- TX -> RX 
(for UART connections, RX and TX should swap between devices)

Solder the receiver on laying flat, starting with a single pin.  

<img width="375" height="500" alt="one_solder" src="https://github.com/user-attachments/assets/480c6cb2-4c5e-495b-ad16-2b8e0914f343" />

<sup> *ELRS receiver soldered with a single connection* </sup>

When satisfied with the alignment, proceed to the remaining pins, ensuring each has a solid connection between the receiver and the Magni Mini on both sides.

<img width="375" height="500" alt="all_solder" src="https://github.com/user-attachments/assets/f1fae401-cc09-4f39-a2ef-da51b0e7a311" />

<sup> *ELRS receiver with all connections soldered* </sup>

Alternatively, the ELRS receiver can also be of the Magni Mini, allowing for a smaller but thicker form factor.  For more details, see "[Reverse Flip Mounting](https://github.com/anonymous-k1wi/Magni-Mini/blob/main/README.md#Reverse-Flip-Mounting)" 

<img width="667" height="500" alt="reverse_flip" src="https://github.com/user-attachments/assets/8c46750d-7477-4445-9ce9-ccc40cae7644" />

<sup> *ELRS receiver mounted in the reverse/flip configuration* </sup>

Attach the remaining power and peripheral device wires to the Magni Mini, using the following wire diagram for reference.

<img width="500" height="500" alt="magni_front_diagram_downscaled" src="https://github.com/user-attachments/assets/7f47e2d9-79d0-4539-9f51-40318e172f50" />  <img width="403" height="500" alt="wired" src="https://github.com/user-attachments/assets/da00f4bf-dd33-494f-afda-ba532ec7e037" />

<sup> *Magni Mini wiring diagram, example wired board* </sup>

After attaching all wires, cover the ELRS receiver and the Magni Mini with heat shrink to protect the receiver from bending forces.  For additional protection, the ELRS receiver can be epoxied to the Magni Mini support wings to better support it.

<img width="352" height="500" alt="shrunk" src="https://github.com/user-attachments/assets/147313c6-fc08-441a-945e-cb6d8a610999" />

<sup> *Magni Mini wired and covered in heat shrink to protect receiver* </sup>

### Transmitter Setup
Mixing can be done either on the controller (recommended for EdgeTX) or by the Magni Mini (recommended for basic ELRS controllers).  If mixing on the controller the channel outputs should match the following:
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

<img width="792" height="500" alt="magni_solder_bridges_downscaled" src="https://github.com/user-attachments/assets/285344ec-834a-4eef-9809-f60647b02407" />

<sup> *Magni Mini solder bridge locations* </sup>

The "E" pads next to the PWM 4 and 5 output pads can be used to enable stretching to access extended PWM (500-2500) on the respective channels.  This is intended for use with compatible servos.  By default (when unbridged), this feature is disabled.

The "Coasting" pad disables motor breaking and enables motor coasting when bridged.  This is not recommended based on personal experience and the motor driver manufacturer's recommendation, but is available as a feature if desired.

The "Mixing" pad enables on-board mixing when bridged, removing the need to program the model mix on your transmitter.  For any transmitters running EdgeTX, this is not recommended due to the lack of flexibility and adjustment.  This feature is intended for use with budget ELRS controllers that do not have the ability to properly create mixes due to a lack of software.

### Software Settings
To access software settings, assign a button to the CH6 output on your transmitter.  Holding this button high (>1500) for 5 seconds will enter settings mode (blue LED).  To toggle settings, tap the CH6 button the number of times (>1500) for the desired setting, then wait for 2.5s to confirm.  The LED will flash green the same number of times the button was pressed for visual confirmation.  To exit settings mode, hold the CH6 button for 5 seconds until the LED turns purple, then release.

Button Presses:
- (1) LED Brightness (Low/Medium/High) - Default High
- (2) Invert Motor 1 (True/False) - Default False
- (3) Invert Motor 2 (True/False) - Default False
- (4) Swap Motor 1 and Motor 2 Outputs, Invert Steering if Mixing Enabled (True/False) - Default False
- (5) Toggle Steering Power for Onboard Mixing (Low/High) - Default Low
- (6) Invert PWM4 (True/False) - Default False
- (7) Invert PWM5 (True/False) - Default False

## In-Depth Setup
### ELRS Receiver Setup
The Magni Mini is designed to interface with any unmodified UART/CRSF output ELRS receiver running V4 firmware.  That means no custom firmware, special setup parameters, or PWM modification is necessary.  While any UART receiver can work with it, it is specifically designed to accept a [BetaFPV ELRS Lite Receiver](https://betafpv.com/products/elrs-lite-receiver) (flat antenna) for optimal direct mounting.  

<img width="500" height="500" alt="ELRS_Lite_Receiver_Flat_Antenna_V1 2_side_view_720x" src="https://github.com/user-attachments/assets/e0f10dd1-b8b1-499f-b68e-63aea7c2c60e" />

<sup> *BetaFPV ELRS Lite receiver* </sup>

The HappyModel EP1/EP2 receivers have also been tested, which both fit but have less ideal antenna situations.  Other receivers of similar form factors will likely also fit, but have not been verified at this time.  Alternatively, using wires to attach the receiver instead of direct mounting it allow for other receivers to be used.

<img width="590" height="500" alt="IMG_3443" src="https://github.com/user-attachments/assets/aae28b77-1142-4279-9a02-26cc202434bd" />

<sup> *Magni Mini with BetaFPV ELRS Lite receiver (left) and HappyModel EP1 receiver (right)* </sup>


When setting up the ELRS receiver, the configuration process should be done "normally" through the ELRS configuration.  The receiver/transmitter are should be flashed to use ELRS V4.  The Magni Mini may work with older versions, but it has not been designed to do so or tested with them.  Forward compatibility with future versions of ELRS cannot be guaranteed but will be evaluated on a new major version release.  Be sure to also set up a bind phrase and... that's it.  The ELRS receiver should now be able to interface with the Magni Mini properly.  The Magni Mini communicates with the ELRS receiver via UART communication, specifically at the ELRS default 420000 baudrate, which should not be changed.

Due to ELRS default settings, there will be one more step you need to do if you intend to use the CH5 PWM output pad as by default ELRS only sends the first full channels at full resolution.  To extend this to the first 8, the [switch mode](https://www.expresslrs.org/software/switch-config/) needs to be changed.  In the ELRS Lua script on your transmitter, set the "Packet Rate" to "333Hz Full" and the "Switch Mode" to "8ch".  It is also advised to reassign the ELRS "[arm](https://www.expresslrs.org/software/switch-config/#whats-so-important-with-arming)" trigger if using CH5 for PWM, although it is often otherwise unused for combat robotics applications.  If you do not intend to use the CH5 PWM output, than these modifications are not necessary.

### Receiver Wiring
After flashing your receiver, it can now be connected to the Magni Mini board.  There are 3 main mounting methods to do so:
1. [Standard flat](https://github.com/anonymous-k1wi/Magni-Mini/blob/main/README.md#Standard-Flat-Mounting)
2. [Reverse flip](https://github.com/anonymous-k1wi/Magni-Mini/blob/main/README.md#Reverse-Flip-Mounting)
3. [Wired](https://github.com/anonymous-k1wi/Magni-Mini/blob/main/README.md#Wired-Mounting)
#### Standard Flat Mounting
For the standard method of mounting, the castellated pads of the Magni Mini and ELRS receiver are aligned, then directly soldered together.  The Magni Mini and most ELRS receivers use a standard pitch, so it should be compatible with a wide variety of receivers.

For nano/lite receivers, most should fit between the support wings of the Magni Mini (review the scaling diagram).  These support wings are designed to prevent bending or other external forces from damaging the hard-soldered direct connections between the boards.  While standard flat mounting is not recommended for larger receivers that do not fit between the support wings, it is still possible if the support wings are removed (see [Reverse Flip Mounting](https://github.com/anonymous-k1wi/Magni-Mini/blob/main/README.md#Reverse-Flip-Mounting)).

For easiest assembly, it is recommended to solder the ELRS receiver to the Magni Mini by first placing both flat on a solder-safe surface, then double-checking the alignment of the castellated pads.  Ground and 5V should both match between the receiver and Magni Mini, and RX and TX should be flipped.  With the recommended BetaFPV Lite receiver, this results in the red antenna side facing down when the Magni Mini board is facing upwards.

Once aligned, the receiver position can be fixed by "tacking" them together with a single solder joint between the two boards.  Using only a single solder joint initially makes it easier to reflow and adjust this connection until you are satisfied with the receiver position.

After aligned and tacked, the remaining joints can be soldered, one at a time, to create the solid connection between the Magni Mini and receiver.  Be sure to flip the board over to ensure there is adequate solder on both sides.

The remaining wires for power, motors, and PWM signals can then be attached.  Use the following diagram for reference.

<img width="500" height="500" alt="magni_front_diagram_downscaled" src="https://github.com/user-attachments/assets/7f47e2d9-79d0-4539-9f51-40318e172f50" />

After testing everything is working as expected, it is recommended to heat shrink the entire board.  The support wings of the Magni Mini will hold the heat shrink, creating a protective sleeve that protects the receiver from bending.

If additional protection is required, it is also recommended to place a small amount of epoxy in the gaps between the receiver and Magni Mini to bond them together.   

#### Reverse Flip Mounting


#### Wired Mounting


## LED Modes
The Magni Mini board features an RGB LED for user feedback.  The LED can have the following colors, which each indicate different things:
- [Purple](https://github.com/anonymous-k1wi/Magni-Mini/blob/main/README.md#purple)
- [Orange](https://github.com/anonymous-k1wi/Magni-Mini/blob/main/README.md#orange)
- [Red](https://github.com/anonymous-k1wi/Magni-Mini/blob/main/README.md#red)
- [Blue]
- [Green]

<img width="540" height="500" alt="magni_led" src="https://github.com/user-attachments/assets/3b370f41-bc09-4b8b-b383-9380e167e9ff" />

<sup> *Magni Mini RGB LED meanings* </sup>

### Purple
The LED will hold a steady purple color during normal operation.  This indicates that it is receiving communication from an ELRS receiver, the receiver is actively connected to a transmitter, and the motor drivers and PWM signal generators are active.  If the ELRS receiver disconnects from the transmitter in this mode (intentionally or accidentally), the LED will turn [red](https://github.com/anonymous-k1wi/Magni-Mini/blob/main/README.md#red) and the PWM generation and motor drivers will be deactivated.

### Orange
On startup, the LED will hold a steady orange color to indicate it is in standby.  This means that it recognizes an ELRS receiver is present, but that the receiver has not yet connected to a transmitter.  The motor drivers and PWM signal generation are not active in this mode.  Once the ELRS receiver has an active link with the transmitter, the Magni Mini will transfer into normal operation mode ([Purple LED](https://github.com/anonymous-k1wi/Magni-Mini/blob/main/README.md#purple)) and it will not be able to re-enter the startup standby mode.

### Red
A red LED indicates that an error or failsafe has occurred during operation.  The most likely cause for a red LED to appear is an ELRS disconnection (intentional or accidental), but it is also possible for general errors communicating with the receiver to cause this.  When the LED is red, the Magni Mini is in a "failsafe" mode where no PWM signals are generated and the motor drivers are not active.  The Magni Mini will continually check if the ELRS disconnect has been resolved, and if a connection to the transmitter is found, it will return to normal operation ([Purple LED](https://github.com/anonymous-k1wi/Magni-Mini/blob/main/README.md#purple)).

### Blue
The LED will turn blue when in the software settings edit mode.  This is described in more detail in the [software settings section](https://github.com/anonymous-k1wi/Magni-Mini/blob/main/README.md#software).

### Green
The LED will flash green in the software settings edit mode to confirm settings changes.  This is described in more detail in the [software settings section](https://github.com/anonymous-k1wi/Magni-Mini/blob/main/README.md#software).



## Settings
There are two major ways to change settings on the Magni Mini - in [hardware](https://github.com/anonymous-k1wi/Magni-Mini/blob/main/README.md#hardware) and in [software](https://github.com/anonymous-k1wi/Magni-Mini/blob/main/README.md#software).
### Hardware
All hardware settings changed by bridging solder pads on the board, labelled on the diagram below.  These are set as physical solder bridges that are read on power on to prevent accidental software overwrites and to ensure purposeful usage.  Do not solder bridges while board is actively powered as it will not change the setting until the next reboot (and you should not solder actively powered electronics).

<img width="792" height="500" alt="magni_solder_bridges_downscaled" src="https://github.com/user-attachments/assets/285344ec-834a-4eef-9809-f60647b02407" />

<sup> *Magni Mini solder bridge locations* </sup>

The "E" pads next to the PWM 4 and 5 output pads can be used to enable extended PWM (500-2500) on the respective channels.  This is intended for use with compatible servos and can extend the turning angle range.  By default (when unbridged), this feature is disabled and a "standard" PWM signal (1000-2000) is output.  This feature is not provided for the PWM 1 output pad (W) as extended PWM is generally not used with weapon ESCs.

The "Coasting" pad disables motor breaking and enables motor coasting when bridged.  This is not recommended based on personal experience and the motor driver manufacturer's recommendation, but is available as a feature if desired.  This could *potentially* be useful in builds that already have a high drivetrain resistance and will stop quickly, but this should be preformed at your own risk.

The "Mixing" pad enables on-board drive mixing when bridged, removing the need to program the model mix on your transmitter.  When enabled, CH1 remains the weapon, CH2 becomes the input for forward/backward driving, and CH3 becomes the input for left/right turning.  Channels 4 and 5 remain untouched.  For any transmitters running EdgeTX, this is not recommended due to the lack of flexibility and adjustment, you are better off building your own mix that you can fully tune to your preferences.  This feature is intended to increase accessibility through use with budget ELRS controllers that do not have the ability to properly create mixes due to a lack of software (i.e. the RadioMaster T8L).  Despite this feature's existence, if you have not yet purchased a transmitter, it is recommended to purchase one that has full EdgeTX support.  It'll be worth it, I promise.

### Software

## Troubleshooting & FAQ
### My ELRS receiver isn't connecting to the Magni Mini!  How do I fix it?
Check the following likely configuration issues:
- The receiver/transmitter are running ELRS V4.  The Magni Mini may work with older versions, but it has not been designed to do so or tested with them.  Forward compatibility with future versions of ELRS cannot be guaranteed but will be evaluated on a new major version release.
- The receiver's buadrate is set to the default value (420000) in the ELRS wifi configuration menu.  This is unlikely to have been changed, but can cause issues if it has been.
- The wiring is correct.  Ensure that RX/TX swap between the receiver and the Magni Mini.

### How do I fix PWM Output 5 is jumping between low and high values?
By ELRS defaults, only channels 1-4 are sent at a full resolution, which is common for drones.  This can be changed.  In the ELRS Lua script, set the [packet rate and switch mode](https://www.expresslrs.org/software/switch-config/#channel-update-rate-versus-packet-rate) to one compatible with full resolution signals on channel 5.   Recommended settings are 333 and full resolution.

### Why is weapon on channel 1?
Safety.  The ELRS channels are sent as a single packet to the receiver, and the Magni Mini has to decode them.  This process starts with the first channel and ends with the last, which means that the channel 1 is processed first.  Since the weapon should have priority in any safety-critical moment, it is assigned to channel 1.
