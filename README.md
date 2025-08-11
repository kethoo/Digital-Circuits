# Project Overview: Key Modules and Components

This project consists of several important modules and circuits designed for digital logic, memory management, input/output control, and timer functionality. Below is an overview of each major component and its purpose.

---

## 1. 8-Bit Input to 7-Segment Display via BCD Conversion

- Converts an 8-bit binary input to BCD using the **double dabble** algorithm (implemented in `BIN2BCD` and helper circuits).  
- Uses `BCD7SEGMENT` and `BCD7SEG` helper circuits to convert each BCD digit (0-9) to corresponding 7-segment display signals.  
- Supports full range up to 255 (max 8-bit value), requiring a 10-bit BCD output.  
- Final output drives the 7-segment display.

---

## 2. 8-Bit Memory with RS Flip-Flops

- Built from RS flip-flops to create an 8-bit memory cell.  
- Four such memory cells cascaded to form the main memory (`mainMemo`).  
- Controlled by buttons:  
  - **Address** to select memory location,  
  - **Write** to store input to selected address,  
  - **Begin** to start address counting (with blinking indicators),  
  - **Stop** to halt counting (with indicators turned off).  
- `mainMemo` receives input, address, start, and stop signals to manage read/write operations and visual feedback.

---

## 3. Input Processing and Display Control Submodules

Five submodules coordinate input handling and display:

- **Transpose:** Corrects input orientation for proper screen display (otherwise image is reversed).  
- **SpeedControl:** Adjusts speed using clock ticks.  
- **CoordinateJoysticks:** Uses 6D triggers to determine joystick position; compares input to 16, then adds/subtracts accordingly.  
- **ObjectMove:** Controls generated object movement; lights up pixels at positions `y, y+1, y+2, y+3`.  
- **Addition:** Combines all input and movement data for a 64x64 matrix display.

---

## 4. DAC and ADC Circuits

- **DAC:**  
  - Converts digital input to analog voltage using an 8-bit R2R ladder.  
  - Includes buttons for voltage adjustment.

- **ADC:**  
  - Converts analog signals to digital using 10 comparators and an encoder to display the value.  
  - Quantization error corrected by halving resistances at the first and last resistors.

---

## 5. Timer Circuit

- **Prescaler** divides the clock frequency.  
- Rotation ticks are manually set and adjustable according to input.  
- Helper circuits generate `IFOCA` and `IFOCB` signals from outputs and enable signals.  
- Waveform helper generates `WGMO` from `WGM`.  
- Interrupt signal triggers when either `IFOCA = 1` or `IFOCB = 1`.  
- All circuits are integrated into the main timer module.

---
