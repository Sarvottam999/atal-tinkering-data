![Alt text](https://raw.githubusercontent.com/Sarvottam999/atal-tinkering-data/main/imgs/soil-moisture.png)

## 👋 Hello Little Makers!

In this project, we will use a **Soil Moisture Sensor** to check if the soil is **dry, normal, or wet** using an **Arduino UNO**!  
The Arduino reads the moisture level and shows the result in the **Serial Monitor** — just like a smart farming assistant! 🌱  
Don't worry — it's super fun and easy! 😊

---

## 🧠 What Will We Learn?

- What is a **Soil Moisture Sensor**
- How to connect the sensor to Arduino
- How to read **analog values**
- How to check if soil is **Dry, Normal, or Wet**
- How to see the output in **Serial Monitor** ✨

---

## 🧰 Things We Need

| Item | Quantity |
|----|----|
| Arduino UNO | 1 |
| Soil Moisture Sensor Module | 1 |
| Jumper Wires | 3 |
| USB Cable | 1 |
| A pot with soil (for testing) | 1 |

---

## 💡 What is a Soil Moisture Sensor?

A **Soil Moisture Sensor** checks **how much water is in the soil**!  
It has two metal prongs that go into the soil.

- When soil is **very dry** → it gives a **high number** (like 800+)
- When soil is **normal** → it gives a **medium number** (300–700)
- When soil is **very wet** → it gives a **low number** (below 300)

📌 Farmers use this to know **when to water their plants**! 🌾

---

## 🔌 Connecting the Parts

Follow these steps carefully:

### Soil Moisture Sensor Module
1. Connect **VCC** to **5V** on Arduino
2. Connect **GND** to **GND** on Arduino
3. Connect **AO** to **A0** on Arduino

📌 We use the **AO (Analog Output)** pin to get the exact moisture number!

---

## 📋 Connection Table

| Soil Moisture Sensor Pin | Arduino Pin |
|----|----|
| VCC | 5V |
| GND | GND |
| AO | A0 |

---

## 💻 Arduino Code

Copy and paste this code into the **Arduino IDE**:

```cpp
int sensorPin = A0;
int moistureValue = 0;

void setup() {
  Serial.begin(9600);
}

void loop() {
  moistureValue = analogRead(sensorPin);

  Serial.print("Moisture Value: ");
  Serial.println(moistureValue);

  if (moistureValue > 700) {
    Serial.println("Soil: DRY");
  }
  else if (moistureValue > 300) {
    Serial.println("Soil: NORMAL");
  }
  else {
    Serial.println("Soil: WET");
  }

  Serial.println("----------------");

  delay(2000);
}
```

---

## 🧩 Understanding the Code (Easy Words)

### 🔹 setup()

- Runs **one time**
- Starts the **Serial Monitor** so we can see the moisture values

### 🔹 analogRead(sensorPin)

- Reads the moisture level from the sensor
- Returns a number between **0 and 1023**
- **Higher number** = **drier soil** 🏜️
- **Lower number** = **wetter soil** 💧

### 🔹 loop()

- Runs **again and again** every 2 seconds
- Reads the **moisture value**
- Prints whether soil is **DRY**, **NORMAL**, or **WET**

✨ Push the sensor into soil and watch the number change! 🎉

---

## 📊 What Do the Numbers Mean?

| Moisture Value | Soil Condition |
|----|----|
| Above 700 | 🏜️ DRY — Water your plant! |
| 300 to 700 | 🌿 NORMAL — Soil is perfect |
| Below 300 | 💧 WET — No need to water |

---

## ▶️ How to See the Output

1. Upload the code to Arduino
2. Open **Serial Monitor** in Arduino IDE
3. Set **Baud Rate = 9600**
4. You will see something like this:

```
Moisture Value: 812
Soil: DRY
----------------
Moisture Value: 450
Soil: NORMAL
----------------
```

---

## ▶️ Run the Project

1. Connect all parts as shown in the table above
2. Connect Arduino to the computer
3. Open **Arduino IDE**
4. Select:
   - **Board:** Arduino UNO
   - **Port:** Correct COM Port
5. Click **Upload**
6. Open **Serial Monitor** (speed: 9600)
7. Put the sensor into soil and watch the readings! 😄

---

## 🧪 Try These Fun Experiments!

- Put the sensor in **dry soil** → see a high number like `812` 🏜️
- **Pour some water** into the soil → watch the number go down 💧
- Hold the sensor prongs together with wet fingers → see **WET**! 🖐️
- Try soil from **different plants** and compare the readings 🌵🌺
- Change `700` and `300` to different numbers and see what happens! 🔢