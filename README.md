# Gesture Control Robotic Hand Using OpenCV

## 📌 Project Overview

This project implements a **Gesture Control Robotic Hand** using **Computer Vision (OpenCV)** and **Arduino**. The system detects hand gestures through a webcam and controls a robotic hand in real time. Finger movements are tracked using image processing techniques, and corresponding commands are sent to the robotic hand to replicate the detected gesture.

The project demonstrates the integration of **Computer Vision**, **Human-Computer Interaction**, **Embedded Systems**, and **Robotics**.

---

## 🎯 Features

- Real-time hand gesture detection
- Finger counting using OpenCV
- Gesture recognition through webcam
- Serial communication with Arduino
- Real-time robotic hand movement
- Low-cost and easy-to-build system
- Expandable for advanced gesture commands

---

## 🛠️ Technologies Used

### Software
- Python 3.10
- OpenCV
- MediaPipe
- NumPy
- PySerial
- Arduino IDE

### Hardware
- Arduino Uno
- Servo Motors
- Robotic Hand
- USB Webcam / Laptop Camera
- Jumper Wires
- External Power Supply

---

## 📂 Project Structure

```
Gesture Control Pipeline
│
├── Camera Input
│   └── Webcam captures hand gesture
│
├── Computer Vision Layer
│   ├── OpenCV processes video frame
│   ├── MediaPipe detects hand landmarks
│   └── Finger counting algorithm
│
├── Decision Layer
│   ├── Gesture classification
│   └── Command generation (0-5)
│
├── Communication Layer
│   └── PySerial → USB COM Port
│
├── Embedded Layer
│   └── Arduino Uno receives command
│
├── Control Layer
│   └── Servo angle calculation
│
└── Actuation Layer
    ├── Thumb Servo
    ├── Index Servo
    ├── Middle Servo
    ├── Ring Servo
    └── Little Servo
         │
         ▼
      Robotic Hand Motion
```

---

## ⚙️ Working Principle

1. Webcam captures live video feed.
2. OpenCV processes each frame.
3. MediaPipe detects hand landmarks.
4. Finger count is calculated.
5. Corresponding command is sent to Arduino.
6. Arduino controls servo motors.
7. Robotic hand replicates the detected gesture.

---

## 🖥️ Installation

### Install Required Libraries

```bash
pip install opencv-python mediapipe numpy pyserial
```

Or

```bash
pip install -r requirements.txt
```

---

## 🚀 Usage

### Step 1: Upload Arduino Code

Open Arduino IDE and upload:

```cpp
robotic_hand.ino
```

### Step 2: Run Python Program

```bash
python gesture_detection.py
```

### Step 3: Show Hand Gestures

The webcam will detect your fingers and control the robotic hand accordingly.

---

## ✋ Supported Gestures

| Fingers Detected | Action |
|------------------|---------|
| 0 | Close Hand |
| 1 | Thumb Open |
| 2 | Two Fingers Open |
| 3 | Three Fingers Open |
| 4 | Four Fingers Open |
| 5 | Fully Open Hand |

---

## 🔌 Hardware Connections

| Finger | Servo Pin |
|----------|-----------|
| Thumb | D3 |
| Index | D5 |
| Middle | D6 |
| Ring | D9 |
| Little | D10 |

> Use an external power supply when powering multiple servos.

---

## 📊 Applications

- Prosthetic Hand Development
- Human Robot Interaction
- Industrial Automation
- Robotics Education
- Assistive Technology

---

## 🔮 Future Improvements

- Machine Learning Gesture Recognition
- Bluetooth Control
- Wi-Fi Control
- ROS Integration
- Custom Gesture Commands
- Multi-Hand Tracking

---

## 👨‍💻 Author

**Bolisetty Sandeep**

B.Tech – Robotics and Automation

Gesture Control Robotic Hand Project


## ⭐ Support

If you found this project useful:

⭐ Star the repository

🍴 Fork the repository

📢 Share it with others

---

### "Controlling a Robotic Hand Using Human Gestures and Computer Vision"
