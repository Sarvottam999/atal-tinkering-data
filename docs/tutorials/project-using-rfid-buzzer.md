![Alt text](https://raw.githubusercontent.com/Sarvottam999/atal-tinkering-data/main/imgs/rfid-master.png)

## 👋 Hello Little Makers!

In this project, we will build a smart **RFID system** using an **Arduino UNO**, an **RFID RC522 sensor**, an **LED**, and a **Buzzer**!  
Just **tap a card** and the system reacts — opens doors, marks attendance, counts votes, and much more!  
This one circuit can do **10 amazing projects**! 🎉

---

## 🧠 What Will We Learn?

- What is an **RFID Sensor**
- How **card scanning** works
- How to connect RFID to Arduino
- How to write an RFID program
- How to make **10 cool projects** with one circuit ✨

---

## 🧰 Things We Need

| Item | Quantity |
|----|----|
| Arduino UNO | 1 |
| RFID Module (RC522) | 1 |
| RFID Card or Key Tag | 1 |
| LED (any color) | 1 |
| Resistor (220Ω) | 1 |
| Buzzer | 1 |
| Jumper Wires | 10–12 |
| USB Cable | 1 |

---

## 💡 What is an RFID Sensor?

**RFID** stands for **Radio Frequency Identification**. 📡  
It is the same technology used in **school ID cards**, **metro cards**, and **library cards**!

When you bring a card close to the sensor, it reads a **secret number called a UID** from the card.  
Arduino can then decide what to do based on that number.

The **RC522 module** has 7 pins:

- **VCC** → Power **(3.3V only! ⚠️)**
- **GND** → Ground
- **SDA/SS** → Chip Select
- **SCK** → Clock
- **MOSI** → Data In
- **MISO** → Data Out
- **RST** → Reset

---

## 🔌 Connecting the Parts

Follow these steps carefully:

### RFID RC522 Module
1. Connect **SDA/SS** to **Pin 10** on Arduino
2. Connect **SCK** to **Pin 13** on Arduino
3. Connect **MOSI** to **Pin 11** on Arduino
4. Connect **MISO** to **Pin 12** on Arduino
5. Connect **RST** to **Pin 9** on Arduino
6. Connect **VCC** to **3.3V** on Arduino ⚠️
7. Connect **GND** to **GND** on Arduino

### LED
1. Connect **Anode (+) long leg** to **Pin 7** on Arduino
2. Connect **Cathode (–) short leg** through a **220Ω resistor** to **GND**

### Buzzer
1. Connect **Positive (+)** to **Pin 6** on Arduino
2. Connect **Negative (–)** to **GND** on Arduino

⚠️ **Important:** Always connect RFID VCC to **3.3V**, NOT 5V. Using 5V can **damage the module**!

---

## 📋 Connection Table

### 1️⃣ RFID RC522 → Arduino

| RFID Pin | Arduino Pin |
|----|----|
| SDA / SS | Pin 10 |
| SCK | Pin 13 |
| MOSI | Pin 11 |
| MISO | Pin 12 |
| RST | Pin 9 |
| VCC | 3.3V ⚠️ |
| GND | GND |

### 2️⃣ LED → Arduino

| LED Pin | Arduino Pin |
|----|----|
| Anode (+) | Pin 7 |
| Cathode (–) | GND (via 220Ω resistor) |

### 3️⃣ Buzzer → Arduino

| Buzzer Pin | Arduino Pin |
|----|----|
| Positive (+) | Pin 6 |
| Negative (–) | GND |

---

## 📦 Install the Library First!

Before uploading the code, we need to install the **MFRC522 library**:

1. Open **Arduino IDE**
2. Go to **Sketch → Include Library → Manage Libraries**
3. Search for **MFRC522**
4. Click **Install**

✅ Now you are ready to upload the code!

---

## 💻 Arduino Code

Copy and paste this code into the **Arduino IDE**:

```cpp
#include <SPI.h>
#include <MFRC522.h>

// ================= SETTINGS =================
int projectIndex = 1;   // 🔥 CHANGE THIS (1 to 10)

#define SS_PIN 10
#define RST_PIN 9

#define LED 7
#define BUZZER 6

MFRC522 rfid(SS_PIN, RST_PIN);

String uid = "";
int votes = 0;
int balance = 500;
bool systemArmed = true;

// ============================================

void setup() {
  Serial.begin(9600);
  SPI.begin();
  rfid.PCD_Init();

  pinMode(LED, OUTPUT);
  pinMode(BUZZER, OUTPUT);

  Serial.println("RFID Multi Project System Started");
}

// ============================================

void loop() {

  if (!rfid.PICC_IsNewCardPresent()) return;
  if (!rfid.PICC_ReadCardSerial()) return;

  uid = "";
  for (byte i = 0; i < rfid.uid.size; i++)
    uid += String(rfid.uid.uidByte[i], HEX);

  Serial.print("Card UID: ");
  Serial.println(uid);

  switch (projectIndex) {

    // 1️⃣ Door Access
    case 1:
      Serial.println("Door Access Granted");
      digitalWrite(LED, HIGH);
      tone(BUZZER, 1500, 200);
      delay(2000);
      digitalWrite(LED, LOW);
      break;

    // 2️⃣ Attendance System
    case 2:
      Serial.println("Attendance Marked");
      digitalWrite(LED, HIGH);
      tone(BUZZER, 1200, 200);
      delay(500);
      digitalWrite(LED, LOW);
      break;

    // 3️⃣ Security Alarm
    case 3:
      systemArmed = !systemArmed;
      Serial.println(systemArmed ? "System Armed" : "System Disarmed");
      if (systemArmed) {
        tone(BUZZER, 2500);
        digitalWrite(LED, HIGH);
        delay(1000);
        noTone(BUZZER);
        digitalWrite(LED, LOW);
      }
      break;

    // 4️⃣ Payment System
    case 4:
      balance -= 50;
      Serial.print("Payment Done. Balance: ");
      Serial.println(balance);
      digitalWrite(LED, HIGH);
      tone(BUZZER, 1500, 200);
      delay(500);
      digitalWrite(LED, LOW);
      break;

    // 5️⃣ Voting Machine
    case 5:
      votes++;
      Serial.print("Total Votes: ");
      Serial.println(votes);
      digitalWrite(LED, HIGH);
      tone(BUZZER, 1000, 150);
      delay(500);
      digitalWrite(LED, LOW);
      break;

    // 6️⃣ Secret Message
    case 6:
      Serial.println("Hello User");
      for (int i = 0; i < 3; i++) {
        digitalWrite(LED, HIGH); delay(200);
        digitalWrite(LED, LOW);  delay(200);
      }
      break;

    // 7️⃣ Treasure Box
    case 7:
      Serial.println("Treasure Box Opened");
      digitalWrite(LED, HIGH);
      tone(BUZZER, 1500, 300);
      delay(2000);
      digitalWrite(LED, LOW);
      break;

    // 8️⃣ Quiz Machine
    case 8:
      Serial.println("Quiz Answer Received");
      digitalWrite(LED, HIGH);
      tone(BUZZER, 1200, 200);
      delay(500);
      digitalWrite(LED, LOW);
      break;

    // 9️⃣ Smart Locker
    case 9:
      Serial.println("Locker Opened");
      digitalWrite(LED, HIGH);
      tone(BUZZER, 1000, 200);
      delay(1500);
      digitalWrite(LED, LOW);
      break;

    // 🔟 Multi Mode Controller
    case 10:
      Serial.println("Mode Activated");
      digitalWrite(LED, HIGH);
      tone(BUZZER, 1500);
      delay(500);
      digitalWrite(LED, LOW);
      noTone(BUZZER);
      break;
  }

  delay(500);
}
```

---

## 🧩 Understanding the Code (Easy Words)

### 🔹 setup()

- Runs **one time**
- Starts the **RFID sensor** and **Serial Monitor**
- Sets **LED** and **Buzzer** as output

### 🔹 loop()

- Runs **again and again**
- Waits for a **card to be scanned**
- Reads the card's **UID** (unique number)
- Runs the correct project based on `projectIndex`

### 🔹 projectIndex

- Change this number **(1 to 10)** to switch projects!
- Example: `int projectIndex = 2;` → **Attendance System**

### 🔹 uid

- Every RFID card has a **unique secret number**
- Arduino reads it and prints it on **Serial Monitor**
- You can use this number to **allow or block** specific cards!

✨ Tap your card and watch the magic happen! 🎉

---

## 🗂️ All 10 Projects at a Glance

| Mode | Project Name | What Happens When Card is Scanned |
|----|----|----|
| 1 | Door Access | LED ON + Buzzer beeps → Door opens 🚪 |
| 2 | Attendance System | LED blinks + Attendance marked in Serial Monitor 📋 |
| 3 | Security Alarm | Card arms or disarms the alarm 🔐 |
| 4 | Payment System | Deducts ₹50 from balance each scan 💳 |
| 5 | Voting Machine | Counts one vote per card scan 🗳️ |
| 6 | Secret Message | Prints a secret message + LED blinks 3 times 🤫 |
| 7 | Treasure Box | LED glows + Buzzer plays → Box unlocked 🏴‍☠️ |
| 8 | Quiz Machine | Records quiz answer with LED + Buzzer ✅ |
| 9 | Smart Locker | Opens locker with LED + beep 🔓 |
| 10 | Multi Mode Controller | Activates a custom mode 🎛️ |

---

## ▶️ Run the Project

1. Connect all parts as shown in the tables above
2. Connect Arduino to the computer
3. Open **Arduino IDE**
4. Install the **MFRC522 library** (see steps above)
5. Change `projectIndex` to the project number you want
6. Select:
   - **Board:** Arduino UNO
   - **Port:** Correct COM Port
7. Click **Upload**
8. Open **Serial Monitor** (speed: 9600)
9. Tap your RFID card and watch the magic! 😄

---

## 🧪 Try These Fun Experiments!

- Change `projectIndex` from `1` to `10` to try all projects 🔄
- Open **Serial Monitor** to see the card UID number 📊
- Try scanning **different cards** — each has a unique UID! 🃏
- In **Mode 4**, start with a bigger `balance` number and watch it decrease 💰
- In **Mode 5**, count votes and declare a class winner! 🏆