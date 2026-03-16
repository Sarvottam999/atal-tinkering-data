![Alt text](https://raw.githubusercontent.com/Sarvottam999/atal-tinkering-data/main/imgs/ultrasonic-buzzer.png)

## 👋 Hello Little Makers!

In this project, we will make a **smart distance sensor** using an **Arduino UNO**, an **Ultrasonic Sensor**, and a **Buzzer**!  
The buzzer will make **different sounds** depending on how close or far an object is.  
This project can do **10 amazing things** — all with the same circuit! 😊

---

## 🧠 What Will We Learn?

- What is an **Ultrasonic Sensor**
- What is a **Buzzer**
- How to connect parts to Arduino
- How to **measure distance** using sound waves
- How to make **10 cool projects** with one circuit ✨

---

## 🧰 Things We Need

| Item | Quantity |
|----|----|
| Arduino UNO | 1 |
| Ultrasonic Sensor (HC-SR04) | 1 |
| Buzzer | 1 |
| Jumper Wires | 6–8 |
| USB Cable | 1 |

---

## 💡 What is an Ultrasonic Sensor?

An Ultrasonic Sensor is like the **ears of a bat**! 🦇  
It sends out a **sound wave** and waits for it to **bounce back**.  
By measuring the time taken, it knows **how far away an object is**.

It has **4 pins**:
- **VCC** → Power (+5V)
- **GND** → Ground (–)
- **TRIG** → Sends the sound wave
- **ECHO** → Receives the bounced wave

---

## 🔔 What is a Buzzer?

A **Buzzer** makes sound when electricity passes through it.  
It has **2 pins**:
- **Positive (+)** → Connected to Arduino pin
- **Negative (–)** → Connected to GND

---

## 🔌 Connecting the Parts

Follow these steps carefully:

### Ultrasonic Sensor (HC-SR04)
1. Connect **VCC** to **5V** on Arduino
2. Connect **GND** to **GND** on Arduino
3. Connect **TRIG** to **Pin 9** on Arduino
4. Connect **ECHO** to **Pin 10** on Arduino

### Buzzer
1. Connect **Positive (+)** to **Pin 6** on Arduino
2. Connect **Negative (–)** to **GND** on Arduino

📌 Double check all connections before powering on!

---

## 📋 Connection Table

### 1️⃣ Arduino → Ultrasonic Sensor

| Arduino Pin | Ultrasonic Sensor Pin |
|----|----|
| 5V | VCC |
| GND | GND |
| Pin 9 | TRIG |
| Pin 10 | ECHO |

### 2️⃣ Arduino → Buzzer

| Arduino Pin | Buzzer Pin |
|----|----|
| Pin 6 | Positive (+) |
| GND | Negative (–) |

---

## 💻 Arduino Code

Copy and paste this code into the **Arduino IDE**:

```cpp
#define trigPin 9
#define echoPin 10
#define buzzerPin 6

long duration;
int distance;

int projectIndex = 1;   // 🔥 CHANGE THIS (1 to 10)

// For object counter project
int lastState = 0;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(buzzerPin, OUTPUT);
  Serial.begin(9600);
}

int getDistance() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);

  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);

  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;
  return distance;
}

void loop() {

  int d = getDistance();
  Serial.println(d);

  switch (projectIndex) {

    // 1️⃣ Parking Distance Alarm
    case 1:
      if (d < 100) {
        int delayTime = d * 5;
        tone(buzzerPin, 1000);
        delay(100);
        noTone(buzzerPin);
        delay(delayTime);
      }
      break;

    // 2️⃣ Table Edge Safety Alarm
    case 2:
      if (d > 20) {
        tone(buzzerPin, 1500);
      } else {
        noTone(buzzerPin);
      }
      break;

    // 3️⃣ Blind Spot Alert
    case 3:
      if (d < 50) {
        tone(buzzerPin, 1200);
        delay(200);
        noTone(buzzerPin);
        delay(200);
      }
      break;

    // 4️⃣ Door Entry Alert
    case 4:
      if (d < 80) {
        tone(buzzerPin, 2000);
        delay(500);
        noTone(buzzerPin);
        delay(500);
      }
      break;

    // 5️⃣ Restricted Area Alarm
    case 5:
      if (d < 30) {
        tone(buzzerPin, 2500);
      } else {
        noTone(buzzerPin);
      }
      break;

    // 6️⃣ Social Distance Reminder
    case 6:
      if (d < 100) {
        tone(buzzerPin, 1000);
        delay(300);
        noTone(buzzerPin);
        delay(300);
      }
      break;

    // 7️⃣ Obstacle Detection Alarm
    case 7:
      if (d < 60) {
        tone(buzzerPin, 1800);
        delay(100);
        noTone(buzzerPin);
        delay(100);
      }
      break;

    // 8️⃣ Object Counting Alarm
    case 8:
      if (d < 20 && lastState == 0) {
        tone(buzzerPin, 2000);
        delay(200);
        noTone(buzzerPin);
        lastState = 1;
      }
      if (d > 30) {
        lastState = 0;
      }
      break;

    // 9️⃣ Ultrasonic Theremin
    case 9:
      if (d >= 5 && d <= 50) {
        int freq = map(d, 5, 50, 2000, 200);
        tone(buzzerPin, freq);
      } else {
        noTone(buzzerPin);
      }
      delay(100);
      break;

    // 🔟 Bag Theft Alert
    case 10:
      if (d < 40) {
        tone(buzzerPin, 3000);
        delay(100);
        noTone(buzzerPin);
        delay(100);
      }
      break;

    default:
      noTone(buzzerPin);
      break;
  }
}
```

---

## 🧩 Understanding the Code (Easy Words)

### 🔹 getDistance()

- Sends a tiny **sound pulse** from TRIG pin
- Waits for the pulse to **bounce back** on ECHO pin
- Calculates the **distance in centimeters**

### 🔹 setup()

- Runs **one time**
- Sets TRIG as **output**, ECHO as **input**, Buzzer as **output**
- Starts **Serial Monitor** to show distance

### 🔹 loop()

- Runs **again and again**
- Gets the **current distance**
- Picks the right project using `projectIndex`

### 🔹 projectIndex

- Change this number **(1 to 10)** to switch projects!
- Example: `int projectIndex = 1;` → **Parking Alarm**

✨ Move your hand closer and farther to hear different sounds! 🎉

---

## 🗂️ All 10 Projects at a Glance

| Mode | Project Name | How It Works |
|----|----|----|
| 1 | Parking Distance Alarm | Beeps faster when object gets closer 🚗 |
| 2 | Table Edge Safety Alarm | Beeps when object moves too far away 🪑 |
| 3 | Blind Spot Alert | Beeps when something is within 50 cm 👁️ |
| 4 | Door Entry Alert | Beeps when someone walks through a door 🚪 |
| 5 | Restricted Area Alarm | Continuous beep when zone is entered 🚫 |
| 6 | Social Distance Reminder | Beeps when someone is too close 🧍 |
| 7 | Obstacle Detection Alarm | Fast beep when obstacle is detected 🛑 |
| 8 | Object Counting Alarm | Beeps once every time an object passes 🔢 |
| 9 | Ultrasonic Theremin | Changes music pitch with your hand! 🎵 |
| 10 | Bag Theft Alert | Fast alarm if someone gets too close to your bag 🎒 |

---

## ▶️ Run the Project

1. Connect all parts as shown in the tables above
2. Connect Arduino to the computer
3. Open **Arduino IDE**
4. Change `projectIndex` to the project number you want
5. Select:
   - **Board:** Arduino UNO
   - **Port:** Correct COM Port
6. Click **Upload**
7. Watch the magic happen! 😄

---

## 🧪 Try These Fun Experiments!

- Change `projectIndex` from `1` to `10` to try all projects 🔄
- Open **Serial Monitor** to see the distance in real time 📊
- Move your hand **closer and farther** to hear different sounds 🎵
- Try the **Theremin (Mode 9)** — it's like playing music with your hand! 🎹