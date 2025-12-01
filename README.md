# Kalem-4-Channel-Isolated-PNP-Output

Isolated 4-channel 12–24 V PNP (high-side) output module for driving industrial loads from a 3.3 V / 5 V microcontroller or PLC.

This repository contains hardware design files, firmware examples and documentation for the **Kalem-4-Channel-Isolated-PNP-Output** board.

---

## 1. Overview

The Kalem-4-Channel-Isolated-PNP-Output is a compact module that provides four optically isolated, high-side MOSFET outputs for 12–24 V DC loads.

Each channel:

- Is controlled from a 3.3 V or 5 V logic signal
- Isolated by an optocoupler (LTV-817S series)
- Uses a P-channel MOSFET (SP40P18P8) to **source** the supply voltage to the load (PNP-style output)
- Has a built-in flyback diode for inductive loads and an output status LED

The board also includes reverse-polarity and surge protection on VIN, plus a power LED and optional jumper to tie MCU ground and load ground together.

---

## 2. Main Features

- 4 × high-side PNP-style outputs for 12–24 V DC loads  
- Per-channel optical isolation between MCU and load side  
- Compatible with 3.3 V and 5 V logic control inputs  
- P-channel MOSFET outputs (40 V rated) with low R<sub>DS(on)</sub>  
- Reverse-polarity protection (SS34) on VIN  
- TVS diode (SMBJ33CA) on the supply for surge protection  
- Flyback diode (SS34) per channel for inductive loads  
- Per-channel output status LEDs + global power LED  
- Separate **MCU_GND** and **GND_BOARD** with optional jumper (H1)  
- KF128-5.0 screw terminals for VIN and load outputs  
- 2.54 mm pin header for MCU interface  

> **Note:** Exact current ratings and thermal limits are given in the PDF datasheet in the `docs/` folder.

---

## 3. Typical Applications

- PLC-style 24 V PNP output expansion for MCUs or small PLCs  
- Controlling relays, contactors, solenoid valves and lamps  
- Building automation, HVAC control and general industrial I/O  
- Any application where you need **sourcing** outputs with galvanic isolation  

---

## 4. Hardware Overview

### 4.1 Power and Loads

- **VIN terminal (2-pin KF128-5.0)**  
  - Pin 1: `V+` (12–24 V DC input)  
  - Pin 2: `GND_BOARD`  

- **LOAD1–LOAD4 terminals (2-pin KF128-5.0 each)**  
  - Pin 1: `LOAD_OUT_x` – switched positive output (channel 1–4)  
  - Pin 2: `GND_BOARD` – connect to load ground / system ground  

> Connect each load between `LOAD_OUT_x` and **ground**.  
> When the channel is ON, the board sources V+ to the load.

### 4.2 MCU Interface (H3, 2.54 mm header)

| Pin | Name        | Description                            |
| --- | ----------- | -------------------------------------- |
| 1   | MCU_CTRL_1  | Channel 1 control input (active HIGH) |
| 2   | MCU_CTRL_2  | Channel 2 control input (active HIGH) |
| 3   | MCU_CTRL_3  | Channel 3 control input (active HIGH) |
| 4   | MCU_CTRL_4  | Channel 4 control input (active HIGH) |
| 5   | MCU_VCC     | MCU logic supply (3.3–5 V)            |
| 6   | MCU_GND     | MCU ground                            |

### 4.3 Ground Jumper (H1)

- **Open**: MCU side and load side are galvanically isolated  
- **Fitted**: `MCU_GND` is tied to `GND_BOARD` (non-isolated reference)

---

## 5. Basic Connection Example

1. Connect a 12–24 V DC supply to the VIN connector (`V+`, `GND_BOARD`).
2. Connect each DC load between `LOAD_OUT_x` and ground.
3. Provide 3.3 V or 5 V to `MCU_VCC` and connect `MCU_GND` to your controller ground.
4. Drive `MCU_CTRL_x` **HIGH** to turn channel **ON**, **LOW** to turn it **OFF**.
5. Decide if you need isolation:
   - Leave jumper **H1 open** for galvanic isolation.
   - Fit jumper **H1** if you want MCU and load grounds tied together.

---
