

![Alt text](https://raw.githubusercontent.com/Sarvottam999/atal-tinkering-data/main/imgs/dustbin.png)

## 2. Project Description

A Smart Dustbin is an automated waste bin that opetrns its lid automatically when a person approaches. The system uses an ultrasonic sensor to detect distance and a servo motor to open and close the lid without physical contact.

---

## 3. Objective

To design and simulate a touchless dustbin that improves hygiene by automatically opening and closing its lid based on proximity detection.

---

## 4. Equipment / Components Required


::contentReference[oaicite:1]{index=1}


| No. | Component                    | Quantity    |
| --- | ---------------------------- | ----------- |
| 1   | Arduino UNO                  | 1           |
| 2   | Ultrasonic Sensor (HC-SR04)  | 1           |
| 3   | Positional Micro Servo Motor | 1           |
| 4   | Jumper Wires                 | As required |
| 5   | Breadboard (optional)        | 1           |
| 6   | USB / Power Source           | 1           |

---

## 5. Working Principle

The ultrasonic sensor continuously measures the distance of objects in front of the dustbin. When an object is detected within a predefined range, the Arduino processes this input and rotates the servo motor to open the lid. When the object moves away, the servo returns to its original position, closing the lid.

---

## 6. Circuit Connections


::contentReference[oaicite:2]{index=2}


### Ultrasonic Sensor (HC-SR04)

| Sensor Pin | Arduino Pin   |
| ---------- | ------------- |
| VCC        | 5V            |
| GND        | GND           |
| TRIG       | Digital Pin 9 |
| ECHO       | Digital Pin 10|

### Servo Motor

| Servo Wire      | Arduino Pin   |
| --------------- | ------------- |
| Red (VCC)       | 5V            |
| Brown (GND)     | GND           |
| Orange (Signal) | Digital Pin 6 |

---

## 7. Arduino Program

```cpp
#include <Servo.h>

Servo lidServo;

const int trigPin = 9;
const int echoPin = 10;
const int servoPin = 6;

long duration;
int distance;

void setup() {
  lidServo.attach(servoPin);
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  lidServo.write(0);
}

void loop() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);

  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;

  if (distance > 0 && distance < 20) {
    lidServo.write(90);
  } else {
    lidServo.write(0);
  }

  delay(200);
}
```

![Alt text](https://raw.githubusercontent.com/Sarvottam999/atal-tinkering-data/main/imgs/dustbin_circuit.png)