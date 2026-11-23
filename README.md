# Industrial Condition Monitoring System

An industrial IoT monitoring system: an STM32F407 sensor node running FreeRTOS, an ESP32 MQTT gateway, a Node.js/TypeScript backend with MongoDB, and a React live dashboard. Built step by step over 12 weeks and documented in this repository.

**Status:** In progress. Firmware basics working (see the progress log).

## What it will do

An STM32 board reads vibration, temperature, humidity and an analog signal, packs the readings into CRC-protected frames and sends them over UART to an ESP32. The ESP32 publishes the data over MQTT. A Node.js backend stores it in MongoDB, checks alert thresholds and pushes live values to a React dashboard. Later stages add AWS IoT Core and a Modbus RTU interface for industrial use.

## Planned architecture

    Sensors -> STM32F407 (FreeRTOS) --UART--> ESP32 gateway --MQTT--> Broker
    Broker -> Node.js API + MongoDB -> WebSocket -> React dashboard
    STM32 --RS485/Modbus RTU--> PC (Modbus master)

A proper diagram will be added in docs/ in Week 7.

## Hardware

| Part | Purpose |
|---|---|
| STM32F407G-DISC1 | Main sensor node (built-in ST-LINK and accelerometer) |
| ESP32 DevKit V1 | Wi-Fi and MQTT gateway |
| SHT31 module | Temperature and humidity (I2C) |
| Potentiometer or current sensor | Analog input (ADC) |
| TTL-to-RS485 module and USB-RS485 adapter | Modbus RTU link |
| 24 MHz USB logic analyzer | Checking UART, SPI and I2C signals |

## Planned STM32 pin map

| Function | Pins |
|---|---|
| User LEDs (green, orange, red, blue) | PD12, PD13, PD14, PD15 |
| User button | PA0 (interrupt) |
| Accelerometer (SPI1) | PA5, PA6, PA7, chip select PE3 |
| SHT31 (I2C1) | PB6 (SCL), PB9 (SDA) |
| Analog input (ADC1) | PA1 |
| ESP32 link (USART2) | PA2 (TX), PA3 (RX) |
| Modbus RS485 (USART3) | PD8 (TX), PD9 (RX) |
| Debug printf (SWO) | PB3 |

These are plans and may change as the build progresses.

## Repository structure

- firmware/ : STM32 project (STM32CubeIDE, HAL, FreeRTOS)
- gateway/ : ESP32 UART-to-MQTT bridge
- backend/ : Node.js and TypeScript API, MongoDB
- dashboard/ : React live dashboard
- docs/ : notes, diagrams and logic analyzer captures

## Build and flash the firmware

1. Install STM32CubeIDE.
2. Open it, choose File > Open Projects from File System, and select firmware/condition-monitor-fw.
3. Connect the STM32F407G-DISC1 through the ST-LINK USB port.
4. Build with the hammer icon, then run or debug with the green buttons.
5. For printf output, start a debug session with SWV enabled (core clock 168 MHz) and open the SWV ITM Data Console.

## Progress log

- Day 1: repo created, STM32CubeIDE set up, LED blink working
- Day 2: LED chase pattern and user button reading working
- Day 3: button interrupt with debounce, printf over SWV working
- Day 4: LinkedIn profile updated
- Day 5: repo cleanup, README and notes added

## Author

Shrinath Sharma, Hyderabad, India. LinkedIn: linkedin.com/in/shrinath25
