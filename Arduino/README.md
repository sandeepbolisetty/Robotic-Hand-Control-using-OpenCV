# Arduino Firmware Documentation

## Overview

The Arduino Uno acts as the controller for the robotic hand. It receives finger position data from the Python application through serial communication and controls five servo motors corresponding to the five fingers of the robotic hand.

---

# Hardware Requirements

| Component                   | Quantity    |
| --------------------------- | ----------- |
| Arduino Uno R3              | 1           |
| HD1501MG Servo Motor        | 5           |
| External 5V–6V Power Supply | 1           |
| Jumper Wires                | As Required |

---

# Servo Connections

| Finger | Servo Object | Arduino Pin |
| ------ | ------------ | ----------- |
| Thumb  | s1           | D3          |
| Index  | s2           | D5          |
| Middle | s3           | D6          |
| Ring   | s4           | D9          |
| Pinky  | s5           | D10         |

---

# Program Workflow

```text
Python Program
      │
      ▼
Serial Communication
      │
      ▼
Arduino Uno
      │
      ▼
Parse Finger Data
      │
      ▼
Control Servo Motors
      │
      ▼
Move Robotic Hand
```

---

# Code Explanation

## Including Servo Library

```cpp
#include <Servo.h>
```

The Servo library provides functions for controlling servo motors.

---

## Creating Servo Objects

```cpp
Servo s1, s2, s3, s4, s5;
```

Five servo objects are created to represent:

* Thumb
* Index Finger
* Middle Finger
* Ring Finger
* Pinky Finger

---

## Setup Function

```cpp
void setup() {
  Serial.begin(9600);

  s1.attach(3);
  s2.attach(5);
  s3.attach(6);
  s4.attach(9);
  s5.attach(10);
}
```

### Purpose

1. Starts serial communication at 9600 baud.
2. Connects each servo object to its respective Arduino pin.

---

## Reading Incoming Data

```cpp
String data = Serial.readStringUntil('\n');
```

Example received data:

```text
1 1 0 0 1
```

Each number represents one finger:

```text
Thumb Index Middle Ring Pinky
```

Where:

```text
1 = Open
0 = Closed
```

---

## Parsing Finger Values

```cpp
sscanf(
  data.c_str(),
  "%d %d %d %d %d",
  &v1, &v2, &v3, &v4, &v5
);
```

Converts the received string into five integer variables.

Example:

```text
1 1 0 0 1
```

becomes:

```cpp
v1 = 1
v2 = 1
v3 = 0
v4 = 0
v5 = 1
```

---

## Controlling Servos

```cpp
s1.write(v1 ? 180 : 0);
```

Logic:

```text
If value = 1 → Servo moves to 180°
If value = 0 → Servo moves to 0°
```

The same logic is applied to all five fingers.

---

# Complete Arduino Source Code

```cpp
#include <Servo.h>

Servo s1, s2, s3, s4, s5;

void setup() {
  Serial.begin(9600);

  s1.attach(3);   // Thumb
  s2.attach(5);   // Index
  s3.attach(6);   // Middle
  s4.attach(9);   // Ring
  s5.attach(10);  // Pinky
}

void loop() {

  if (Serial.available() > 0) {

    String data = Serial.readStringUntil('\n');

    int v1, v2, v3, v4, v5;

    sscanf(
      data.c_str(),
      "%d %d %d %d %d",
      &v1, &v2, &v3, &v4, &v5
    );

    s1.write(v1 ? 180 : 0);
    s2.write(v2 ? 180 : 0);
    s3.write(v3 ? 180 : 0);
    s4.write(v4 ? 180 : 0);
    s5.write(v5 ? 180 : 0);
  }
}
```

---

# Upload Instructions

1. Open Arduino IDE.
2. Install the Servo library (usually pre-installed).
3. Connect the Arduino Uno to your computer.
4. Select the correct COM port.
5. Select **Arduino Uno** as the board.
6. Upload the code.
7. Run the Python gesture detection program.

The Arduino will now receive finger data and move the robotic hand accordingly.
