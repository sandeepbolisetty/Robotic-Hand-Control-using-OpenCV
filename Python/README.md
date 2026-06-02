# Code Explanation

This document explains how the Gesture Control Robotic Hand software works, including both the Python program and the Arduino firmware.

---

# Python Program

The Python script is responsible for:

1. Capturing video from the webcam.
2. Detecting the user's hand.
3. Determining which fingers are open or closed.
4. Sending finger data to the Arduino.
5. Displaying the hand landmarks on the screen.

---

## Importing Libraries

```python
import cv2
import mediapipe as mp
import serial
import time
```

### Explanation

* `cv2` (OpenCV) handles webcam access and image processing.
* `mediapipe` detects and tracks hand landmarks.
* `serial` enables communication with the Arduino.
* `time` is used to delay execution while the serial connection initializes.

---

## Establishing Serial Communication

```python
ser = serial.Serial('COM3', 9600)
time.sleep(2)
```

### Explanation

The Arduino and Python program communicate through a USB serial connection.

* `COM3` is the communication port used by the Arduino.
* `9600` is the baud rate.
* `time.sleep(2)` allows the Arduino to reset and become ready before data is transmitted.

---

## Initializing MediaPipe

```python
mp_hands = mp.solutions.hands
hands = mp_hands.Hands()
mp_draw = mp.solutions.drawing_utils
```

### Explanation

MediaPipe provides a pre-trained hand tracking model.

This model identifies:

* Palm position
* Finger joints
* Finger tips

A total of **21 landmarks** are detected for each hand.

---

## Starting the Webcam

```python
cap = cv2.VideoCapture(0)
```

### Explanation

Opens the default webcam.

`0` represents the primary camera connected to the computer.

---

## Capturing Video Frames

```python
success, img = cap.read()
```

### Explanation

Reads a single frame from the webcam.

* `success` indicates whether the frame was captured.
* `img` contains the image data.

---

## Converting Image Format

```python
imgRGB = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
```

### Explanation

OpenCV uses BGR color format.

MediaPipe requires RGB format.

Therefore the image is converted before processing.

---

## Detecting Hands

```python
results = hands.process(imgRGB)
```

### Explanation

MediaPipe analyzes the frame and returns:

* Hand landmarks
* Hand orientation
* Finger positions

---

## Finger State Storage

```python
fingers = [0, 0, 0, 0, 0]
```

### Explanation

Stores the status of each finger.

```text
[Thumb, Index, Middle, Ring, Pinky]
```

Values:

```text
1 = Open
0 = Closed
```

---

## Thumb Detection

```python
fingers[0] = 1 if lm[4].x < lm[3].x else 0
```

### Explanation

Landmark:

* Tip = 4
* Joint = 3

If the thumb tip moves outward beyond the joint position:

```text
Thumb = Open
```

Otherwise:

```text
Thumb = Closed
```

---

## Index Finger Detection

```python
fingers[1] = 1 if lm[8].y < lm[6].y else 0
```

### Explanation

Landmarks:

* Tip = 8
* Joint = 6

If the fingertip is higher than the joint:

```text
Index Finger = Open
```

---

## Middle Finger Detection

```python
fingers[2] = 1 if lm[12].y < lm[10].y else 0
```

Uses the same logic as the index finger.

---

## Ring Finger Detection

```python
fingers[3] = 1 if lm[16].y < lm[14].y else 0
```

Checks whether the ring fingertip is above its joint.

---

## Pinky Finger Detection

```python
fingers[4] = 1 if lm[20].y < lm[18].y else 0
```

Checks whether the pinky fingertip is above its joint.

---

## Drawing Hand Landmarks

```python
mp_draw.draw_landmarks(
    img,
    handLms,
    mp_hands.HAND_CONNECTIONS
)
```

### Explanation

Draws:

* Hand joints
* Finger connections
* Palm structure

on the video feed.

---

## Creating Data Packet

```python
data = f"{fingers[0]} {fingers[1]} {fingers[2]} {fingers[3]} {fingers[4]}\n"
```

### Example

```text
1 1 0 0 1
```

Meaning:

```text
Thumb  = Open
Index  = Open
Middle = Closed
Ring   = Closed
Pinky  = Open
```

---

## Sending Data to Arduino

```python
ser.write(data.encode())
```

### Explanation

The finger information is converted into bytes and transmitted through USB serial communication.

---

## Exit Condition

```python
if cv2.waitKey(1) & 0xFF == 27:
    break
```

### Explanation

Pressing the ESC key closes the application.

---

# Arduino Program

The Arduino receives finger information and controls the servo motors.

---

## Including Servo Library

```cpp
#include <Servo.h>
```

Provides functions for controlling servo motors.

---

## Creating Servo Objects

```cpp
Servo s1, s2, s3, s4, s5;
```

Each object controls one finger.

---

## Attaching Servos

```cpp
s1.attach(3);
s2.attach(5);
s3.attach(6);
s4.attach(9);
s5.attach(10);
```

| Servo | Finger | Pin |
| ----- | ------ | --- |
| s1    | Thumb  | D3  |
| s2    | Index  | D5  |
| s3    | Middle | D6  |
| s4    | Ring   | D9  |
| s5    | Pinky  | D10 |

---

## Reading Serial Data

```cpp
String data = Serial.readStringUntil('\n');
```

Receives a complete line from Python.

Example:

```text
1 1 0 0 1
```

---

## Extracting Values

```cpp
sscanf(data.c_str(),
       "%d %d %d %d %d",
       &v1, &v2, &v3, &v4, &v5);
```

Separates the incoming string into five integer values.

---

## Controlling Servos

```cpp
s1.write(v1 ? 180 : 0);
```

Logic:

```text
1 → Servo moves to 180°
0 → Servo moves to 0°
```

The same operation is performed for all five servos.

---

# Complete System Workflow

```text
User Hand
    │
    ▼
Webcam
    │
    ▼
OpenCV
    │
    ▼
MediaPipe
    │
    ▼
Finger Detection
    │
    ▼
Serial Communication
    │
    ▼
Arduino Uno
    │
    ▼
Servo Motors
    │
    ▼
Robotic Hand
```

This workflow enables the robotic hand to mirror the user's hand movements in real time.
