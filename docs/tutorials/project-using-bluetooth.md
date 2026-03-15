![Alt text](https://raw.githubusercontent.com/Sarvottam999/atal-tinkering-data/main/imgs/bluetooth-master.png)

## 👋 Hello Little Makers!

In this project, we will use a **Bluetooth Module (HC-05)** to control an **LED** and **Buzzer** from your **phone** using an **Arduino UNO**!  
You can send commands from a Bluetooth app and make things happen wirelessly — no wires needed between you and the Arduino! 📱  
Don't worry — it's super fun and easy! 😊

---

## 🧠 What Will We Learn?

- What is a **Bluetooth Module (HC-05)**
- How to connect the parts
- How to send commands from your **phone**
- How to write a simple Arduino program
- How to make **15 cool wireless projects**! ✨

---

## 🧰 Things We Need

| Item | Quantity |
|----|----|
| Arduino UNO | 1 |
| Bluetooth Module HC-05 | 1 |
| LED (any color) | 1 |
| Resistor (220Ω) | 1 |
| Buzzer | 1 |
| Jumper Wires | As needed |
| USB Cable | 1 |
| Smartphone with Bluetooth | 1 |

---

## 💡 What is an HC-05 Bluetooth Module?

An **HC-05** lets your Arduino **talk to your phone wirelessly** using Bluetooth!  
- Your phone **sends a command** (like `1` or `0`)
- Arduino **receives it** and does something (like turning ON the LED)

📌 It works just like connecting wireless earphones to your phone! 🎧

---

## 🔊 What is a Buzzer?

A **Buzzer** is a tiny speaker that makes a **beep sound**.  
It has **two legs**:
- **Positive (+)** → connects to Arduino pin
- **Negative (–)** → connects to GND

---

## 🔌 Connecting the Parts

Follow these steps carefully:

### Bluetooth Module HC-05
1. Connect **VCC** to **5V** on Arduino
2. Connect **GND** to **GND** on Arduino
3. Connect **TX** to **Pin 11** on Arduino
4. Connect **RX** to **Pin 10** on Arduino

### LED
1. Connect **Anode (+) long leg** to **Pin 7** on Arduino
2. Connect **Cathode (–) short leg** through a **220Ω resistor** to **GND**

### Buzzer
1. Connect **Positive (+)** to **Pin 6** on Arduino
2. Connect **Negative (–)** to **GND** on Arduino

📌 The resistor protects the LED from damage.

---

## 📋 Connection Table

| Arduino Pin | Connected To | Component Pin |
|----|----|---|
| Pin 11 | Bluetooth HC-05 | TX |
| Pin 10 | Bluetooth HC-05 | RX |
| Pin 7 | LED | Anode (+) |
| Pin 6 | Buzzer | Positive (+) |
| 5V | Bluetooth HC-05 | VCC |
| GND | Bluetooth HC-05 | GND |
| GND | LED | Cathode (–) via resistor |
| GND | Buzzer | Negative (–) |

---

## 💻 Arduino Code

Copy and paste this code into the **Arduino IDE**:

```cpp
#include <SoftwareSerial.h>

// ================= SETTINGS =================
int projectIndex = 1;   // 🔥 CHANGE THIS (1 to 15)

SoftwareSerial BT(10, 11);

int led = 7;
int buzzer = 6;

String password = "1234";
String input = "";
bool silentMode = false;

// ============================================

void setup() {
  Serial.begin(9600);
  BT.begin(9600);
  pinMode(led, OUTPUT);
  pinMode(buzzer, OUTPUT);
  Serial.println("Bluetooth Multi Project System Started");
}

// ============================================

void loop() {
  if (!BT.available()) return;

  char cmd = BT.read();
  Serial.print("Command: ");
  Serial.println(cmd);

  switch (projectIndex) {

    // 1️⃣ Phone Controlled LED
    case 1:
      if (cmd == '1') digitalWrite(led, HIGH);
      if (cmd == '0') digitalWrite(led, LOW);
      break;

    // 2️⃣ Voice Style ON/OFF
    case 2:
      if (cmd == 'A') digitalWrite(led, HIGH);
      if (cmd == 'B') digitalWrite(led, LOW);
      break;

    // 3️⃣ Remote Alarm
    case 3:
      if (cmd == '1') tone(buzzer, 2000);
      if (cmd == '0') noTone(buzzer);
      break;

    // 4️⃣ Bluetooth Door Lock
    case 4:
      if (cmd == '#') {
        if (input == password) {
          digitalWrite(led, HIGH);
          delay(2000);
          digitalWrite(led, LOW);
        } else {
          tone(buzzer, 2500, 500);
        }
        input = "";
      } else {
        input += cmd;
      }
      break;

    // 5️⃣ Wireless Buzzer
    case 5:
      if (cmd == 'A') tone(buzzer, 1500, 500);
      break;

    // 6️⃣ App Controlled Multi Mode
    case 6:
      if (cmd == '1') digitalWrite(led, HIGH);
      if (cmd == '2') digitalWrite(led, LOW);
      if (cmd == '3') tone(buzzer, 2000, 500);
      break;

    // 7️⃣ Morse Blink System
    case 7:
      if (cmd == 'S') {
        for (int i = 0; i < 3; i++) {
          digitalWrite(led, HIGH); delay(200);
          digitalWrite(led, LOW);  delay(200);
        }
      }
      break;

    // 8️⃣ LED + Buzzer Combo
    case 8:
      if (cmd == '1') { digitalWrite(led, HIGH); tone(buzzer, 1500); }
      if (cmd == '0') { digitalWrite(led, LOW);  noTone(buzzer); }
      break;

    // 9️⃣ Remote Security Alert
    case 9:
      if (cmd == 'X') {
        for (int i = 0; i < 5; i++) {
          tone(buzzer, 2500); delay(200);
          noTone(buzzer);     delay(200);
        }
      }
      break;

    // 🔟 Text Response System
    case 10:
      if (cmd == '1') BT.println("Hello User");
      if (cmd == '2') BT.println("System Ready");
      break;

    // 1️⃣1️⃣ Bluetooth Panic Button
    case 11:
      if (cmd == 'P') {
        for (int i = 0; i < 10; i++) {
          digitalWrite(led, HIGH); tone(buzzer, 3000); delay(150);
          digitalWrite(led, LOW);  noTone(buzzer);     delay(150);
        }
      }
      break;

    // 1️⃣2️⃣ Pattern Blink Controller
    case 12:
      if (cmd == 'B') {
        digitalWrite(led, HIGH); delay(100);
        digitalWrite(led, LOW);  delay(100);
        digitalWrite(led, HIGH); delay(300);
        digitalWrite(led, LOW);
      }
      break;

    // 1️⃣3️⃣ Silent Alert Mode
    case 13:
      if (cmd == 'S') silentMode = !silentMode;
      if (cmd == 'A') {
        digitalWrite(led, HIGH);
        if (!silentMode) tone(buzzer, 2000, 300);
        delay(500);
        digitalWrite(led, LOW);
      }
      break;

    // 1️⃣4️⃣ Countdown Alarm
    case 14:
      if (cmd == 'C') {
        for (int i = 5; i > 0; i--) {
          Serial.print("Countdown: "); Serial.println(i);
          digitalWrite(led, HIGH); delay(300);
          digitalWrite(led, LOW);  delay(700);
        }
        tone(buzzer, 2500, 1000);
      }
      break;

    // 1️⃣5️⃣ Command Logger
    case 15:
      Serial.print("Received Command: ");
      Serial.println(cmd);
      digitalWrite(led, HIGH); delay(200);
      digitalWrite(led, LOW);
      break;
  }
}
```

---

## 🧩 Understanding the Code (Easy Words)

### 🔹 setup()

- Runs **one time**
- Tells Arduino which pins are for **input** and **output**
- Starts **Bluetooth** and **Serial Monitor**

### 🔹 BT.read()

- Reads the **command sent from your phone**
- Returns a **character** like `'1'`, `'A'`, `'P'`

### 🔹 loop()

- Runs **again and again**
- Waits for a **Bluetooth command** from your phone
- Runs the project you selected using `projectIndex`

✨ Change `projectIndex` to switch between projects! 🎉

---

## 🗂️ All 15 Projects at a Glance

| Mode | Project Name | Phone Command | What It Does |
|----|----|----|---|
| 1 | Phone Controlled LED | `1` / `0` | LED ON / OFF from phone 💡 |
| 2 | Voice Style ON/OFF | `A` / `B` | LED ON / OFF with letters 🔤 |
| 3 | Remote Alarm | `1` / `0` | Buzzer ON / OFF wirelessly 🔔 |
| 4 | Bluetooth Door Lock | Type `1234` + `#` | LED unlocks on correct password 🔐 |
| 5 | Wireless Buzzer | `A` | Single buzzer beep 📳 |
| 6 | App Controlled Multi Mode | `1` / `2` / `3` | LED + Buzzer combo control 🎛️ |
| 7 | Morse Blink System | `S` | LED blinks 3 times like Morse code ✨ |
| 8 | LED + Buzzer Combo | `1` / `0` | Both LED and Buzzer together 🚨 |
| 9 | Remote Security Alert | `X` | Fast alarm beeps 5 times 🛡️ |
| 10 | Text Response System | `1` / `2` | Arduino replies text to phone 💬 |
| 11 | Bluetooth Panic Button | `P` | Emergency flash + alarm 🆘 |
| 12 | Pattern Blink Controller | `B` | LED blinks in a special pattern 🌟 |
| 13 | Silent Alert Mode | `S` to toggle, `A` to alert | Alert without buzzer sound 🤫 |
| 14 | Countdown Alarm | `C` | 5-second countdown then alarm ⏱️ |
| 15 | Command Logger | Any key | Logs every command received 📋 |

---

## ▶️ Run the Project

1. Connect Arduino to the computer
2. Open **Arduino IDE**
3. Install **SoftwareSerial** (comes built-in!)
4. Select:
   - **Board:** Arduino UNO
   - **Port:** Correct COM Port
5. Click **Upload**
6. Open a **Bluetooth Terminal App** on your phone (e.g. *Serial Bluetooth Terminal*)
7. Pair with **HC-05** (default password: `1234`)
8. Send commands and watch the magic! 😄

---

## 🧪 Try These Fun Experiments!

- Try **Mode 1** → send `1` from phone → LED turns ON! 💡
- Try **Mode 4** → type `1234#` from app → LED unlocks like a real door! 🔐
- Try **Mode 7** → send `S` → LED blinks like a **Morse Code** signal! ✨
- Try **Mode 11** → send `P` → **Panic alarm** flashes and beeps fast! 🆘
- Try **Mode 14** → send `C` → watch the **5-second countdown** then alarm! ⏱️