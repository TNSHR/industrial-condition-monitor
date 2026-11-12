# Industrial Condition Monitoring System

An industrial IoT monitoring system built with an STM32F407 sensor node (FreeRTOS),
an ESP32 MQTT gateway, a Node.js/TypeScript backend and a React dashboard.

**Status:** In progress (Day 1 of 84)

## Architecture
(Diagram coming in Week 7)

## Hardware
- STM32F407G-DISC1
- ESP32 DevKit V1
- SHT31 temperature/humidity sensor
- RS485 modules (Modbus RTU)

## Repository structure
- firmware/  : STM32 code (CubeIDE, HAL, FreeRTOS)
- gateway/   : ESP32 UART-to-MQTT bridge
- backend/   : Node.js + TypeScript API, MongoDB
- dashboard/ : React live dashboard
- docs/      : diagrams, captures, notes

## Progress log
- Day 1: repo created
- Day 1: repo created, STM32CubeIDE set up, LED blink on PD12 working
