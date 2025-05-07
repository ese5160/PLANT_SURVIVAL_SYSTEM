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

- **Team Number:** T13  
- **Team Name:** DreamCatcher  
- **Team Members:**  
  - Abhik Kumar  
  - Toma Yasuda
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

Plant Survival System is an environmental monitoring and response system built using FreeRTOS and a SAMD21 microcontroller. It senses humidity, temperature, light levels, soil moisture, air quality, and detects motion to trigger appropriate actuation responses like fan control, buzzer alarms, pump watering, and motor activation (Puppet control). The system includes UART-based NPK soil nutrient sensing, and is organized into well-isolated drivers with non-blocking asynchronous patterns for sensor polling. Sensor values are pushed to a queue for central processing.

Key Features:
- Asynchronous I2C, UART, and ADC integration
- Interrupt-based motion detection
- Modular peripheral drivers (buzzer, fan, puppet, pump)
- Intelligent threshold-based actuation logic
- Stack watermarks printed for task memory debugging
- Node red based Frontend supports OTU

---

## 3. Hardware & Software Requirements


### Hardware Requirements Specification (HRS)

#### Overview
The IoT Plant Monitoring System was developed for real-time plant health monitoring and management using a combination of sensors and actuators. The system was powered by the SAMW25 microcontroller, which provided integrated Wi-Fi communication for data sharing and supported peripherals for environmental monitoring and actuation.

The hardware integrated soil moisture sensors, temperature and humidity sensors, a light sensor, motion sensor, air quality sensor, and a soil NPK sensor. Actuators such as a water pump and motion deterrent system ensured automated responses. The system also featured GPS for location tracking and a microSD card for efficient data logging.

#### Definitions and Abbreviations
- **SAMW25**: Microcontroller with integrated Wi-Fi
- **RTOS**: Real-Time Operating System
- **Li-ion**: Lithium-ion battery

#### Functional Requirements

- **HRS 01**: The SAMW25 microcontroller was used for processing, Wi-Fi communication, and interfacing with peripherals via I2C, SPI, UART, and GPIO.

- **HRS 02**: A capacitive soil moisture sensor measured soil water content (±3% accuracy) via I2C and triggered a water pump when moisture dropped below 30%.

- **HRS 03**: A DHT22 sensor measured temperature and humidity with ±0.5°C and ±2% accuracy. Watering increased by 10% for every 5°C rise above 26°C.

- **HRS 04**: A photodiode-based light sensor interfaced via ADC and detected lux levels (±2 lux). It helped disable sensors at night to save power.

- **HRS 05**: A soil NPK sensor (via RS485 + I2C) measured nitrogen, phosphorus, and potassium levels. A 12V boost converter powered it.

- **HRS 06**: A DC water pump (500 ml/min) was activated via GPIO based on soil moisture and adjusted for temperature and weather.

- **HRS 07**: A PIR motion sensor detected objects within 50 cm and triggered a buzzer via GPIO for 5 seconds.

- **HRS 08**: An optional GPS module (Neo-6M) logged location and fetched weather forecasts.

- **HRS 09**: The system ran on a 3.7V 2500mAh Li-ion battery with buck and boost converters for 3.3V, 5V, and 12V lines.

- **HRS 10**: A microSD card (via SPI) logged timestamped data including GPS coordinates and sensor readings.

- **HRS 11**: A PWM-controlled motor-driven puppet was activated on motion detection to deter animals.

- **HRS 12**: Power and Wi-Fi LEDs provided system status.

- **HRS 13**: RS485 interfaced with the NPK sensor and was powered by a 12V boost converter.

- **HRS 14**: An SGP40 sensor monitored VOC levels (0–1000 ppm) via I2C.

- **HRS 15**: A 5V wall adapter powered high-current devices like the pump and fan.

---

### Software Requirements Specification (SRS)

#### Overview
The system software managed real-time sensor data collection, automated actuation, and remote monitoring through Wi-Fi. It was developed using FreeRTOS and integrated cloud support.

#### Definitions and Abbreviations
- **Web Interface**: Platform for user interaction and control
- **Wi-Fi**: Wireless communication protocol
- **GPS**: Global Positioning System

#### Functional Requirements

- **SRS 01**: Sensor data was collected every 1 minute with ±1% sampling accuracy.

- **SRS 02**: Wi-Fi transmitted real-time soil moisture, temperature, humidity, and light data to the cloud.

- **SRS 03**: NPK levels were measured every minute. Alerts were generated if nutrient levels dropped below thresholds.

- **SRS 04**: The water pump activated below 30% soil moisture and turned off above 60%. GPS-based rain forecasts suppressed unnecessary watering.

- **SRS 05**: The PIR motion sensor activated a buzzer and puppet deterrent for 5 seconds upon motion. It was overrideable by button.

- **SRS 06**: GPS coordinates were logged for each plant and used to fetch forecast data.

- **SRS 07**: Notifications were sent via email to alert users about critical conditions like temperature extremes or low nutrients.

- **SRS 08**: Real-time and historical data were visualized through a web interface with graphs and system status.

- **SRS 09**: A microSD card logged timestamped data and used a rolling buffer to manage storage. Data synced with cloud when Wi-Fi was available.

- **SRS 10**: The fan remained on continuously to maintain airflow for stable sensor readings.

---

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
