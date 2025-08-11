# Project Overview: Key Modules and Components

This project consists of several important modules and circuits designed for digital logic, CPU implementation, memory management, input/output control, and timer functionality. Below is an overview of each major component and its purpose.

---

## 1. CPU Implementation

- Uses 8-bit instructions with the first 5 bits as the opcode (20 variants).  
- Instructions are 24 bits wide, with unused bits padded by zeros on the right.  
- GPIO has 8 output LEDs indicating pin values (1 for input signal, 0 for output signal).  
- ROM stores instructions with opcodes such as LOAD, LOADI, STORE, ALU operations, JUMP, BRNE, BREQ, pin mode change, and digitalWrite-like commands.  
- Timer interrupt triggers a secondary 4-address ROM; main instructions pause and resume after completion.

---

## 2. 8-Bit Input to 7-Segment Display via BCD Conversion

- Converts an 8-bit binary input to BCD using the **double dabble** algorithm (implemented in `BIN2BCD` and `helper` circuits).  
- Uses `BCD7SEGMENT` and `BCD7SEG` helper circuits to convert each BCD digit (0-9) to corresponding 7-segment display signals.  
- Supports full range up to 255 (max 8-bit value), requiring a 10-bit BCD output.  
- Final output drives the 7-segment display.

---

## 3. 8-Bit Memory with RS Flip-Flops

- Built from RS flip-flops to create an 8-bit memory cell.  
- Four such memory cells cascaded to form the main memory (`mainMemo`).  
- Controlled by buttons:  
  - `Address` to select memory location,  
  - `Write` to store input to selected address,  
  - `Begin` to start address counting (with blinking indicators),  
  - `Stop` to halt counting (with indicators turned off).  
- `mainMemo` receives input, address, start, and stop signals to manage read/write operations and visual feedback.

---

## 4. Input Processing and Display Control Submodules

Five submodules coordinate input handling and display:

- **Transpose:** Corrects input orientation for proper screen display (otherwise image is reversed).  
- **SpeedControl:** Adjusts speed using clock ticks.  
- **CoordinateJoysticks:** Uses 6D triggers to determine joystick position; compares input to 16, then adds/subtracts accordingly.  
- **ObjectMove:** Controls generated object movement; lights up pixels at positions `y, y+1, y+2, y+3`.  
- **Addition:** Combines all input and movement data for a 64x64 matrix display.

---

## 5. DAC, ADC, and Timer Circuits

- **DAC:** Converts digital input to analog voltage using an 8-bit R2R ladder and buttons for voltage adjustment.  
- **ADC:** Converts analog signals to digital using 10 comparators and an encoder to display the value; quantization error corrected by halving resistances at the first and last resistor.  
- **Timer:**  
  - Prescaler divides the clock.  
  - Rotation ticks set manually and adjustable by input.  
  - Helper circuits generate `IFOCA` and `IFOCB` signals from outputs and enable signals.  
  - Waveform helper generates `WGMO` from `WGM`.  
  - Interrupt signal triggers when `IFOCA` or `IFOCB` is set.  
  - All circuits integrated in the main timer module.

---

Feel free to request detailed diagrams, timing charts, or deeper explanations of any module.
