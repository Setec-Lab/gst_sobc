# Master MCU - UART commands


## How to set up communication?
* Micro USB cable from **PC to MSP432 LaunchPad** (communication uses back-channel UART of LaunchPad)
* UART settings: 256.000 baud/s, 8n1
* send commands in Ascii, e.g. using [HTerm](http://www.der-hammer.info/pages/terminal.html), Send on enter: _Null_


## UART commands
* `type` or `Type` - Returns _"MSP432P401R LaunchPad on EPS prototype: FRDET with MPPT"_ (standard string that describes device + purpose).
* `bdc [on/off]` - **[default: OFF]** Switch **both** BDCs `on` or `off` _(master MCU sends SPI command to slaves)_.
* `bdc [-/+]` - Decrease (`-`) or increase (`+`) duty cycle of BDCs by one step _(master MCU sends SPI command to slaves)_.
* `bdc [min/max/act]` - Get minimum (`min`), maximum (`max`) or actual (`act`) duty cycle of BDCs _(master MCU sends SPI command to slaves)_.
* `ctrl` or `mppt` - Shows which control modules are active and inactive (MPPT or fixed voltage control).
* `ctrl timing` or `mppt timing` - **[default: OFF]** Enables/disables printing MPPT routine timing (clock cycles and duration) via UART.
* `ctrl int [x]` or `mppt int [x]` - Changes the control loop execution interval (CLEI) to `[x]` ms. Send `ctrl int` or `mppt int` (without `[x]`) to get the current value.
* `mppt [on/off]` - **[default: OFF]** Enable/disable maximum power point tracking (MPPT).
* `pvset [on/off]` - **[default: OFF]** Enable/disable fixed voltage set point for V_pva. Default, if enabled: 4.5 V.
* `pvset [x]` - **[default: OFF]** Set the voltage set point for V_pva to `[x]` mV and enable it. Send `pvset` to get current state and setpoint value.
* `lp [on/off]` - **[default: OFF]** Enable/disable low-pass filter that filters ADC measurement values before using them in the control loop. Send `lp` only to get the current state.
* `lp [x]` - Set filter constant _tau_ to `[x]` ms. Send `lp` to get the current value. Cut-off frequency is **f_c = 1/(2\*pi\*tau)**.
* `dc print` or `print dc` - **[default: OFF]** Enables/disables printing of duty cycle.
* `dc reset` or `reset dc` - Reset the duty cycle to DEFAULT value; only for simulation purposes, affects only simulated PVA.
* `bat sim [x]` - Set the simulated battery's voltage to [x] mV; only relevant for the simulation case _pv_sim()_ (simulated PVA).
* `sweep` - Run a sweep through solar cell voltage to determine I-V characteristics; only for simulation purposes, affects only simulated PVA (_pv_sim()_).
* `uart bd` - Returns current UART baudrate of master MCU.
* `uart bd [x]` - Sets UART baudrate to `[x]` baud/s.
* `spi [on/off]` - **[default: ON]** Enable (`on`) or disable (`off`) SPI communication from master MCU (MSP432) to slave MCUs (PIC16).
* `spi clk` - Returns current SPI clock frequency (communication between master and slave MCUs).
* `spi clk [x]` - Sets SPI clock frequency to `[x]` kHz.
* `cpu clk` - Returns current CPU freqency (master clock) of master MCU.
* `cpu clk [x]` - Set CPU clock to `[x]` kHz. Allowed values are: 1500, 3000, 6000, 12000, 24000 and 48000.
* `adc timing` - **[default: OFF]** Enables/disables printing ADC routine timing.
* `print adc` or `adc print` - **[default: OFF]** Enables/disables printing ADC measurement values in _slow_ interval.
* `print meas` or `meas print` - **[default: OFF]** Enables/disables printing physical measurement values (unfiltered) in _slow_ interval.
* `print input` or `input print` - **[default: OFF]** Enables/disables printing input signals (filtered or unfiltered input to control loop) in _slow_ interval.
* `plots` - **[default: OFF]** Enables/disables sending measurement values in format `$[data];` (**in fast interval**), so that they can be displayed with Serial Port Plotter. Useful for monitoring e.g. PVA voltage and current over time.
* `plots fast` - **[default: OFF]** Enables/disables sending measurement values in format `$[data];` (**in super-fast interval**), so that they can be displayed with Serial Port Plotter.
* `plots [pv/pv lp/bat2/bat2 lp]` - **[default: OFF]** Enables/disables sending ADC measurement values in format `$[data];`. `pv` - V,I,P of PV bus,
  `pv lp` - low-pass filtered V,I,P of PV bus, `bat2` - V,I of BAT2, `bat2 lp` - low-pass filtered V,I of BAT2.
* `noise` - **[default: OFF]** Enables/disables sending ADC measurement values (I_PVA in µA) in format `$[data];`, to determine the typical noise of a current measurement channel
* `print stddev` or `stddev print` - **[default: OFF]** Enables/disables printing standard deviation of I_PVA and V_PVA.
* `adc zero i` or `zero i` - **[default: OFF]** Enables/disables zero current voltage measurement. Takes about 5 min to get reasonable value (using software low-pass filtering).
            This command is used to measure the voltage that is output by the [ACS723-05AB](https://www.allegromicro.com/en/Products/Sense/Current-Sensor-ICs/Zero-To-Fifty-Amp-Integrated-Conductor-Sensor-ICs/ACS723)
            current sensors for **zero current**.
            When using this command, ensure that no load is connected to the PCB and no current is flowing anywhere.
            The outcome of this measurement can be used to adjust the 'calibration' in software through hard-coding the offset.
            Be aware that _I_PDU5V_ and _I_PDU3.3V_ are measured through [LTC3112](https://www.analog.com/media/en/technical-documentation/data-sheets/3112fd.pdf),
            so the zero current measurement does not apply here.
* `cpu load` - **[default: OFF]** Enables/disables printing an estimation of the CPU load periodically via UART. Handle with caution.  
   Actually, this command does not print the **cpu load** but the **period load**, i.e. which portion of the SAMPLING_INTERVAL (ADC sampling interval) is occupied by non-idle state (ADC routine, MPPT, ...).  
   The ADC causes the highest portion on the cpu load (~ 5ms for averaging 100 samples on 7 ADC channels, ADC clock 6 MHz, 14-bit resolution).

 
## So what are those UART commands good for?
* Set volatile configurations (the MCU awakes to default configuration after CPU reset)
* Query parameters from the MCU
* Activate and deactivate modules on the prototype PCB


## Who can I talk to?
* [Adrian Wenzel](mailto:a.wenzel@tum.de) 
* [Juan J. Rojas](mailto:juan.rojas@itcr.ac.cr)

 