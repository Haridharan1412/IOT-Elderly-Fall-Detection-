<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,11,20&height=200&section=header&text=Elderly%20Fall%20Detection%20System&fontSize=40&fontColor=ffffff&animation=twinkling&fontAlignY=38&desc=Real-Time%20IoT%20Safety%20Guardian%20Powered%20by%20ESP8266%20%2B%20Blynk&descAlignY=60&descSize=15" width="100%"/>

[![Typing SVG](https://readme-typing-svg.demolab.com?font=Fira+Code&size=22&duration=2500&pause=800&color=00D4FF&center=true&vCenter=true&multiline=true&width=800&height=80&lines=⚡+Detects+Falls+in+Real-Time;📡+Sends+Instant+Alerts+to+Caregivers)](https://git.io/typing-svg)

<br/>

<img src="https://user-images.githubusercontent.com/74038190/212284100-561aa473-3905-4a80-b561-0d28506553ee.gif" width="100%">

[![Arduino](https://img.shields.io/badge/Platform-ESP8266-blue?style=for-the-badge&logo=arduino&logoColor=white)](https://www.arduino.cc/)
[![Blynk](https://img.shields.io/badge/Cloud-Blynk%20IoT-00C853?style=for-the-badge)](https://blynk.io/)
[![Sensor](https://img.shields.io/badge/Sensor-MPU6050-FF6F00?style=for-the-badge&logo=adafruit&logoColor=white)](https://invensense.tdk.com/)

<br/>

</div>

---

## 📌 About The Project

<table>
<tr>
<td width="100%">

Falls are the **#1 cause of injury** among elderly adults — and delayed response makes outcomes far worse. This project tackles that with a compact, low-cost IoT device.

The **Elderly Fall Detection System** straps onto the elderly person and uses the **MPU6050 IMU sensor** to track 6-axis motion data 10 times per second. When a sudden fall-like jolt is detected via a hardware motion interrupt, it instantly sends the sensor readings to the **Blynk IoT cloud** and pushes a **real-time alert** to the caregiver's smartphone.

**No manual reporting. No delays. Just instant protection.**

### 🎯 Objectives
- Monitor real-time acceleration and angular velocity
- Detect abnormal motion patterns that indicate a fall
- Alert caregivers immediately via smartphone notifications
- Keep hardware simple, affordable, and wearable

</td>

<br/><br/>

</td>
</tr>
</table>

---

<img src="https://user-images.githubusercontent.com/74038190/212284100-561aa473-3905-4a80-b561-0d28506553ee.gif" width="100%">

## ✨ Features

<div align="center">

| Feature | Description |
|:---:|:---|
| ⚡ **Real-Time Detection** | MPU6050 hardware interrupt fires within milliseconds of a fall |
| 📡 **Blynk IoT Cloud** | Live sensor data streamed to cloud via Wi-Fi every 100ms |
| 🔔 **Push Notifications** | Instant alert delivered to caregiver's phone via Blynk app |
| 📊 **Live Dashboard** | 5 sensor channels visualized live on the Blynk mobile dashboard |
| 🧠 **Smart Filtering** | 0.63 Hz high-pass filter removes gravity drift; only real motion triggers |
| 🔋 **Interrupt-Driven** | Hardware interrupt architecture — no wasted CPU cycles during inactivity |
| 🔧 **Configurable** | Adjustable motion threshold (default: `1`) and duration (default: `20ms`) |
| 📶 **Auto Reconnect** | Robust Wi-Fi + Blynk reconnection with serial diagnostics |

</div>

---

<img src="https://user-images.githubusercontent.com/74038190/212284100-561aa473-3905-4a80-b561-0d28506553ee.gif" width="100%">

## 🏗️ System Architecture

```mermaid
graph TD
    A([👴 Elderly Person\nWears Device]) -->|Motion| B

    subgraph HW ["🔧 Hardware"]
        B[MPU6050 IMU\nAccelerometer + Gyroscope]
        B -->|I2C SDA/SCL| C[ESP8266 NodeMCU\nMicrocontroller + Wi-Fi]
    end

    subgraph LOGIC ["⚙️ Detection Logic"]
        C -->|100ms Timer Poll| D{Motion\nInterrupt?}
        D -->|No| D
        D -->|Yes ⚠️| E[Read 5 Sensor Axes\nAccelY/Z · GyroX/Y/Z]
    end

    subgraph CLOUD ["☁️ Blynk IoT Cloud"]
        E -->|Wi-Fi TCP| F[Blynk Server]
        F --> G[Virtual Pins V1–V5\nLive Data]
        F --> H[Event Logger\nREST API]
    end

    G --> I([📱 Caregiver App\nLive Dashboard])
    H --> J([🔔 Push Notification\nInstant Alert])

    style HW fill:#1a1a2e,stroke:#00d4ff,color:#fff
    style LOGIC fill:#16213e,stroke:#00d4ff,color:#fff
    style CLOUD fill:#0f3460,stroke:#00d4ff,color:#fff
```

---

<img src="https://user-images.githubusercontent.com/74038190/212284100-561aa473-3905-4a80-b561-0d28506553ee.gif" width="100%">

## 🔧 Hardware Components

<div align="center">

<img src="https://media.giphy.com/media/l3fQjHugtGPGKQ8tO/giphy.gif" width="100%" height="4"/>

</div>

| # | Component | Purpose | Qty |
|:---:|:---|:---|:---:|
| 1 | **ESP8266 NodeMCU v1.0** | Main processor + Wi-Fi module | 1 |
| 2 | **MPU6050 GY-521** | 3-axis Accelerometer + 3-axis Gyroscope | 1 |
| 3 | **Breadboard** | Prototyping base | 1 |
| 4 | **Jumper Wires (M-M)** | GPIO connections | ~10 |
| 5 | **USB Micro-A Cable** | Programming & power supply | 1 |
| 6 | **5V Power Bank** | Portable power for wearable use | 1 |

<div align="center">

</div>

---

<img src="https://user-images.githubusercontent.com/74038190/212284100-561aa473-3905-4a80-b561-0d28506553ee.gif" width="100%">

## 🔌 Circuit Connections

```
ESP8266 NodeMCU              MPU6050 (GY-521)
┌─────────────────┐          ┌──────────────────┐
│   3.3V  ────────┼──────────┼── VCC            │
│   GND   ────────┼──────────┼── GND            │
│ D2/GPIO4 ───────┼──────────┼── SDA  (I2C Data)│
│ D1/GPIO5 ───────┼──────────┼── SCL  (I2C CLK) │
│                 │          │   AD0 ─── GND    │
└─────────────────┘          └──────────────────┘
```

| MPU6050 Pin | ESP8266 Pin | Notes |
|:---:|:---:|:---|
| VCC | 3.3V | ⚠️ Do NOT use 5V — will damage sensor |
| GND | GND | Common ground |
| SDA | D2 (GPIO4) | I2C Data line |
| SCL | D1 (GPIO5) | I2C Clock line |
| AD0 | GND | Sets I2C address to `0x68` |

---

<img src="https://user-images.githubusercontent.com/74038190/212284100-561aa473-3905-4a80-b561-0d28506553ee.gif" width="100%">

## 💻 Software & Libraries

**IDE:** Arduino IDE 2.x + ESP8266 Board Package

| Library | Purpose | Install Via |
|:---|:---|:---|
| `ESP8266WiFi.h` | Wi-Fi stack for NodeMCU | Board package (built-in) |
| `BlynkSimpleEsp8266.h` | Blynk cloud integration | Library Manager → *Blynk* |
| `Adafruit_MPU6050.h` | MPU6050 IMU sensor driver | Library Manager → *Adafruit MPU6050* |
| `Adafruit_Sensor.h` | Unified sensor abstraction | Library Manager → *Adafruit Unified Sensor* |
| `Wire.h` | I2C communication | Built-in |

---

<img src="https://user-images.githubusercontent.com/74038190/212284100-561aa473-3905-4a80-b561-0d28506553ee.gif" width="100%">

## ⚙️ How It Works

<div align="center">
<img src="https://media.giphy.com/media/xT9IgzoKnwFNmISR8I/giphy.gif" width="100%" height="3"/>
</div>

### Step-by-Step Operation

**1. Boot & Connect**
ESP8266 connects to Wi-Fi (`Amit1`) and initializes MPU6050 over I2C. Serial monitor confirms both connections at 115200 baud.

**2. Motion Detection Setup**
MPU6050 is configured with:
- 🔹 High-pass filter: `0.63 Hz` — removes gravity drift, captures only sudden movements
- 🔹 Threshold: `1` — sensitivity level for motion detection
- 🔹 Duration: `20 ms` — motion must last 20ms (eliminates vibration noise)
- 🔹 Latch mode: `true` — interrupt stays active until explicitly cleared

**3. Timer-Based Polling**
`BlynkTimer` triggers `sendSensor()` every **100ms** — non-blocking, so Blynk stays connected.

**4. Fall Detection**
Inside `sendSensor()`, the MPU6050's interrupt flag is checked. If raised:
- All 5 axes are read: `AccelY`, `AccelZ`, `GyroX`, `GyroY`, `GyroZ`
- Data is logged to Serial Monitor
- Values pushed to Blynk virtual pins **V1–V5**

**5. Cloud Alert**
Blynk receives the data spike and notifies the caregiver's app instantly.

### Virtual Pin Mapping

| Virtual Pin | Sensor Value | Unit | What It Tells Us |
|:---:|:---:|:---:|:---|
| V1 | AccelY | m/s² | Forward/backward tilt |
| V2 | AccelZ | m/s² | Vertical impact (key fall indicator) |
| V3 | GyroX | rad/s | Roll rate |
| V4 | GyroY | rad/s | Pitch rate |
| V5 | GyroZ | rad/s | Yaw rate |

---

## 🔄 Project Workflow

```mermaid
flowchart TD
    A([🟢 Power ON]) --> B[Init Serial 115200 baud]
    B --> C[Connect Wi-Fi]
    C --> D{Connected?}
    D -->|Retrying...| C
    D -->|✅ Yes| E[Init MPU6050 via I2C]
    E --> F{Sensor Found?}
    F -->|❌ No| G([🔴 Halt: Sensor Error])
    F -->|✅ Yes| H[Configure Motion Interrupt\nThreshold=1 · Duration=20ms\nHPF=0.63Hz]
    H --> I[Connect to Blynk Cloud]
    I --> J[Set Timer: 100ms interval]
    J --> K{⏱️ Timer Fires?}
    K --> L{Motion Interrupt\nDetected?}
    L -->|No| K
    L -->|⚠️ Yes - FALL!| M[Read AccelY/Z · GyroX/Y/Z]
    M --> N[Print to Serial Monitor]
    N --> O[Write to Blynk V1–V5]
    O --> P[☁️ Blynk Cloud Processes]
    P --> Q([🔔 Push Notification\nto Caregiver Phone])
    Q --> K

    style A fill:#00C853,color:#fff,stroke:#00C853
    style G fill:#D32F2F,color:#fff,stroke:#D32F2F
    style Q fill:#FF6F00,color:#fff,stroke:#FF6F00
    style P fill:#1565C0,color:#fff,stroke:#1565C0
```

---

## 🚀 Setup Guide

**1. Install ESP8266 board in Arduino IDE**
> File → Preferences → Additional Board URLs:
```
https://dl.espressif.com/dl/package_esp32_index.json
```
Then: Tools → Board Manager → search `ESP8266` → Install

**2. Install required libraries** via Tools → Manage Libraries:
```
Blynk · Adafruit MPU6050 · Adafruit Unified Sensor
```

**3. Create a Blynk Template** at [blynk.cloud](https://blynk.cloud)
- Add 5 datastreams: V1–V5 (type: Double)
- Copy your Template ID, Template Name, and Auth Token

**4. Update credentials in the `.ino` file:**
```cpp
#define BLYNK_TEMPLATE_ID   "YOUR_TEMPLATE_ID"
#define BLYNK_TEMPLATE_NAME "YOUR_TEMPLATE_NAME"
#define BLYNK_AUTH_TOKEN    "YOUR_AUTH_TOKEN"

char ssid[] = "YOUR_WIFI_NAME";
char pass[] = "YOUR_WIFI_PASSWORD";
```

**5. Upload & Verify**
- Board: `NodeMCU 1.0 (ESP-12E Module)`
- Serial Monitor: `115200 baud`
- Expected output:
```
Connecting to YourWiFi
..........WiFi connected
MPU6050 Found!
AccelY:0.12, AccelZ:-9.78, GyroX:0.01, GyroY:0.02, GyroZ:-0.01
```

---

## 📸 Demo & Output

<div align="center">

| Circuit Setup | Blynk Dashboard |
|:---:|:---:|
| ![Circuit](assets/images/circuit_setup.jpg) | ![Dashboard](assets/images/blynk_dashboard.jpg) |
| *ESP8266 + MPU6050 wired on breadboard* | *Live sensor readings on Blynk app* |

| Fall Alert Notification | Serial Monitor Output |
|:---:|:---:|
| ![Alert](assets/images/fall_alert.jpg) | ![Serial](assets/images/serial_output.jpg) |
| *Push notification triggered on caregiver phone* | *115200 baud serial data stream* |

> 📷 Replace image paths with your actual project photos.

<br/>

<img src="https://media.giphy.com/media/077i6AULCXc0FKTj9s/giphy.gif" width="380" alt="IoT Dashboard Animation"/>

</div>

---

## 🚀 Future Enhancements

| Enhancement | Description |
|:---|:---|
| 🤖 **AI Fall Prediction** | TensorFlow Lite model on-device to predict falls before they happen |
| 📱 **Custom Mobile App** | Flutter/React Native app with SOS button and caregiver management |
| 🗺️ **GPS Tracking** | NEO-6M GPS module for real-time location during fall events |
| ❤️ **Vitals Monitoring** | MAX30102 for heart rate + SpO2 alongside motion detection |
| ☁️ **Analytics Dashboard** | Web dashboard with fall history, frequency charts, and health trends |
| ⌚ **Wearable PCB** | Custom PCB + 3D-printed enclosure for a wristband form factor |

---

<img src="https://user-images.githubusercontent.com/74038190/212284100-561aa473-3905-4a80-b561-0d28506553ee.gif" width="100%">

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,11,20&height=120&section=footer&text=Built%20with%20❤️%20to%20protect%20our%20elders&fontSize=18&fontColor=ffffff&animation=twinkling" width="100%"/>

⭐ **If this project helped you, please give it a star!** ⭐

</div>
