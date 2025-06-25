# DAQ project

PiDAQ System - RP2040-based Data Acquisition System

PiDAQ is a lightweight data acquisition firmware written in C for the Raspberry Pi Pico (RP2040). It communicates with an external high-resolution ADC via SPI, renders signal waveforms on an SSD1306 OLED display via I2C, and transmits processed measurements to a PC using UART. GPIO buttons provide basic user interaction for system configuration.

## Features

- SPI communication with external ADC
- Real-time signal sampling and noise-cleaning
- Display of live waveform on SSD1306 OLED
- UART data transmission to a host computer
- Button-driven user interface for channel selection, timebase adjustment, and scaling

## System Overview

- MCU: Raspberry Pi Pico (RP2040)
- ADC: External SPI-based 
- Display: SSD1306 OLED over I2C
- Interface to PC: USB-UART
- Input controls: GPIO buttons

## Build Instructions

1. Install and initialize the Pico SDK:

```
git submodule update --init
```

2. Build the project:

```
mkdir build
cd build
cmake ..
make
```

3. Flash the resulting .uf2 file to the RP2040 using USB mass storage mode.

## External Libraries

- pico-sdk (mandatory)
- SSD1306 I2C driver (custom or community implementation)

## Core API Functions

### SPI-ADC Interface

- `adc_spi_init()`: Initializes the SPI peripheral for ADC communication
- `read_frame(uint8_t *frame)`: Reads a 32-bit data frame (8-bit status + 24-bit sample)

### I2C-Display Driver

- `ssd1306_init()`: Initializes the OLED display
- `draw_waveform(float voltage)`: Draws signal point based on voltage value

### UART-PC Communication

- `send_to_pc(float voltage)`: Sends formatted data string to PC via UART

### GPIO-Input Handler

- `gpio_callback(uint gpio, uint32_t events)`: Handles user button inputs

