# Hardware

This folder contains the hardware design files for the Gesture Control Robotic Hand.

## Circuit Diagram

The complete wiring schematic is available in:

- `circuit_diagram.png`

## Wiring Overview

### Arduino Uno Connections

| Servo Motor | Arduino Pin |
|-------------|-------------|
| Thumb Servo | D3 |
| Index Servo | D5 |
| Middle Servo | D6 |
| Ring Servo | D9 |
| Little Servo | D10 |

### Power Connections

- Servo VCC → External 5V–6V Supply
- Servo GND → Common Ground
- Arduino GND → Common Ground
- Arduino USB → Computer

### Communication

```text
Webcam
   │
   ▼
OpenCV + MediaPipe (Python)
   │
   ▼
USB Serial Communication
   │
   ▼
Arduino Uno
   │
   ▼
5 Servo Motors
   │
   ▼
Robotic Hand
```

## Notes

- Do not power all servos directly from the Arduino 5V pin.
- Use an external power supply capable of providing sufficient current.
- Ensure all grounds are connected together.
