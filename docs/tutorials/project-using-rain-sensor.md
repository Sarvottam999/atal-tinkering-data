![Alt text](https://raw.githubusercontent.com/Sarvottam999/atal-tinkering-data/main/imgs/rain-sensor.png)

## 👋 Hello Little Makers!

In this project, we will use a **Rain Sensor** to detect **water drops** using an **Arduino UNO**!  
When it rains, the Arduino will automatically turn ON an **LED** — just like a smart weather detector! 🌧️  
Don't worry — it's super fun and easy! 😊

---

## 🧠 What Will We Learn?

- What is a **Rain Sensor**
- How to connect the parts
- How to write a simple Arduino program
- How to make a **smart rain detector** that turns ON a light! ✨

---

## 🧰 Things We Need

| Item | Quantity |
|----|----|
| Arduino UNO | 1 |
| Rain Sensor Module | 1 |
| LED (any color) | 1 |
| Resistor (220Ω) | 1 |
| Jumper Wires | As needed |
| USB Cable | 1 |

---

## 💡 What is a Rain Sensor?

A **Rain Sensor** has a special plate that can **feel water drops**!  
- When **water touches the plate** → it sends a **LOW** signal
- When the plate is **dry** → it sends a **HIGH** signal

📌 It is used in smart cars to turn on wipers automatically! 🚗

---

## 🔌 Connecting the Parts

Follow these steps carefully:

### Rain Sensor Module
1. Connect **VCC** to **5V** on Arduino
2. Connect **GND** to **GND** on Arduino
3. Connect **DO** to **Pin 2** on Arduino

### LED
1. Connect **Anode (+) long leg** through a **220Ω resistor** to **Pin 8** on Arduino
2. Connect **Cathode (–) short leg** to **GND**

📌 The resistor protects the LED from damage.

---

## 📋 Connection Table

| Arduino Pin | Connected To | Component Pin |
|----|----|---|
| Pin 2 | Rain Sensor Module | DO |
| Pin 8 | LED | Anode (+) via 220Ω resistor |
| 5V | Rain Sensor Module | VCC |
| GND | Rain Sensor Module | GND |
| GND | LED | Cathode (–) |

---

## ⚙️ How Does It Work?

1. The rain sensor plate **detects water drops** 💧
2. When water touches the plate → module sends a **LOW** signal from DO pin
3. Arduino **reads the signal**
4. If rain is detected → **LED turns ON** 💡
5. If no rain → **LED stays OFF**

---

## 💻 Arduino Code

Copy and paste this code into the **Arduino IDE**:

```cpp
int rainPin = 2;
int ledPin = 8;

void setup() {
  pinMode(rainPin, INPUT);
  pinMode(ledPin, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  int rainState = digitalRead(rainPin);

  if (rainState == LOW) {
    Serial.println("Rain Detected!");
    digitalWrite(ledPin, HIGH);
  }
  else {
    Serial.println("No Rain");
    digitalWrite(ledPin, LOW);
  }

  delay(500);
}
```

---

## 🧩 Understanding the Code (Easy Words)

### 🔹 setup()

- Runs **one time**
- Tells Arduino that **Pin 2** will receive signal from rain sensor
- Tells Arduino that **Pin 8** will send power to LED
- Starts **Serial Monitor** so we can see messages

### 🔹 digitalRead(rainPin)

- Reads the rain sensor
- Returns **LOW** when it is **raining** 🌧️
- Returns **HIGH** when it is **dry** ☀️

### 🔹 loop()

- Runs **again and again**
- Checks the **rain sensor** every 0.5 seconds
- Turns LED **ON** if rain is detected
- Turns LED **OFF** if no rain

✨ This makes a smart rain detector! 🎉

---

## ▶️ Run the Project

1. Connect Arduino to the computer
2. Open **Arduino IDE**
3. Select:
   - **Board:** Arduino UNO
   - **Port:** Correct COM Port
4. Click **Upload**
5. Open **Serial Monitor**
6. Put a few drops of water on the sensor plate and watch the LED turn ON! 😄

---

## 🧪 Try These Fun Experiments!

- Put a **drop of water** on the sensor → LED turns ON 💡
- **Wipe the sensor dry** → LED turns OFF ☀️
- Change `delay(500)` to `delay(100)` → faster response ⚡
- Connect a **Buzzer** to Pin 9 and add `tone(9, 2000)` → make it beep when it rains! 🔔