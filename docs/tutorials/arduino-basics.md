![Alt text](https://raw.githubusercontent.com/Sarvottam999/atal-tinkering-data/main/imgs/arduino-basics.png)


## 1️⃣ POWER SECTION (bottom left)

| Pin  | Use          | Simple explanation                                         |
|------|-------------|-----------------------------------------------------------|
| VIN  | Input voltage | “Plug a battery here to power the Arduino”               |
| GND  | Ground       | “This is the negative side, like the ‘return path’ for electricity” |
| 5V   | 5 Volt output | “Use this to give 5 volts to sensors, LEDs, etc.”       |
| 3.3V | 3.3 Volt output | “Some small sensors need 3.3 volts, use this pin”    |

---

## 2️⃣ RESET Button (top left corner)

“Press this button and Arduino starts over like a restart on your phone”

---

## 3️⃣ DIGITAL PINS (top right row, 0–13)

| Pin        | Use             | Child-friendly explanation                                |
|------------|----------------|----------------------------------------------------------|
| 0 (RX)     | Serial receive  | “Arduino can get messages from computer”                |
| 1 (TX)     | Serial send     | “Arduino can send messages to computer”                 |
| 2–13       | General digital pins | “These are like tiny switches you can turn ON or OFF” |
| 3, 5, 6, 9, 10, 11 | PWM      | “These pins can dim LEDs or make motors go slower/faster” |
| 13         | Built-in LED    | “A small LED is already connected here, so we can test without adding an LED” |

---

## 4️⃣ ANALOG INPUT PINS (A0–A5, bottom right)

| Pin  | Use          | Simple explanation                                         |
|------|-------------|-----------------------------------------------------------|
| A0–A5 | Analog inputs | “These read sensors that give numbers between 0 and 1023, like how bright light is” |

---

## 5️⃣ SPECIAL PINS (near power pins)

| Pin  | Use            | Explanation                                             |
|------|----------------|---------------------------------------------------------|
| AREF | Analog reference | “Helps Arduino read sensors accurately, like setting a ruler” |
| GND  | More ground     | “Another negative side, like extra return path”        |

---

## 🔹 Extra Info

- **USB port (top left)** → powers Arduino + uploads code  
- **Barrel jack (left)** → for battery or external power  
- **TX/RX LEDs** → blink when Arduino is sending/receiving data
