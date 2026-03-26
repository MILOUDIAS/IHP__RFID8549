# Project: IHP_RFID8549

## Overview

The "RFID8549" is a mixed-signal low-frequency (LF) passive RFID tag SoC designed for animal identification.
The system integrates:
_Analog Front-End (power extraction + clock generation + Reset)
_ Digital baseband core
_Bi-phase encoder
_ SPI Design-for-Test (DFT) interface

This document describes the current pre-silicon implementation and simulation characterization.

## Key Features

- 128-bit FDX-B frame generation
- Internal ROM-based ID storage
- Bi-phase encoded output (modulated_bit)
- Power-aware startup using power_stable
- Dual clock operation (AFE clock / SPI test clock)
- SPI DFT support (chip ID read, ROM test, scan control)
- RTL and gate-level simulation verified

### Operating Frequency

| Parameter           | Value                          |
| ------------------- | ------------------------------ |
| RFID operating band | Low Frequency (LF)             |
| Carrier frequency   | 134.2 kHz                      |
| Clock source        | Extracted from RF field (AFE)  |
| Verification clock  | \~134.2 kHz (`clk_AFE`)        |
| Bit timing          | `BIT_PERIOD = 32` clock cycles |

## Functional Description

### 1- Normal Operation

. The AFE extracts power from the RF field.  
. The AFE generates:`clk_AFE`,`reset_n_AFE` and `power_stable`.
. The digital core reads the 128-bit frame from ROM.  
. The frame is serialized and bi-phase encoded.
. Output transmitted on `modulated_bit`.

### 2- DFT / Test Operation

#### SPI interface supports

. Chip-ID read
. ROM direct access/sweaep testing
. Scan chain testing (shift and capture)
. Test reset control

#### Frame Structure

The tag generates a fixed 128-bit FDX-B frame stored in internal ROM
. Header
. Identification field (ID)
. CRC-16
. Trailer

## Chip Pin-Out (Digital part)

| Pin Name      | IO  | Function                                         |
| :------------ | :-- | :----------------------------------------------- |
| clk_AFE       | I   | Clock extracted from the RF field (\~134.2 kHz). |
| reset_n_AFE   | I   | Active-low reset.                                |
| power_stable  | I   | Supply stable indicator.                         |
| modulated_bit | O   | Bi-phase encoded output.                         |
| spi_sck       | I   | SPI Clock for Test mode.                         |
| cs_n          | I   | SPI Chip Select.                                 |
| mosi          | I   | SPI Data Input.                                  |
| miso          | O   | SPI Data Output.                                 |

## Verification Status


- RTL simulation with cocotb + verilator 
- Gate-level simulation (GLS) with cocotb + iverilog
- Cocotb testbench (Functional + Coverage)
- Formal assertions (RTL level)

