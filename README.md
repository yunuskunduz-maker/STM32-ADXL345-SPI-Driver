# STM32 ADXL345 SPI Driver (HAL Library)

This repository contains a bare-metal SPI driver implementation for the **ADXL345 Accelerometer** using **STM32F103RB (Nucleo)** and the **STM32 HAL Library**.

Unlike many I2C implementations found online, this driver uses **SPI (4-Wire)** for faster and more robust communication.

## 🚀 Features
* **Protocol:** SPI Mode 3 (CPOL=High, CPHA=2Edge).
* **Speed:** Prescaler 256 (Safe speed for long wires/breadboards).
* **Functionality:**
    * Reads Device ID (Checks connection).
    * Configures Power Control (Wake Up).
    * Reads Raw X, Y, Z data continuously.

## 🔌 Hardware Connections (Pinout)

This project uses **SPI1** on the STM32F103RB.

| ADXL345 Pin | STM32 Nucleo Pin | STM32 MCU Pin | Function |
| :--- | :--- | :--- | :--- |
| **VCC** | 3.3V | - | Power |
| **GND** | GND | - | Ground |
| **CS** | **A2** | **PA4** | Chip Select (Software Controlled) |
| **SCL** | **D13** | **PA5** | SPI1 SCK |
| **SDO** | **D12** | **PA6** | SPI1 MISO |
| **SDA** | **D11** | **PA7** | SPI1 MOSI |

> **Note:** The `CS` pin is defined as `ADXL_CS` in CubeMX. You can change it to any GPIO Output pin.

## ⚠️ Critical Note on Hardware (Troubleshooting)
If you are receiving `0` or `255` values consistently, check the following:
1.  **Soldering:** Ensure the header pins on the ADXL345 module are **soldered**. Loose contact or just "touching" the pins will NOT work for SPI communication.
2.  **Wiring:** Ensure `CS`, `VCC`, and `GND` are connected.
3.  **Module Type:** Some ADXL345 modules have a voltage regulator (662K). If so, powering with 5V might be more stable.

## 🛠️ How to Use
1.  Open the project in **STM32CubeIDE**.
2.  Connect your Nucleo board.
3.  Build and Debug.
4.  Add `x_val`, `y_val`, `z_val`, and `dev_id` to **Live Expressions**.
5.  Run the code (Resume). You should see values changing as you move the sensor.
