![Alt text](https://raw.githubusercontent.com/Sarvottam999/atal-tinkering-data/main/imgs/ir-master.png)

## 👋 Hello Little Makers!

In this project, we will use an **IR Sensor** to detect **objects and movements** using an **Arduino UNO**.  
The Arduino will then turn ON an **LED** or make a **Buzzer** beep — all on its own!  
Don't worry — it's super fun and easy! 😊

---

## 🧠 What Will We Learn?

- What is an **IR Sensor**
- What is a **Buzzer**
- How to connect all the parts
- How to write a simple Arduino program
- How to make **10 cool projects** using just an IR sensor! ✨

---

## 🧰 Things We Need

| Item | Quantity |
|----|----|
| Arduino UNO | 1 |
| IR Sensor Module | 1 |
| LED (any color) | 1 |
| Resistor (220Ω) | 1 |
| Buzzer | 1 |
| Jumper Wires | As needed |
| USB Cable | 1 |

---

## 💡 What is an IR Sensor?

An **IR Sensor** can **feel objects** without touching them!  
It sends out **invisible light** (Infrared) and checks if something is blocking it.

- **Object in front** → it sends a **LOW** signal
- **Nothing in front** → it sends a **HIGH** signal

📌 IR stands for **Infrared** — it's the same light used in TV remotes! 📺

---

## 🔊 What is a Buzzer?

A **Buzzer** is a tiny speaker that makes a **beep sound**.  
It has **two legs**:
- **Positive (+)** → connects to Arduino pin
- **Negative (–)** → connects to GND

---

## 🔌 Connecting the Parts

Follow these steps carefully:

### IR Sensor Module
1. Connect **VCC** to **5V** on Arduino
2. Connect **GND** to **GND** on Arduino
3. Connect **OUT** to **Pin 2** on Arduino

### LED
1. Connect **Anode (+) long leg** to **Pin 7** on Arduino
2. Connect **Cathode (–) short leg** through a **220Ω resistor** to **GND**

### Buzzer
1. Connect **Positive (+)** to **Pin 8** on Arduino
2. Connect **Negative (–)** to **GND** on Arduino

📌 The resistor protects the LED from damage.

---

## 📋 Connection Table

| Arduino Pin | Connected To | Component Pin |
|----|----|---|
| Pin 2 | IR Sensor Module | OUT |
| Pin 7 | LED | Anode (+) |
| Pin 8 | Buzzer | Positive (+) |
| 5V | IR Sensor Module | VCC |
| GND | IR Sensor Module | GND |
| GND | LED | Cathode (–) via resistor |
| GND | Buzzer | Negative (–) |

---

## 💻 Arduino Code

Copy and paste this code into the **Arduino IDE**:

```cpp
#define irPin 2
#define buzzerPin 8
#define ledPin 7

int projectIndex = 1;   // 🔥 CHANGE THIS (1 to 10)

int objectCount = 0;
int lastState = HIGH;
unsigned long lastTriggerTime = 0;
unsigned long interval = 1000;

String projectName = "";
bool ledState = LOW;
bool buzzerState = LOW;

void printProjectName() {
  switch (projectIndex) {
    case 1: projectName = "Line Detection Alarm"; break;
    case 2: projectName = "Intruder Alert"; break;
    case 3: projectName = "Object Counter"; break;
    case 4: projectName = "Security Beam Break System"; break;
    case 5: projectName = "Automatic Light"; break;
    case 6: projectName = "Hand Detection Toggle Switch"; break;
    case 7: projectName = "Speed Detection Concept"; break;
    case 8: projectName = "Touchless Switch"; break;
    case 9: projectName = "Conveyor Counter"; break;
    case 10: projectName = "Obstacle Alert System"; break;
    default: projectName = "Unknown Project";
  }

  Serial.println("=========================================");
  Serial.println("IR Detection System Projects");
  Serial.print("Running Project: ");
  Serial.println(projectName);
  Serial.println("=========================================");
}

void logStatus(String action) {
  Serial.print("[Time: ");
  Serial.print(millis());
  Serial.print(" ms] | Project: ");
  Serial.print(projectName);
  Serial.print(" | Sensor: ");
  Serial.print(digitalRead(irPin));
  Serial.print(" | LED: ");
  Serial.print(ledState ? "ON" : "OFF");
  Serial.print(" | Buzzer: ");
  Serial.print(buzzerState ? "ON" : "OFF");
  Serial.print(" | Count: ");
  Serial.print(objectCount);
  Serial.print(" | Action: ");
  Serial.println(action);
}

void setup() {
  pinMode(irPin, INPUT);
  pinMode(buzzerPin, OUTPUT);
  pinMode(ledPin, OUTPUT);

  Serial.begin(9600);
  delay(500);
  printProjectName();
}

void loop() {

  int sensorState = digitalRead(irPin);
  unsigned long currentTime = millis();

  if (sensorState != lastState) {
    Serial.println("-----------------------------------------");
    Serial.print("Sensor Changed → ");
    Serial.println(sensorState == LOW ? "OBJECT DETECTED" : "NO OBJECT");
  }

  switch (projectIndex) {

    case 1:
      if (sensorState == LOW) {
        ledState = HIGH;
        buzzerState = HIGH;
        logStatus("Line Detected - Alarm ON");
      } else {
        ledState = LOW;
        buzzerState = LOW;
        logStatus("No Line - Alarm OFF");
      }
      break;

    case 2:
      if (sensorState == LOW && lastState == HIGH) {
        ledState = HIGH;
        buzzerState = HIGH;
        logStatus("Intruder Detected!");
        delay(500);
        ledState = LOW;
        buzzerState = LOW;
      }
      break;

    case 3:
      if (sensorState == LOW && lastState == HIGH) {
        objectCount++;
        logStatus("Object Count Increased");
        delay(300);
      }
      break;

    case 4:
      if (sensorState == HIGH) {
        ledState = HIGH;
        buzzerState = LOW;
        logStatus("Beam Normal");
      } else {
        buzzerState = HIGH;
        logStatus("Beam Interrupted!");
        delay(200);
        buzzerState = LOW;
      }
      break;

    case 5:
      if (sensorState == LOW) {
        ledState = HIGH;
        logStatus("Light ON");
      } else {
        ledState = LOW;
        logStatus("Light OFF");
      }
      break;

    case 6:
      if (sensorState == LOW && lastState == HIGH) {
        ledState = !ledState;
        logStatus("Switch Toggled");
        delay(300);
      }
      break;

    case 7:
      if (sensorState == LOW) {
        if (currentTime - lastTriggerTime < interval) {
          buzzerState = HIGH;
          logStatus("High Speed Object!");
          delay(200);
          buzzerState = LOW;
        } else {
          logStatus("Normal Speed Object");
        }
        lastTriggerTime = currentTime;
      }
      break;

    case 8:
      if (sensorState == LOW) {
        ledState = HIGH;
        logStatus("Touch Detected");
      } else {
        ledState = LOW;
        logStatus("No Touch");
      }
      break;

    case 9:
      if (sensorState == LOW && lastState == HIGH) {
        objectCount++;
        ledState = HIGH;
        logStatus("Item Passed");
        delay(100);
        ledState = LOW;
      }
      break;

    case 10:
      if (sensorState == LOW) {
        buzzerState = HIGH;
        ledState = HIGH;
        logStatus("Obstacle Detected - Alarm ON");
      } else {
        buzzerState = LOW;
        ledState = LOW;
        logStatus("Path Clear");
      }
      break;
  }

  digitalWrite(ledPin, ledState);
  digitalWrite(buzzerPin, buzzerState);

  lastState = sensorState;
}
```

---

## 🧩 Understanding the Code (Easy Words)

### 🔹 setup()

- Runs **one time**
- Tells Arduino which pins are for **input** and **output**
- Starts the **Serial Monitor** so we can see messages

### 🔹 getLightState() / digitalRead()

- Reads the IR sensor
- Returns **LOW** when an **object is detected**
- Returns **HIGH** when the **path is clear**

### 🔹 loop()

- Runs **again and again**
- Checks the **IR sensor** every moment
- Runs the project you selected using `projectIndex`

✨ Change `projectIndex` to switch between projects! 🎉

---

## 🗂️ All 10 Projects at a Glance

| Mode | Project Name | What It Does |
|----|----|---|
| 1 | Line Detection Alarm | LED + Buzzer ON when object is near 🚨 |
| 2 | Intruder Alert | Short beep when someone passes 👤 |
| 3 | Object Counter | Counts every object that passes by 🔢 |
| 4 | Security Beam Break System | Buzzer beeps when beam is broken 🔦 |
| 5 | Automatic Light | LED turns ON when object is detected 💡 |
| 6 | Hand Detection Toggle Switch | Wave hand to toggle LED ON/OFF ✋ |
| 7 | Speed Detection Concept | Beeps if object moves too fast ⚡ |
| 8 | Touchless Switch | LED ON when hand is near 🖐️ |
| 9 | Conveyor Counter | Counts items on a conveyor belt 📦 |
| 10 | Obstacle Alert System | LED + Buzzer when obstacle found 🛑 |

---

## ▶️ Run the Project

1. Connect Arduino to the computer
2. Open **Arduino IDE**
3. Select:
   - **Board:** Arduino UNO
   - **Port:** Correct COM Port
4. Click **Upload**
5. Wave your hand in front of the IR sensor and watch the magic! 😄

---

## 🧪 Try These Fun Experiments!

- Change `projectIndex = 1` to `projectIndex = 10` → Full **Obstacle Alert**! 🛑
- Wave your hand fast in front of the sensor → it detects **speed** in Mode 7 ⚡
- Put small toys in front of the sensor → watch it **count** them in Mode 3 🔢
- Try **Mode 6** → wave your hand to **toggle the LED** ON and OFF like magic! ✨