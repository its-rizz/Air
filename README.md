# ESP32 Air Quality Monitoring System

A comprehensive IoT-based air quality monitoring solution built on ESP32 that measures indoor air quality parameters and provides real-time monitoring through web interface and Firebase integration.

## ✨ Features

- **Multi-sensor Integration**: Monitors CO₂, CO, CH₄, PM1.0, PM2.5, PM10, temperature, and humidity
- **Real-time AQI Calculation**: EPA standard-based Air Quality Index computation
- **Firebase Integration**: Automatic data logging to Firebase Realtime Database
- **Web Dashboard**: Live sensor readings accessible via ESP32-hosted web server
- **Smart Alerts**: Automatic warnings for hazardous air quality conditions
- **WiFi Connectivity**: Seamless internet connectivity for data synchronization
- **Timestamped Logging**: IST timezone support for accurate data tracking

## 🔧 Hardware Requirements

| Component          | Model           | Purpose                                      |
| ------------------ | --------------- | -------------------------------------------- |
| Microcontroller    | ESP32-WROOM-32  | Main processing unit                         |
| CO₂ Sensor         | MQ135           | Carbon dioxide monitoring (400-800 ppm)      |
| Gas Sensor         | MQ9             | CO (0-2 ppm) and CH₄ (1.8-2.5 ppm) detection |
| Particulate Sensor | PMS5003         | PM1.0, PM2.5, PM10 measurement               |
| Climate Sensor     | DHT22           | Temperature and humidity monitoring          |
| Resistor           | 10kΩ            | Sensor circuit support                       |
| Power Supply       | 5V USB/External | System power                                 |
| Connectivity       | WiFi Router     | Internet access for Firebase                 |

## 📌 Pin Configuration
