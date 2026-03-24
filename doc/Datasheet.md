ANIMALS LF RFID Tag

Project: IHP_RFID8549

Overview

The "RFID8549" is a mixed-signal low-frequency (LF) passive RFID tag SoC designed for animal identification.
The system integrates:
                     * Analog Front-End (power extraction + clock generation)
                     * Digital baseband core
                     * Bi-phase encoder
                     * SPI Design-for-Test (DFT) interface

This document describes the current pre-silicon implementation and simulation characterization.

 Key Features
 
 * 128-bit FDX-B frame generation
 * Internal ROM-based ID storage
 * Bi-phase encoded output (modulated_bit)
 * Power-aware startup using power_stable
 * Dual clock operation (AFE clock / SPI test clock)
 * SPI DFT support (chip ID read, ROM test, scan control)
 * RTL and gate-level simulation verified

 Operating Frequency

| Parameter | Value |
| ----- | ----- |
| RFID operating band | Low Frequency (LF) |
| Carrier frequency | 134.2 kHz |
| Clock source | Extracted from RF field (AFE) |
| Verification clock | \~134.2 kHz (`clk_AFE`) |
| Bit timing | `BIT_PERIOD = 32` clock cycles |

Functional Description

1- Normal Operation
. The AFE extracts power from the RF field.  
. The AFE generates:`clk_AFE`,`reset_n_AFE` and `power_stable`. 
. The digital core reads the 128-bit frame from ROM.  
. The frame is serialized and bi-phase encoded.
. Output transmitted on `modulated_bit`.

2- DFT / Test Operation
SPI interface supports:
 . Chip-ID read
 . ROM test read
 . Scan shift / capture
 . Test reset control

 Frame Structure
 
 The tag generates a fixed 128-bit FDX-B frame stored in internal ROM
 . Header
 . Identification field (ID)
 . CRC-16
 . Trailer
 
Chip Pin-Out

| Pin Name | IO | Function |
| :---- | :---- | :---- |
| clk\_AFE | I | Clock extracted from the RF field (\~134.2 kHz). |
| reset\_n\_AFE | I | Active-low reset. |
| power\_stable| I | Supply stable indicator. |
| modulated\_bit | O | Bi-phase encoded output. |
| spi\_sck | I | SPI Clock for Test mode. |
| cs\_n | I | SPI Chip Select. |
| mosi | I | SPI Data Input. |
| miso\_o | O | SPI Data Output. |

Power Characteristics (Preliminary)

| Parameter | Value |
| ----- | ----- |
| Digital supply voltage | 1.2 V |
| Total extracted capacitance | \~5.99 pF |
| Mean dynamic current | \~106.7 nA |
| Peak dynamic current  | \~1.496 mA |

Note: Values are based on simulation (VCD \+ SPEF).

Verification Status

The design has been verified using:
* RTL simulation  
* Gate-level simulation (GLS)  
* Cocotb testbench  
* Formal assertions (RTL level)

Project Status

* RTL completed  
* Digital verification completed  
* Pre-silicon mixed-signal integration  
* Preliminary datasheet release

