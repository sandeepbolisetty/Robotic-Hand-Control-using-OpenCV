# Bill of Materials (BOM)

## Project Information

**Project Name:** Gesture Control Robotic Hand Using OpenCV

**Controller:** Arduino Uno R3

**Programming Language:** Python & Arduino C++

**Computer Vision Library:** OpenCV + MediaPipe

---

# Hardware Components

| S.No | Component | Quantity |
|------|-----------|----------|
| 1 | Arduino Uno R3 | 1 |
| 2 | HD1501MG High Torque Servo Motor | 5 |
| 3 | USB Webcam / Laptop Camera | 1 |
| 4 | External 5V–6V Power Supply | 1 |
| 5 | Jumper Wires | 1 Set |
| 6 | USB Type-B Cable | 1 |
| 7 | Servo Horns | 5 |
| 8 | Servo Mounting Screws | 1 Set |
| 9 | Fishing Line / Tendon Wire | As Required |
| 10 | M3 Nuts and Bolts | As Required |
| 11 | 3D Printed Hand Components | 1 Set |

---

# Software Requirements

| S.No | Software |
|------|----------|
| 1 | Python 3.x |
| 2 | OpenCV |
| 3 | MediaPipe |
| 4 | NumPy |
| 5 | PySerial |
| 6 | Arduino IDE |
| 7 | Git |
| 8 | GitHub |

---

# Servo Connections

| Finger | Arduino Pin |
|---------|------------|
| Thumb | D3 |
| Index | D5 |
| Middle | D6 |
| Ring | D9 |
| Little | D10 |

---

# Power Connections

| Device | Connection |
|----------|-----------|
| Servo VCC | External 5V–6V Supply |
| Servo GND | Common Ground |
| Arduino GND | Common Ground |
| Arduino USB | Computer |

---

# Communication Architecture

```text
User Hand Gesture
        │
        ▼
Webcam
        │
        ▼
OpenCV + MediaPipe
        │
        ▼
Gesture Recognition
        │
        ▼
Python Program
        │
        ▼
Serial Communication (USB)
        │
        ▼
Arduino Uno
        │
        ▼
HD1501MG Servo Motors
        │
        ▼
Robotic Hand
```

---

# 3D Printed Components

The following 3D printable files are included in the `3D_Files` directory:

- files-e5p1
- files-hand5
- files-servohorn
- fingerdesign-all-1
- forarm-9-2
- forarm-9-3
- forearm9-1
- hand5thumb3
- myminifactory-handback
- servo-hold
- servo-hold-1

---

# Printing Recommendations

- Material: PLA / PETG
- Layer Height: 0.2 mm
- Infill: 20–30%
- Nozzle Diameter: 0.4 mm
- Print Scale: 100%

---

# Notes

- Use an external power supply for all servos.
- Do not power the HD1501MG servos directly from the Arduino 5V pin.
- Ensure all grounds are connected together.
- Verify servo rotation direction before final assembly.
