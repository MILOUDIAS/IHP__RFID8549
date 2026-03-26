# System Specifications

## 1\. System Requirements

| Requirement    | Description         |
| -------------- | ------------------- |
| Operating mode | Passive LF RFID tag |
| Protocol       | FDX                 |
| Frame length   | 128 bits            |
| Clock source   | Extracted from AFE  |
| Encoding       | Bi-phase encoding   |
| Test interface | SPI DFT supported   |

## 2\. Functional Requirements

| Requirement       | Description                                                   |
| ----------------- | ----------------------------------------                      |
| Startup condition | Core starts only when `power_stable = 1` and `reset released` |
| Data source       | Frame stored in internal ROM                                  |
| Transmission      | Serialized bitstream output                                   |
| Output signal     | `modulated_bit`                                               |
| Test mode         | SPI-based testing supported                                   |

## 3\. Interface Requirements

| Signal        | Requirement                                  |
| ------------- | --------------------------------------       |
| clk_AFE       | Must be supported as functional clock        |
| reset_n_AFE   | Must be supported as reset source            |
| power_stable  | Must control system startup                  |
| SPI interface | Must follow protocol `Mode 0 (CPOL=0, CPHA=0)` |
