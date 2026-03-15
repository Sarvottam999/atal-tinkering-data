![Alt text](https://raw.githubusercontent.com/Sarvottam999/atal-tinkering-data/main/imgs/keypad-master.png)

## 👋 Hello Little Makers!

In this project, we will use a **4×4 Keypad** to press buttons and control an **LED** and **Buzzer** using an **Arduino UNO**.  
You can make a **password lock**, a **calculator**, a **voting machine**, and much more — all with one keypad!  
Don't worry — it's super fun and easy! 😊

---

## 🧠 What Will We Learn?

- What is a **4×4 Keypad**
- What is a **Buzzer**
- How to connect all the parts
- How to write a simple Arduino program
- How to make **10 cool projects** using just a keypad! ✨

---

## 🧰 Things We Need

| Item | Quantity |
|----|----|
| Arduino UNO | 1 |
| 4×4 Keypad | 1 |
| LED (any color) | 1 |
| Resistor (220Ω) | 1 |
| Buzzer | 1 |
| Jumper Wires | As needed |
| USB Cable | 1 |

---

## 💡 What is a 4×4 Keypad?

A **4×4 Keypad** is like a tiny keyboard with **16 buttons**!  
It has buttons: `1 2 3 A`, `4 5 6 B`, `7 8 9 C`, `* 0 # D`

- When you **press a button** → Arduino knows which key you pressed
- It uses **8 wires** — 4 for Rows and 4 for Columns

📌 It works just like the number pad on your phone! 📱

---

## 🔊 What is a Buzzer?

A **Buzzer** is a tiny speaker that makes a **beep sound**.  
It has **two legs**:
- **Positive (+)** → connects to Arduino pin
- **Negative (–)** → connects to GND

---

## 🔌 Connecting the Parts

Follow these steps carefully:

### 4×4 Keypad
1. Connect **Row 1** to **Pin 9** on Arduino
2. Connect **Row 2** to **Pin 8** on Arduino
3. Connect **Row 3** to **Pin 7** on Arduino
4. Connect **Row 4** to **Pin 6** on Arduino
5. Connect **Column 1** to **Pin 5** on Arduino
6. Connect **Column 2** to **Pin 4** on Arduino
7. Connect **Column 3** to **Pin 3** on Arduino
8. Connect **Column 4** to **Pin 2** on Arduino

### LED
1. Connect **Anode (+) long leg** to **Pin 12** on Arduino
2. Connect **Cathode (–) short leg** through a **220Ω resistor** to **GND**

### Buzzer
1. Connect **Positive (+)** to **Pin 11** on Arduino
2. Connect **Negative (–)** to **GND** on Arduino

📌 The resistor protects the LED from damage.

---

## 📋 Connection Table

| Arduino Pin | Connected To | Component Pin |
|----|----|---|
| Pin 9 | Keypad | Row 1 |
| Pin 8 | Keypad | Row 2 |
| Pin 7 | Keypad | Row 3 |
| Pin 6 | Keypad | Row 4 |
| Pin 5 | Keypad | Column 1 |
| Pin 4 | Keypad | Column 2 |
| Pin 3 | Keypad | Column 3 |
| Pin 2 | Keypad | Column 4 |
| Pin 12 | LED | Anode (+) |
| Pin 11 | Buzzer | Positive (+) |
| GND | LED | Cathode (–) via resistor |
| GND | Buzzer | Negative (–) |

---

## 💻 Arduino Code

Copy and paste this code into the **Arduino IDE**:

```cpp
#include <Keypad.h>

// ================= CONFIG =================
int projectIndex = 1;   // 🔥 CHANGE THIS (1 to 10)

const byte ROWS = 4;
const byte COLS = 4;

char keys[ROWS][COLS] = {
  {'1','2','3','A'},
  {'4','5','6','B'},
  {'7','8','9','C'},
  {'*','0','#','D'}
};

byte rowPins[ROWS] = {9,8,7,6};
byte colPins[COLS] = {5,4,3,2};

Keypad keypad = Keypad(makeKeymap(keys), rowPins, colPins, ROWS, COLS);

int buzzer = 11;
int led = 12;

String input = "";
String password = "1234";
int voteA = 0, voteB = 0;
bool systemArmed = false;
int balance = 1000;

// ==========================================

void setup() {
  Serial.begin(9600);
  pinMode(buzzer, OUTPUT);
  pinMode(led, OUTPUT);
  Serial.println("System Ready...");
}

void loop() {

  char key = keypad.getKey();

  if (key) {
    tone(buzzer, 1000, 100);
    Serial.print("Key: ");
    Serial.println(key);
  }

  switch(projectIndex) {
    case 1: passwordLock(key); break;
    case 2: calculator(key); break;
    case 3: safeSystem(key); break;
    case 4: quizMachine(key); break;
    case 5: votingMachine(key); break;
    case 6: pinAlarm(key); break;
    case 7: digitalSafe(key); break;
    case 8: commandBuzzer(key); break;
    case 9: miniATM(key); break;
    case 10: multiModeSelector(key); break;
  }
}

// ================= PROJECT 1 =================
void passwordLock(char key) {
  if (!key) return;
  if (key == '#') {
    if (input == password) {
      Serial.println("Access Granted");
      digitalWrite(led, HIGH);
      delay(2000);
      digitalWrite(led, LOW);
    } else {
      Serial.println("Wrong Password");
      tone(buzzer, 2000, 500);
    }
    input = "";
  } else {
    input += key;
  }
}

// ================= PROJECT 2 =================
void calculator(char key) {
  static long num1 = 0;
  static long num2 = 0;
  static char op = 0;
  static bool second = false;

  if (!key) return;

  if (key >= '0' && key <= '9') {
    if (!second) {
      num1 = num1 * 10 + (key - '0');
      Serial.print("Num1: "); Serial.println(num1);
    } else {
      num2 = num2 * 10 + (key - '0');
      Serial.print("Num2: "); Serial.println(num2);
    }
  }

  if (key == 'A') { op = '+'; second = true; Serial.println("Operator +"); }
  if (key == 'B') { op = '-'; second = true; Serial.println("Operator -"); }
  if (key == 'C') { op = '*'; second = true; Serial.println("Operator *"); }

  if (key == '#') {
    long result = 0;
    if (op == '+') result = num1 + num2;
    if (op == '-') result = num1 - num2;
    if (op == '*') result = num1 * num2;
    Serial.print("Result: "); Serial.println(result);
    num1 = 0; num2 = 0; op = 0; second = false;
  }

  if (key == 'D') {
    num1 = 0; num2 = 0; op = 0; second = false;
    Serial.println("Cleared");
  }
}

// ================= PROJECT 3 =================
void safeSystem(char key) {
  if (!key) return;
  if (key == 'A') { systemArmed = true; Serial.println("System Armed"); }
  if (key == 'B') { systemArmed = false; Serial.println("System Disarmed"); }
  if (systemArmed && key) { tone(buzzer, 2500, 200); }
}

// ================= PROJECT 4 =================
void quizMachine(char key) {
  Serial.println("Q: 2+2=? Press 4");
  if (key == '4') {
    Serial.println("Correct!");
    digitalWrite(led, HIGH);
    delay(1000);
    digitalWrite(led, LOW);
  }
}

// ================= PROJECT 5 =================
void votingMachine(char key) {
  if (key == '1') voteA++;
  if (key == '2') voteB++;
  if (key == '#') {
    Serial.print("Votes A: "); Serial.println(voteA);
    Serial.print("Votes B: "); Serial.println(voteB);
  }
}

// ================= PROJECT 6 =================
void pinAlarm(char key) {
  if (!key) return;
  if (key == '*') { Serial.println("Alarm Triggered!"); tone(buzzer, 3000, 1000); }
}

// ================= PROJECT 7 =================
void digitalSafe(char key) {
  if (!key) return;
  if (key == 'D') {
    password = input;
    Serial.println("Password Changed");
    input = "";
  } else {
    input += key;
  }
}

// ================= PROJECT 8 =================
void commandBuzzer(char key) {
  if (key == '1') tone(buzzer, 1000);
  if (key == 'A') tone(buzzer, 2000);
  if (key == '2') noTone(buzzer);
}

// ================= PROJECT 9 =================
void miniATM(char key) {
  if (key == '1') { Serial.print("Balance: "); Serial.println(balance); }
  if (key == '2') { balance -= 100; Serial.println("Withdraw 100"); }
}

// ================= PROJECT 10 =================
void multiModeSelector(char key) {
  if (!key) return;
  if (key == '1') digitalWrite(led, HIGH);
  if (key == '2') digitalWrite(led, LOW);
  if (key == '3') tone(buzzer, 1500, 500);
}
```

---

## 🧩 Understanding the Code (Easy Words)

### 🔹 setup()

- Runs **one time**
- Tells Arduino which pins are for **input** and **output**
- Starts the **Serial Monitor** so we can see messages

### 🔹 keypad.getKey()

- Checks if **any button is pressed**
- Returns the **key character** like `'1'`, `'A'`, `'#'`
- If nothing is pressed, it returns nothing

### 🔹 loop()

- Runs **again and again**
- Checks **which key** was pressed
- Runs the project you selected using `projectIndex`

✨ Change `projectIndex` to switch between projects! 🎉

---

## 🗂️ All 10 Projects at a Glance

| Mode | Project Name | What It Does |
|----|----|---|
| 1 | Password Lock | Type `1234` + `#` to unlock LED 🔐 |
| 2 | Calculator | Press numbers + `A/B/C` + `#` to calculate 🧮 |
| 3 | Safe System | Press `A` to arm, `B` to disarm 🔒 |
| 4 | Quiz Machine | Answer quiz question with keypad 🧠 |
| 5 | Voting Machine | Press `1` for A, `2` for B, `#` for results 🗳️ |
| 6 | PIN Alarm | Press `*` to trigger alarm 🚨 |
| 7 | Digital Safe | Press `D` to save a new password 🔑 |
| 8 | Command Buzzer | Press `1` / `A` / `2` to control buzzer 🔔 |
| 9 | Mini ATM | Press `1` to check balance, `2` to withdraw 💰 |
| 10 | Multi Mode Selector | Press `1` / `2` / `3` to control LED & Buzzer 🎛️ |

---

## ▶️ Run the Project

1. Connect Arduino to the computer
2. Open **Arduino IDE**
3. Install the **Keypad Library** from Library Manager
4. Select:
   - **Board:** Arduino UNO
   - **Port:** Correct COM Port
5. Click **Upload**
6. Open **Serial Monitor** and start pressing keys! 😄

---

## 🧪 Try These Fun Experiments!

- Try **Mode 1** → type `1234` and press `#` → LED turns ON! 🔐
- Try **Mode 2** → press `5`, then `A`, then `3`, then `#` → see `8` as result! 🧮
- Try **Mode 5** → press `1` many times, then `2` a few times, then `#` → see who wins! 🗳️
- Try **Mode 9** → press `2` three times, then press `1` → see your new balance! 💰