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

MQ135 → GPIO 34 (Analog)
MQ9 → GPIO 35 (Analog)
PMS5003 → RX: GPIO 16, TX: GPIO 17
DHT22 → GPIO 26 (Digital)

## 💻 Software Requirements

### Development Environment

- **Arduino IDE** or **PlatformIO**
- **ESP32 Board Support**: `https://dl.espressif.com/dl/package_esp32_index.json`

### Required Libraries

git clone https://github.com/your-username/esp32-air-quality-monitor.git
cd esp32-air-quality-monitor

### 2. Arduino IDE Configuration

- Install Arduino IDE
- Add ESP32 board support via **File → Preferences → Additional Boards Manager URLs**
- Install **esp32 by Espressif Systems** in Boards Manager
- Install required libraries via **Sketch → Include Library → Manage Libraries**

### 3. Firebase Setup

1. Create Firebase project at [Firebase Console](https://console.firebase.google.com)
2. Enable Realtime Database
3. Copy credentials and update code:

#define FIREBASE_HOST "your-project-id.firebaseio.com"
#define FIREBASE_AUTH "your-database-secret"

### 4. WiFi Configuration

Update network credentials:
const char* ssid = "your-wifi-ssid";
const char* password = "your-wifi-password";

### 5. Upload Code

- Open `main.ino` in Arduino IDE
- Select **ESP32 Dev Module** and appropriate port
- Upload via **Sketch → Upload**

## 🔬 Sensor Calibration

### MQ135 (CO₂) & MQ9 (CO/CH₄) Calibration

**Current Calibration Values:**

- `RZERO135 = 64877.9` (for ~400 ppm CO₂)
- `RZERO9 = 13156.9` (for ~0.5 ppm CO, ~1.8 ppm CH₄)

**Calibration Process:**

1. **Clean Air Exposure**: Place sensors in well-ventilated area
2. **Rs Value Collection**: Monitor serial output for Rs readings
3. **RZERO Calculation**:
   - **MQ135**: `RZERO135 = Rs / (pow(400 / (11.48 * 0.02242), -1/2.769034857))`
   - **MQ9 (CO)**: `RZERO9 = Rs / (pow(0.5 / 0.114, -1/1.2))`
   - **MQ9 (CH₄)**: `RZERO9 = Rs / (pow(1.8 / 0.076, -1/1.5))`
4. **Code Update**: Modify `#define RZERO135` and `#define RZERO9` values
5. **Verification**: Test in target environment and adjust if needed

> **Note**: PMS5003 is factory-calibrated and requires no adjustment

## 📊 Air Quality Index (AQI) Calculation

Based on **U.S. EPA Standards** using linear interpolation:

| Pollutant | Range     | Breakpoints                             |
| --------- | --------- | --------------------------------------- |
| **PM2.5** | 0-500 AQI | 12, 35.4, 55.4, 150.4, 250.4, 500 µg/m³ |
| **PM10**  | 0-500 AQI | 54, 154, 254, 354, 424, 604 µg/m³       |
| **CO**    | 0-500 AQI | 4.4, 9.4, 12.4, 15.4, 30.4, 50.4 ppm    |

**Overall AQI**: Highest sub-index among measured pollutants

## 🖥️ Usage

### 1. System Startup

- Power ESP32 via USB/external supply
- Monitor serial output at **115200 baud** for initialization status

### 2. Serial Monitor

View real-time data including:

- Sensor readings (CO₂, CO, CH₄, PM values, temperature, humidity)
- Calculated AQI values
- Alert notifications for hazardous conditions

### 3. Web Interface

- Connect device to same WiFi network as ESP32
- Navigate to ESP32 IP address (shown in serial monitor)
- Access live dashboard with auto-refresh capability
- Manual refresh available via web button

### 4. Firebase Dashboard

- Access Firebase Realtime Database
- View timestamped data under `/data/AirQualityMonitor2/`
- Latest readings available at `/latest/AirQualityMonitor2`

## ⚠️ Alert Thresholds

System triggers warnings for:

- **CO**: >2 ppm
- **CH₄**: >2.5 ppm
- **PM2.5**: >12 µg/m³

## 🤝 Contributing

We welcome contributions! Please follow these steps:

1. **Fork** the repository
2. **Create** feature branch (`git checkout -b feature/amazing-feature`)
3. **Commit** changes (`git commit -m 'Add amazing feature'`)
4. **Push** to branch (`git push origin feature/amazing-feature`)
5. **Open** Pull Request

### Contribution Guidelines

- Include detailed description of changes
- Provide calibration/test data when applicable
- Document any new features or modifications
- Follow existing code style and structure

## 📈 Future Enhancements

- [ ] NDIR CO₂ sensor integration (MH-Z19) for improved accuracy
- [ ] O₃ and NO₂ sensor support
- [ ] Mobile app development
- [ ] Machine learning-based air quality predictions
- [ ] Multi-device network support
- [ ] Historical data visualization

## ⚡ Technical Specifications

- **Update Frequency**: 60-second Firebase uploads, 5-second web refresh
- **Timezone**: IST (UTC+5:30)
- **Communication**: WiFi 802.11 b/g/n
- **Power Requirements**: 5V DC supply
- **Operating Temperature**: -10°C to +50°C
- **Data Format**: JSON via Firebase REST API

**Built for healthier indoor environments** 🌱
