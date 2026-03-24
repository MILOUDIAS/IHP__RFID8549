ANIMALS LF RFID Tag

System Specifications

1\. System Requirements

| Requirement | Description |
| ----- | ----- |
| Operating mode | Passive LF RFID tag |
| Protocol | FDX |
| Frame length | 128 bits |
| Clock source | Extracted from AFE |
| Encoding | Bi-phase encoding |
| Test interface | SPI DFT supported |

2\. Functional Requirements

| Requirement | Description |
| ----- | ----- |
| Startup condition | Core starts only when `power_stable = 1` |
| Data source | Frame stored in internal ROM |
| Transmission | Serialized bitstream output |
| Output signal | `modulated_bit` |
| Test mode | SPI-based testing supported |

3\. Interface Requirements

| Signal | Requirement |
| ----- | ----- |
| clk\_AFE | Must be supported as functional clock |
| reset\_n\_AFE | Must be supported as reset source |
| power\_stable | Must control system startup |
| SPI interface | Must support chip-ID and test commands |

4\. Verification Requirements

| Requirement | Description |
| ----- | ----- |
| RTL simulation | Required |
| Gate-level simulation | Required |
| Functional testbench | Required |
| Power estimation | Required |
