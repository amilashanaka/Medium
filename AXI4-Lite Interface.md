# AXI4-Lite Interface

## Introduction to AXI4-Lite

## Introduction to AXI4-Lite (Advanced Extensible Interface)

Advanced eXtensible Interface 4 (AXI4) is a family of buses defined as part of the fourth generation of the ARM Advanced Microcontroler Bus Architectrue (AMBA) standard. AXI was first introduced with the third generation of AMBA, as AXI3, in 1996.

The AMBA specification defines 3 AXI4 protocols:

- AXI4: A high performance memory mapped data and address interface. Capable of Burst access to memory mapped devices.
- AXI4-Lite: A subset of AXI, lacking burst access capability. Has a simpler interface than the full AXI4 interface.
- AXI4-Stream: A fast unidirectional protocol for transfering data from master to slave.

### Use in Xilinx-Based designs

Xilinx Vivado helps in the creation of custom IP with AXI4 interfaces. These can be connected to the Zynq’s Proccessing System or to other devices. This Document will cover the operation of the AXI4-Lite interface, which is convenient for implementing memory mapped registers.



### AXI4-Lite Interface Signals

The AXI4-Lite interface consists of five channels: Read Address, Read Data, Write Address, Write Data, and Write Response. An AXI4 read transaction using the Read Address and Data channels is shown in figure 1. Similarly an AXI4 write transaction using the Write Address, Data, and Response channels is shown in figure 2. Note that these figures depict burst transfers, which AXI4-Lite is incapable of.

![Figure 1. AXI4 Read Transaction.](https://www.realdigital.org/img/cede9613613d73fe3cf53fde7c215b73.png)





![Figure 2. AXI4 Write Transaction.](https://www.realdigital.org/img/01b29efbcdc24d7feadbbb7c33cab5c5.png)





he following table provides a detailed explanation about each signals on AXI4-Lite Interface.

| **Global Signals** |     |                                  |
| ------------------ | --- | -------------------------------- |
| `ACLK`             | M→S | Clock source.                    |
| `ARESETN`          | M→S | Global reset source, active low. |

| **Read Address Channel** |           |                                                                                                                                                                 |
| ------------------------ | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Name                     | Direction | Descrption                                                                                                                                                      |
| `ARADDR`                 | M→S       | Read address, usually 32-bit wide.                                                                                                                              |
| `ARCACHE`                | M→S       | Memory type. Xilinx IP usually ignores this value if a slave. IP as a master generates transactions with Normal Non-cacheable Modifiable and Bufferable (0011). |
| `ARPROT`                 | M→S       | Protection type. Xilinx IP usually ignores as a slave. As a master IP generates transactions with Normal, Secure, and Data attributes (000).                    |
| `ARVALID`                | M→S       | Read address valid. Master generates this signal when Read Address and the control signals are valid.                                                           |
| `ARREADY`                | M←S       | Read address ready. Slave generates this signal when it can accept the read address and control signals.                                                        |



| **Read Data Channel** |           |                                                                                         |
| --------------------- | --------- | --------------------------------------------------------------------------------------- |
| Name                  | Direction | Descrption                                                                              |
| `RDATA`               | M←S       | Read Data (32-bit only).                                                                |
| `RRESP`               | M←S       | Read response. This signal indicates the status of data transfer.                       |
| `RVALID`              | M←S       | Read valid. Slave generates this signal when Read Data is valid                         |
| `RREADY`              | M→S       | Read ready. Master generates this signal when it can accept the Read Data and response. |

| **Write Address Channel** |           |                                                                                                                                      |
| ------------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Name                      | Direction | Descrption                                                                                                                           |
| `AWADDR`                  | M→S       | Write address, usually 32-bits wide.                                                                                                 |
| `AWCACHE`                 | M→S       | Memory type. Slave IP usually ignores and Master IP generates transactions as Normal Non-cacheable Modifiable and Bufferable (0011). |
| `AWPROT`                  | M→S       | Protection type. Slave IP usually ignores and Master IP generates transactions with Normal, Secure and Data attributes (000).        |
| `AWVALID`                 | M→S       | Write address valid. Master generates this signal when Write Address and control signals are valid                                   |
| `AWREADY`                 | M←S       | Write address ready. Slave generates this signal when it can accept Write Address and control signals                                |

| **Write Data Channel** |           |                                                                                                                         |
| ---------------------- | --------- | ----------------------------------------------------------------------------------------------------------------------- |
| Name                   | Direction | Descrption                                                                                                              |
| `WDATA`                | M→S       | Write data (32-bit only).                                                                                               |
| `WSTRB`                | M→S       | Write strobes. 4-bit signal indicating which of the 4-bytes of Write Data. Slaves can choose assume all bytes are valid |

| **Write Response Channel** |           |                                                                                                |
| -------------------------- | --------- | ---------------------------------------------------------------------------------------------- |
| Name                       | Direction | Descrption                                                                                     |
| `BRESP`                    | M←S       | Write response. This signal indicates the status of the write transaction.                     |
| `BVALID`                   | M←S       | Write response valid. Slave generates this signal when the write response on the bus is valid. |
| `BREADY`                   | M→S       | Response ready. Master generates this signal when it can accept a write response               |


