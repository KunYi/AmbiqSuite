# Apollo 3 Blue Study with SparkFun Edge Board

This repository contains the AmbiqSuite SDK R2.5.1 integrated with SparkFun BSPs, specifically for use with the SparkFun Edge board in Apollo 3 Blue studies.

## Overview

This project combines the [AmbiqSuite SDK Rel2.5.1](https://ambiq.com/wp-content/uploads/2020/09/AmbiqSuite-R2.5.1.zip) with [SparkFun BSPs](https://github.com/sparkfun/SparkFun_Apollo3_AmbiqSuite_BSPs) to provide a comprehensive development environment for the Apollo 3 Blue microcontroller using the SparkFun Edge board.

## Prerequisites

Before you begin, ensure you have the following installed:

- arm-none-eabi-gcc toolchain (recommended version: [8-2018-q4-major](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads#panel2a) or lower)
- make
- python3 (required for bootloading)

## Installation and Usage

1. Clone the repository with submodules:
   ```bash
   git clone https://github.com/KunYi/AmbiqSuite.git amsdk --recurse-submodules
   cd amsdk
   ```

2. Build examples:
   ```bash
   BOARD=edge
   EXAMPLE=hello_world_uart
   cd boards_sfe/common/examples/$EXAMPLE/gcc
   make BOARD=$BOARD
   ```

   Note: You can replace `edge` with other board options like `artemis_thing_plus`, `artemis_redboard_nano`, or `artemis_redboard_atp`. Similarly, you can choose different examples applicable to your board.

3. Common make commands:
   ```bash
   make BOARD=$BOARD clean
   make BOARD=$BOARD bootload     # eqivalent to bootload_svl
   make BOARD=$BOARD bootload_svl # builds and bootloads with SparkFun Variable Loader - you must have this bootloader flashed onto your board
   make BOARD=$BOARD bootload_asb # builds and bootloads with Ambiq Secure Bootloader - should work with all boards. If not try changing the baud rate or manually setting the board into bootload mode
   ```

4. Output of hello_world_uart
   ```log
   Hello World!

   Vendor Name: AMBQ
   Device type: Apollo3 Blue
   Qualified: No
   Device Info:
           Part number: 0x06672198
           Chip ID0:    0xCA250251
           Chip ID1:    0x5C91C3C1
           Revision:    0x000ECF21 (RevB0)
           Flash size:  1048576 (1024 KB)
           SRAM size:    393216 (384 KB)

   App Compiler:    GCC 10.3.1 20210621 (release)
   HAL Compiler:    GCC 10.3.1 20210621 (release)
   HAL SDK version: 2.5.0
   HAL compiled with CMSIS-style registers
   SBL ver: 0x5 - 0x99a0, INFO0 valid, ver 0x0
   ```

## Advanced Usage

### Make Line Options

You can customize your build process using the following options:

| Option | Default Value | Description |
|--------|---------------|-------------|
| `BOARD` | | Short syntax to select board BSPs |
| `BOARDPATH` | | Path to the board directory containing BSP files |
| `COM_PORT` | COM4 | USB serial port for bootloading |
| `PYTHON3` | python3 | Command to invoke Python 3.x |
| `ASB_UPLOAD_BAUD` | 115200 | Baud rate for Ambiq Secure Bootloader |
| `SVL_UPLOAD_BAUD` | 921600 | Baud rate for SparkFun Variable Loader |
| `SDKPATH` | ../../../../.. | Path to AmbiqSuiteSDK root |
| `COMMONPATH` | ../../../../common | Path to common directory |
| `PROJECTPATH` | .. | Path to project directory |

Example usage:
```bash
make BOARD=edge COM_PORT=/dev/ttyUSB0 ASB_UPLOAD_BAUD=921600 bootload_asb
```

## References

- [Using SparkFun Edge Board with Ambiq Apollo3 SDK](https://learn.sparkfun.com/tutorials/using-sparkfun-edge-board-with-ambiq-apollo3-sdk)
- [SparkFun Apollo3 AmbiqSuite BSPs](https://github.com/sparkfun/SparkFun_Apollo3_AmbiqSuite_BSPs)
