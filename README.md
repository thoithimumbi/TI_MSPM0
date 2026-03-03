# MSPM0-Based USB Development Board with Integrated Motion Sensing

## Project Overview

This project is a custom-designed embedded development board built around the Texas Instruments MSPM0G3507 ARM Cortex-M0+ microcontroller. The objective was to design a complete, USB-powered embedded platform from schematic level, focusing on power integrity, clock stability, communication interfaces, and debug accessibility.

The board integrates a USB-C power interface, on-board 3.3V regulation, USB-to-UART communication, SWD programming interface, external crystal oscillator, and an I2C-based accelerometer for motion sensing applications.

This project demonstrates full embedded hardware design workflow: system architecture, schematic capture, peripheral integration, and production-aware design practices.

## Preview

![Schematic](TI%20MSPM0.jpeg)
<p align="center">
  <img src="TI MSPM0.png" alt="3D Image" width="400"/>
</p>

## System Architecture

The system is divided into the following functional blocks:

- USB-C Power Input  
- 3.3V Low-Dropout Regulation  
- MSPM0 Microcontroller Core  
- USB–UART Communication Bridge  
- External High-Frequency Crystal Oscillator  
- SWD Debug Interface  
- I2C Accelerometer Sensor Subsystem  

Each subsystem was designed with proper decoupling, signal routing consideration, and modular separation to ensure clean integration.


## Power Architecture

The board is powered via USB-C (5V VBUS). Power is regulated to 3.3V using an SPX3819 LDO regulator.

**Design considerations:**

- Input and output bulk + high-frequency decoupling capacitors  
- Stable 3.3V rail for MCU and sensor operation  
- Clean ground reference  
- USB device-mode CC configuration resistors  

The LDO-based design prioritizes low noise and simplicity over switching efficiency, suitable for low-power embedded applications.

## Microcontroller Subsystem

At the core of the design is the MSPM0G3507 microcontroller featuring:

- ARM Cortex-M0+ core  
- UART interface for serial communication  
- I2C peripheral for sensor communication  
- SWD interface for programming and debugging  
- External crystal support for accurate timing  

**Design considerations:**

- Local decoupling capacitors close to VDD pins  
- Dedicated reset pull-up and filtering capacitor  
- Proper VREF decoupling  
- Clean oscillator load matching capacitors  

This reflects production-grade MCU integration practices.

## Communication Interfaces

### USB–UART Interface

A CH340 USB-to-Serial converter provides:

- Virtual COM port over USB  
- Direct firmware logging and debugging  
- Simplified development workflow  

### I2C Sensor Interface

An onboard accelerometer is connected via I2C with:

- External pull-up resistors  
- Interrupt lines routed to the MCU  
- Local decoupling capacitor  

This enables motion-based embedded applications and sensor fusion experimentation.

## Debug & Programming Interface

A dedicated SWD header provides:

- SWDIO  
- SWCLK  
- NRST  
- 3.3V reference  
- Ground  

This ensures professional debugging capability using external debuggers.
