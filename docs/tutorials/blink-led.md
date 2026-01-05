![Alt text](https://raw.githubusercontent.com/Sarvottam999/atal-tinkering-data/main/imgs/blink-led.png)

## 👋 Hello Little Makers!

In this project, we will make a **small light blink ON and OFF** using an **Arduino UNO**.  
This is one of the **first and easiest projects** to learn Arduino.  
Don’t worry — it’s fun and super easy! 😊

---

## 🧠 What Will We Learn?

- What is an **Arduino**
- What is an **LED**
- How to connect parts
- How to write a simple Arduino program
- How to make a light blink ✨

---

## 🧰 Things We Need

| Item | Quantity |
|----|----|
| Arduino UNO | 1 |
| LED (any color) | 1 |
| Resistor (220Ω or 330Ω) | 1 |
| Jumper Wires | 2 |
| USB Cable | 1 |

---

## 💡 What is an LED?

An **LED** is a tiny light.  
It has **two legs**:
- **Long leg** → Positive (+)
- **Short leg** → Negative (–)

---

## 🔌 Connecting the LED

Follow these steps carefully:

1. Connect the **long leg of LED** to **Pin 2** of Arduino  
2. Connect the **short leg of LED** to a **resistor**  
3. Connect the other side of the resistor to **GND (Ground)** on Arduino  

📌 The resistor protects the LED from damage.

---

## 💻 Arduino Code

Copy and paste this code into the **Arduino IDE**:

```cpp
void setup() {
  pinMode(2, OUTPUT);
}

void loop() {
  digitalWrite(2, HIGH);  // LED ON
  delay(1000);            // wait 1 second
  digitalWrite(2, LOW);   // LED OFF
  delay(1000);            // wait 1 second
}
```

## 🧩 Understanding the Code (Easy Words)

### 🔹 setup()

- Runs **one time**
- Tells Arduino that **Pin 2** will send power

### 🔹 loop()

- Runs **again and again**
- Turns LED **ON**
- Waits **1 second**
- Turns LED **OFF**
- Waits **1 second**

✨ This makes the LED blink 🎉

---

## ▶️ Run the Project

1. Connect Arduino to the computer
2. Open **Arduino IDE**
3. Select:
   - **Board:** Arduino UNO
   - **Port:** Correct COM Port
4. Click **Upload**
5. Watch your LED blink! 😄

---

## 🧪 Try These Fun Experiments!

- Change `1000` to `500` → faster blinking ⚡
- Change `1000` to `2000` → slower blinking 🐢
- Try a different LED color 🌈
