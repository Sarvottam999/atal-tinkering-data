## 1️⃣ Arduino Connections

| Arduino Pin | Connected Component | Component Pin |
| --- | --- | --- |
| 5V | Ultrasonic Sensor | VCC |
| 5V | Servo Motor | Red (VCC) |
| GND | Ultrasonic Sensor | GND |
| GND | Servo Motor | Brown / Black (GND) |
| Pin 9 | Ultrasonic Sensor | TRIG |
| Pin 10 | Ultrasonic Sensor | ECHO |
| Pin 6 | Servo Motor | Signal (Orange / Yellow) |

---

## 2️⃣ Ultrasonic Sensor (HC-SR04) Connections

| Ultrasonic Pin | Connected To | Arduino Pin |
| --- | --- | --- |
| VCC | Power | 5V |
| GND | Ground | GND |
| TRIG | Digital Input | Pin 9 |
| ECHO | Digital Output | Pin 10 |

---

## 3️⃣ Servo Motor Connections

| Servo Wire | Connected To | Arduino Pin |
| --- | --- | --- |
| Red | Power | 5V |
| Brown / Black | Ground | GND |
| Orange / Yellow | Signal | Pin 6 |

---

## 💻 Arduino Code (10 Modes)

```cpp
#include <Servo.h>

#define MODE 10   // <<< CHANGE THIS NUMBER (1–10)

const int trigPin = 9;
const int echoPin = 10;
const int servoPin = 6;

Servo myServo;

long duration;
int distance;
int currentAngle = 0;

long readDistance() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;

  return distance;
}

void logStatus(String modeName) {
  Serial.print("[MODE ");
  Serial.print(MODE);
  Serial.print(" - ");
  Serial.print(modeName);
  Serial.print("] Distance: ");
  Serial.print(distance);
  Serial.print(" cm | Servo Angle: ");
  Serial.println(currentAngle);
}

void setup() {
  Serial.begin(9600);
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  myServo.attach(servoPin);
  myServo.write(0);

  Serial.println("System Started...");
}

void loop() {

  distance = readDistance();

  switch(MODE) {

    case 1:  // Automatic Dustbin
      if (distance < 20) {
        currentAngle = 90;
        myServo.write(currentAngle);
        logStatus("Automatic Dustbin - OPEN");
        delay(3000);

        currentAngle = 0;
        myServo.write(currentAngle);
        logStatus("Automatic Dustbin - CLOSE");
        delay(1000);
      }
    break;

    case 2:  // Parking Barrier
      if (distance < 15) {
        currentAngle = 100;
      } else {
        currentAngle = 0;
      }
      myServo.write(currentAngle);
      logStatus("Parking Barrier");
    break;

    case 3:  // Hand Sanitizer
      if (distance < 10) {
        currentAngle = 70;
        myServo.write(currentAngle);
        logStatus("Hand Sanitizer - DISPENSE");
        delay(1000);

        currentAngle = 0;
        myServo.write(currentAngle);
        delay(2000);
      }
    break;

    case 4:  // Door Opener
      if (distance < 25) {
        currentAngle = 120;
      } else {
        currentAngle = 0;
      }
      myServo.write(currentAngle);
      logStatus("Door Opener");
    break;

    case 5:  // Object Sorting
      if (distance < 10) {
        currentAngle = 45;
      } else if (distance < 20) {
        currentAngle = 90;
      } else {
        currentAngle = 135;
      }
      myServo.write(currentAngle);
      logStatus("Object Sorting Gate");
    break;

    case 6:  // Radar Scanner
      Serial.println("Radar Scan Starting...");
      for (int angle = 0; angle <= 180; angle++) {
        myServo.write(angle);
        delay(15);
        int d = readDistance();
        Serial.print("Angle: ");
        Serial.print(angle);
        Serial.print(" | Distance: ");
        Serial.print(d);
        Serial.println(" cm");
      }
      for (int angle = 180; angle >= 0; angle--) {
        myServo.write(angle);
        delay(15);
        int d = readDistance();
        Serial.print("Angle: ");
        Serial.print(angle);
        Serial.print(" | Distance: ");
        Serial.print(d);
        Serial.println(" cm");
      }
    break;

    case 7:  // Smart Tap
      if (distance < 12) {
        currentAngle = 80;
      } else {
        currentAngle = 0;
      }
      myServo.write(currentAngle);
      logStatus("Smart Tap");
    break;

    case 8:  // Distance Based Angle
      currentAngle = map(distance, 5, 40, 0, 180);
      currentAngle = constrain(currentAngle, 0, 180);
      myServo.write(currentAngle);
      logStatus("Distance Based Angle Control");
      delay(200);
    break;

    case 9:  // Motion Pointer
      if (distance < 30) {
        currentAngle = map(distance, 5, 30, 180, 0);
        myServo.write(currentAngle);
      }
      logStatus("Motion Controlled Pointer");
      delay(100);
    break;

    case 10:  // Mini Robot Head
      if (distance < 20) {
        currentAngle = 60;
        myServo.write(currentAngle);
        logStatus("Robot Head - LEFT");
        delay(300);

        currentAngle = 120;
        myServo.write(currentAngle);
        logStatus("Robot Head - RIGHT");
        delay(300);
      } else {
        currentAngle = 90;
        myServo.write(currentAngle);
        logStatus("Robot Head - CENTER");
      }
    break;
  }

  delay(100);
}
```

---

## 🧩 Mode Guide

| Mode | Project Name |
| --- | --- |
| 1 | Automatic Dustbin |
| 2 | Parking Barrier |
| 3 | Hand Sanitizer |
| 4 | Door Opener |
| 5 | Object Sorting Gate |
| 6 | Radar Scanner |
| 7 | Smart Tap |
| 8 | Distance Based Angle Control |
| 9 | Motion Controlled Pointer |
| 10 | Mini Robot Head |

📌 Change `#define MODE 10` to any number (1–10) to switch projects!