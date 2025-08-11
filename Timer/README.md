## Timer Circuit Description

- The **Prescaler** circuit divides the clock (tact).  
- The number of ticks per one rotation is manually set and can change according to the input.  

- An additional **helper circuit** generates:  
  - `IFOCA` from `OCA` and `OIE`  
  - `IFOCB` from `OCB` and `OIE`  
  - Using constants like `255` and a counter `IFO`.  

- Another helper circuit, **waveformhelper**, generates `WGMO` from `WGM`.  

- Interrupt logic:  
  - If `IFOCA = 1` **OR** `IFOCB = 1`, then `interrupted = 1`.  

- All of these circuits are implemented in the **main** module, which collectively form the timer.
