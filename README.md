# Low-Power MSPM0 Sensor Node with USB-C Connectivity

## 📌 System Overview
The board is powered via a USB-C connector, providing a primary 5V rail which is regulated to 3.3V for the MCU and onboard peripherals.

The system integrates:
- A high-performance ARM Cortex-M0+ microcontroller  
- A USB-to-UART bridge for direct serial communication  
- A 3-axis accelerometer for motion sensing applications  

---

## 🧩 Functional Blocks

### 🔌 Power Management
- **Input:** +5V from USB VBUS  
- **Regulation:** SPX3819M5-L-3-3 LDO → 3.3V rail  
- **Filtering:**
  - 10 µF (bulk)
  - 470 nF (high-frequency bypass)

Decoupling capacitors are placed on both input and output stages to reduce noise and ensure rail stability.

---

### 🧠 Microcontroller (TI MSPM0G3507)
The MSPM0G3507PTR (LQFP-48) serves as the central processing unit.

**Key configurations:**
- **Clocking:**  
  External 8 MHz crystal (X1) with 15 pF load capacitors for precise timing  

- **Programming & Debugging:**  
  TC2030 SWD header (SWDIO / SWCLK) for firmware flashing and real-time debugging  

- **Reset Circuit:**  
  - 5.1 kΩ pull-up resistor  
  - 470 nF capacitor for noise filtering  
  Ensures stable and reliable startup behavior  

---

### 🔄 USB-to-UART Interface
- **IC:** CH340E USB-to-serial converter  
- **Function:** Bridges USB differential pair (D+ / D−) to MCU UART  

**Connections:**
- PA0 → TX  
- PA1 → RX  

**Protection:**
- USBLC6-2SC6 ESD diode array on USB lines  
- Safeguards against electrostatic discharge and hot-plug transients  

---

### 📡 Sensors & Peripherals

#### LIS2DH Accelerometer
A low-power, high-resolution 3-axis accelerometer integrated on the 3.3V domain.

- **Interface:** I2C  
  - SDA → PA10  
  - SCL → PA11  
  - Pull-ups: 5.1 kΩ  

- **Interrupts:**
  - INT1 → PB8  
  - INT2 → PB9  

Supports interrupt-driven operation, enabling:
- Motion-triggered events  
- Low-power sleep modes with wake-on-interrupt  

---

## ⚙️ Technical Specifications

| Component        | Description                                  |
|------------------|----------------------------------------------|
| MCU              | TI MSPM0G3507 (ARM Cortex-M0+, up to 80 MHz) |
| USB Connector    | USB-C (USB 2.0 Full Speed)                   |
| Interface IC     | CH340E USB-to-UART                           |
| Voltage Rails    | 5V (USB), 3.3V (LDO Output)                  |
| Accelerometer    | LIS2DH (3-axis)                              |
| I2C Address      | Configurable via hardware                    |
| PCB Features     | 4× M3 mounting holes, 3× fiducials           |

---

## 🔗 Connectivity Table (Key Signals)

| Function  | MCU Pin | Peripheral     |
|----------|--------|----------------|
| UART TX  | PA0    | CH340E RXD     |
| UART RX  | PA1    | CH340E TXD     |
| I2C SDA  | PA10   | LIS2DH SDA     |
| I2C SCL  | PA11   | LIS2DH SCL     |
| SWDIO    | PA19   | TC2030 (Pin 2) |
| SWCLK    | PA20   | TC2030 (Pin 4) |

---

## 🚀 Design Notes
- External crystal ensures accurate UART baud rates and I2C timing  
- Interrupt-driven accelerometer minimizes power consumption  
- USB ESD protection improves reliability in real-world usage  
- Tag-Connect header reduces footprint while maintaining debug access  

---

## 📷 Media
![Schematic](TI%20MSPM0.jpeg)
<p align="center">
  <img src="TI MSPM0.png" alt="3D Image" width="400"/>
</p>
