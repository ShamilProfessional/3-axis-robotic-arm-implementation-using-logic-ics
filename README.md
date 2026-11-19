# 3-Axis Robotic Arm Using Logic ICs

## Introduction

This project uses logic ICs to control a three-axis robotic arm with 28BYJ-48 stepper motors.

## What the Project Does

Use the UP and DOWN push buttons to control each joint. Each motor moves independently. The UP button moves its motor clockwise. The DOWN button moves it counter-clockwise.

## How It Works

The control circuit generates a four-bit pattern for the motor coils. The pattern uses wave drive, also called one-phase-on drive. It energises one coil at a time.

The 28BYJ-48 has four phase inputs. In the table, `1` means that the phase is energised and `0` means that it is off. The order of the phases depends on the motor wiring. If the motor turns in the opposite direction, reverse the sequence or swap the direction control.

### Wave-Drive Truth Table

| Step | A | B | C | D |
|---:|---:|---:|---:|---:|
| 1 | 1 | 0 | 0 | 0 |
| 2 | 0 | 1 | 0 | 0 |
| 3 | 0 | 0 | 1 | 0 |
| 4 | 0 | 0 | 0 | 1 |

Repeat the steps from 1 to 4 for one direction. Use the reverse order, 4 to 1, for the other direction. The phase labels are logical labels. Check the motor and driver wiring before connecting the circuit. Use a suitable driver stage for the motor coil current; do not connect the motor coils directly to logic IC outputs.

Each motor has four coils. The circuit energises the coils in order to rotate the motor. Reversing the order reverses the motor direction.

## Clock and Step Pattern

A 74HC193 four-bit up/down counter provides the step count. The two least significant bits select one of four states. A 74HC139 two-to-four decoder changes those states into the coil pattern. A NE555 timer provides the common clock.

The 74HC139 outputs are active low. NOT gates invert these outputs where the circuit needs active-high signals. Two 74HC139 ICs can provide the decoder outputs for all three motors because each IC contains two decoders.

## Direction and Button Control

The motor must hold its current position when neither button is pressed. It must move clockwise when UP is pressed and counter-clockwise when DOWN is pressed. It must hold its position when both buttons are pressed.

The 74HC193 has separate count-up and count-down clock inputs. The control logic sends clock pulses to the correct input for the selected direction and prevents pulses when the motor must hold its position.

<!-- Add the 74HC193 datasheet or counter-input diagram here. Example: ![74HC193 counter inputs](media/images/74hc193-counter-inputs.png) -->

### Control Logic Design

<!-- Add the first control-logic image here. Example: ![Control logic diagram 1](media/images/control-logic-1.png) -->

<!-- Add the second control-logic image here. Example: ![Control logic diagram 2](media/images/control-logic-2.png) -->

The control logic uses 74HC08 AND gates and 74HC04 NOT gates.

## Push Buttons

The circuit uses 6 × 6 mm, four-pin push buttons. The buttons use active-low signals. A 74HC14 Schmitt-trigger IC debounces the button signals and inverts them to active-high signals for the control logic.

## Three-Motor Circuit

The control circuit is repeated for each motor. This lets you control each joint separately. The schematic shows the full circuit and the shared decoder arrangement.

<!-- Add the full schematic here. Example: ![Full robotic arm control schematic](schematics/full-schematic.png) -->

## Final Result

<!-- Add a photo of the completed robotic arm here. Example: ![Completed 3-axis robotic arm](media/images/final-result.jpg) -->

## Project Report

[Open the project report PDF](Robotic_Arm_Project_Report.pdf)

## Project Media

Add project photos to `media/images/` and demonstration videos to `media/videos/`. For example:

```markdown
![Working prototype](media/images/working-prototype.jpg)

[Watch the demonstration video](media/videos/robot-arm-demo.mp4)
```

## 3D Files

Add CAD models and other 3D files to `3d-files/` when they are available.
