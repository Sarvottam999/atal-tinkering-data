![Alt text](https://raw.githubusercontent.com/Sarvottam999/atal-tinkering-data/main/imgs/project-using-ldr.jpg)

## 👋 Hello Little Makers!

In this project, we will use a **Light Sensor (LDR)** to detect **dark and bright light** using an **Arduino UNO**.  
The Arduino will then turn ON an **LED** or make a **Buzzer** beep — all by itself!  
Don't worry — it's super fun and easy! 😊

---

## 🧠 What Will We Learn?

- What is an **LDR (Light Sensor)**
- What is a **Buzzer**
- How to connect all the parts
- How to write a simple Arduino program
- How to make **10 cool projects** using just light! ✨

---

## 🧰 Things We Need

| Item | Quantity |
|----|----|
| Arduino UNO | 1 |
| LDR Module | 1 |
| LED (any color) | 1 |
| Resistor (220Ω) | 1 |
| Buzzer | 1 |
| Jumper Wires | As needed |
| USB Cable | 1 |

---

## 💡 What is an LDR?

An **LDR** is a special sensor that can **feel light**!  
- In **bright light** → it sends a LOW signal
- In **darkness** → it sends a HIGH signal

📌 LDR stands for **Light Dependent Resistor**

---

## 🔊 What is a Buzzer?

A **Buzzer** is a tiny speaker that makes a **beep sound**.  
It has **two legs**:
- **Positive (+)** → connects to Arduino pin
- **Negative (–)** → connects to GND

---

## 🔌 Connecting the Parts

Follow these steps carefully:

### LDR Module
1. Connect **VCC** to **5V** on Arduino
2. Connect **GND** to **GND** on Arduino
3. Connect **OUT / DO** to **Pin 2** on Arduino

### LED
1. Connect **Anode (+) long leg** to **Pin 6** on Arduino
2. Connect **Cathode (–) short leg** through a **220Ω resistor** to **GND**

### Buzzer
1. Connect **Positive (+)** to **Pin 9** on Arduino
2. Connect **Negative (–)** to **GND** on Arduino

📌 The resistor protects the LED from damage.

---

## 📋 Connection Table

| Arduino Pin | Connected To | Component Pin |
|----|----|---|
| Pin 2 | LDR Module | OUT / DO |
| Pin 6 | LED | Anode (+) |
| Pin 9 | Buzzer | Positive (+) |
| 5V | LDR Module | VCC |
| GND | LDR Module | GND |
| GND | LED | Cathode (–) via resistor |
| GND | Buzzer | Negative (–) |

---

## 💻 Arduino Code

Copy and paste this code into the **Arduino IDE**:

```cpp
#define ldrPin 2
#define ledPin 6
#define buzzerPin 9

int projectIndex = 1;   // 🔥 CHANGE THIS (1 to 10)

int currentState;
int lastState = -1;

unsigned long darkStartTime = 0;
bool darkTimerRunning = false;

void setup() {
  pinMode(ldrPin, INPUT);
  pinMode(ledPin, OUTPUT);
  pinMode(buzzerPin, OUTPUT);
  Serial.begin(9600);

  Serial.println("===== LDR MASTER SYSTEM STARTED =====");
}

int getLightState() {
  return digitalRead(ldrPin);  // HIGH = DARK (usually)
}

void loop() {

  currentState = getLightState();

  if (currentState != lastState) {
    Serial.print("Light Changed -> ");
    if (currentState == HIGH)
      Serial.println("DARK");
    else
      Serial.println("BRIGHT");

    lastState = currentState;
  }

  switch (projectIndex) {

    // 1️⃣ Automatic Night Lamp
    case 1:
      digitalWrite(ledPin, currentState == HIGH ? HIGH : LOW);
      break;

    // 2️⃣ Light Alarm System
    case 2:
      if (currentState == LOW)
        tone(buzzerPin, 2000);
      else
        noTone(buzzerPin);
      break;

    // 3️⃣ Darkness Alert
    case 3:
      if (currentState == HIGH) {
        digitalWrite(ledPin, HIGH);
        tone(buzzerPin, 1500);
      } else {
        digitalWrite(ledPin, LOW);
        noTone(buzzerPin);
      }
      break;

    // 4️⃣ Laser Tripwire Style
    case 4:
      if (currentState == HIGH) {
        tone(buzzerPin, 2500);
        delay(200);
        noTone(buzzerPin);
        delay(200);
      }
      break;

    // 5️⃣ Dark Blink Indicator
    case 5:
      if (currentState == HIGH) {
        digitalWrite(ledPin, HIGH);
        delay(100);
        digitalWrite(ledPin, LOW);
        delay(100);
      }
      break;

    // 6️⃣ Night Reminder Beep
    case 6:
      if (currentState == HIGH) {
        tone(buzzerPin, 1000);
        delay(300);
        noTone(buzzerPin);
        delay(700);
      }
      break;

    // 7️⃣ Study Lamp Alert
    case 7:
      if (currentState == HIGH) {
        digitalWrite(ledPin, HIGH);
        tone(buzzerPin, 1800);
        delay(100);
        noTone(buzzerPin);
      } else {
        digitalWrite(ledPin, LOW);
      }
      break;

    // 8️⃣ Sudden Light Entry Alert
    case 8:
      if (currentState == LOW && lastState == HIGH) {
        tone(buzzerPin, 2000);
        delay(300);
        noTone(buzzerPin);
      }
      break;

    // 9️⃣ Sunlight Detector
    case 9:
      digitalWrite(ledPin, currentState == LOW ? HIGH : LOW);
      break;

    // 🔟 Smart Intruder Memory Alarm
    case 10:
      if (currentState == HIGH) {
        if (!darkTimerRunning) {
          darkStartTime = millis();
          darkTimerRunning = true;
          Serial.println("Darkness detected... starting timer");
        }

        if (millis() - darkStartTime >= 5000) {
          Serial.println("Intruder Confirmed! Alarm ON");
          tone(buzzerPin, 2200);
          digitalWrite(ledPin, HIGH);
        }

      } else {
        darkTimerRunning = false;
        digitalWrite(ledPin, LOW);
        noTone(buzzerPin);
      }
      break;
  }
}
```

---

## 🧩 Understanding the Code (Easy Words)

### 🔹 setup()

- Runs **one time**
- Tells Arduino which pins are for **input** and **output**
- Starts the **Serial Monitor** so we can see messages

### 🔹 getLightState()

- Reads the LDR sensor
- Returns **HIGH** when it is **DARK**
- Returns **LOW** when it is **BRIGHT**

### 🔹 loop()

- Runs **again and again**
- Checks the **light level** every moment
- Runs the project you selected using `projectIndex`

✨ Change `projectIndex` to try different projects! 🎉

---

## 🗂️ All 10 Projects at a Glance

| Mode | Project Name | What It Does |
|----|----|---|
| 1 | Automatic Night Lamp | LED turns ON in dark 🌙 |
| 2 | Light Alarm System | Buzzer beeps in bright light ☀️ |
| 3 | Darkness Alert | LED + Buzzer ON when dark 🚨 |
| 4 | Laser Tripwire Style | Buzzer beeps fast when dark ⚡ |
| 5 | Dark Blink Indicator | LED blinks in dark ✨ |
| 6 | Night Reminder Beep | Buzzer beeps slowly at night 🔔 |
| 7 | Study Lamp Alert | LED + short beep when dark 📚 |
| 8 | Sudden Light Entry Alert | Beeps when light suddenly appears 💡 |
| 9 | Sunlight Detector | LED ON only in bright light 🌞 |
| 10 | Smart Intruder Alarm | Alarm after 5 seconds of darkness 🔐 |

---

## ▶️ Run the Project

1. Connect Arduino to the computer
2. Open **Arduino IDE**
3. Select:
   - **Board:** Arduino UNO
   - **Port:** Correct COM Port
4. Click **Upload**
5. Cover the LDR with your hand and watch the magic! 😄

---

## 🧪 Try These Fun Experiments!

- Change `projectIndex = 1` to `projectIndex = 3` → LED **and** Buzzer together! 🔔
- Cover the LDR with your hand → it thinks it is **night time** 🌙
- Shine a torch on the LDR → it thinks it is **day time** ☀️
- Try **Mode 10** and wait 5 seconds in the dark → Intruder Alarm! 🚨