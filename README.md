<!--

[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/AlBFWSQg)
# a14g-final-submission

    * Team Number: 
    * Team Name: 
    * Team Members: 
    * Github Repository URL: 
    * Description of test hardware: (development boards, sensors, actuators, laptop + OS, etc) 

## 1. Video Presentation

## 2. Project Summary

## 3. Hardware & Software Requirements

## 4. Project Photos & Screenshots

## Codebase

- A link to your final embedded C firmware codebases
- A link to your Node-RED dashboard code
- Links to any other software required for the functionality of your device

# A14G Final Submission

/-->

## Team Details

- **Team Number:** A14G  
- **Team Name:** DreamCatcher  
- **Team Members:**  
  - Abhik Kumar  
  - Toma  
- **GitHub Repository URL:** [https://github.com/your-repo-url-here](https://github.com/your-repo-url-here)

## Description of Test Hardware

- **Development Board:** Atmel SAMD21 Xplained Pro  
- **Sensors:**
  - SHT4x (Temperature and Humidity over I2C)
  - STEMMA Soil Sensor (Capacitive Moisture and Temperature via I2C)
  - SGP40 (VOC Sensor over I2C)
  - Photoresistor (Analog ADC on PB03)
  - PIR Motion Sensor (GPIO interrupt on PB02)
  - NPK Sensor (UART communication on SERCOM5)
- **Actuators:**
  - Fan (GPIO)
  - Buzzer (PWM via TCC2 on PA17)
  - Water Pump (GPIO based on STEMMA Soil Sensor)
  - Motor (PWM via TCC0 on PA06)
- **Other:**
  - Serial terminal interface over USB for debug
  - FreeRTOS-based multi-tasking architecture

---

## 1. Video Presentation

- Link: [https://youtu.be/example-link](https://youtu.be/example-link)

---

## 2. Project Summary

DreamCatcher is an environmental monitoring and response system built using FreeRTOS and a SAMD21 microcontroller. It senses humidity, temperature, light levels, soil moisture, air quality, and detects motion to trigger appropriate actuation responses like fan control, buzzer alarms, pump watering, and motor activation. The system includes UART-based NPK soil nutrient sensing, and is organized into well-isolated drivers with non-blocking asynchronous patterns for sensor polling. Sensor values are pushed to a queue for central processing.

Key Features:
- Asynchronous I2C, UART, and ADC integration
- Interrupt-based motion detection
- Modular peripheral drivers (buzzer, fan, motor, pump)
- Intelligent threshold-based actuation logic
- Stack watermarks printed for task memory debugging

---

## 3. Hardware & Software Requirements

### Hardware:
- SAMD21 Xplained Pro board
- SHT4x sensor
- SGP40 VOC sensor
- STEMMA Soil Sensor
- PIR Motion Sensor
- Photoresistor
- NPK UART sensor
- Buzzer (PA17)
- Fan (PA11)
- Pump (PA02)
- Motor (PA06)
- USB cable
- Windows/Linux laptop

### Software:
- Atmel Studio 7 / Microchip Studio
- ASF (Atmel Software Framework)
- FreeRTOS
- Serial terminal (PuTTY / Tera Term)
- Node-RED (optional for dashboard)

---

## 4. Project Photos & Screenshots

### Node-RED Dashboard Screenshot:
![Node-RED Dashboard](screenshots/nodered.png)

### Circuit Setup:
![Hardware Setup](screenshots/hardware.jpg)

---

## Codebase

- **Embedded C firmware:** [https://github.com/your-repo-url-here/firmware](https://github.com/your-repo-url-here/firmware)
- **Node-RED Flow:** [https://github.com/your-repo-url-here/nodered](https://github.com/your-repo-url-here/nodered)
- **Additional Tools:** 
  - Custom queue manager for data handling
  - UART timeout-based reading logic for NPK
  - PWM duty-cycle tuning routines for motor, fan, and pump

---

## Task Breakdown

| Task                    | Description                                       |
|-------------------------|---------------------------------------------------|
| I2C Task                | SHT4x, Soil Sensor, SGP40 polling                 |
| ADC Task                | Photoresistor peak sampling                       |
| UART Task               | NPK sensor polling with timeout protection       |
| Motion Handler Task     | Interrupt-based motion activation + actuation    |
| Schedule Task           | Aggregates all sensors and manages pump logic    |

---

## Notes

- Buzzer is driven using TCC2 on PA17
- Pump uses TCC1 on PA02 (WO[0])
- Fan uses TCC0 on PA11 (WO[3])
- Non-blocking UART and I2C communication used wherever possible
- All sensor values are debug-printed to serial terminal
