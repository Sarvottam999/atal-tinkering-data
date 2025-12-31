
![Alt text](https://raw.githubusercontent.com/Sarvottam999/atal-tinkering-data/main/imgs/automatic-plant-watering-system.png)

## 2. Project Description  

An Automatic Plant Watering System is a smart irrigation solution that supplies water to plants based on soil moisture levels. The system uses a soil moisture sensor to monitor soil condition and automatically activates a water pump through a relay module when the soil becomes dry. This ensures optimal watering without manual intervention and prevents overwatering.

---

## 3. Objective  

To design and simulate an automated irrigation system that maintains proper soil moisture levels by automatically controlling a water pump using sensor-based decision making.

---

## 4. Equipment / Components Required  

| No. | Component                     | Quantity    |
| --- | ----------------------------- | ----------- |
| 1   | Arduino UNO                   | 1           |
| 2   | Soil Moisture Sensor Module   | 1           |
| 3   | Relay Module (5V)             | 1           |
| 4   | DC Water Pump                 | 1           |
| 5   | Jumper Wires                  | As required |
| 6   | Breadboard (optional)         | 1           |
| 7   | External Power Supply (Pump)  | 1           |
| 8   | USB / Power Source (Arduino)  | 1           |

---

## 5. Working Principle  

The soil moisture sensor continuously measures the water content present in the soil. The sensor outputs an analog signal corresponding to the moisture level. The Arduino reads this value and compares it with a predefined threshold.

- When the soil is **dry**, the Arduino activates the relay module, which turns ON the water pump.
- When the soil is **sufficiently moist**, the relay is turned OFF, stopping the pump.

This automated process ensures efficient water usage and healthy plant growth.

---

## 6. Circuit Connections  

### Soil Moisture Sensor  

| Sensor Pin | Arduino Pin |
| ---------- | ----------- |
| VCC        | 5V          |
| GND        | GND         |
| AO         | A0          |

### Relay Module  

| Relay Pin | Arduino Pin |
| --------- | ----------- |
| VCC       | 5V          |
| GND       | GND         |
| IN        | Digital Pin 7 |

### Water Pump  

- Pump positive terminal → Relay NO (Normally Open)  
- Pump negative terminal → External power supply GND  

> **Note:** The water pump should be powered using an external power source to avoid damage to the Arduino board.

---

## 7. Arduino Program  

```cpp
const int soilPin = A0;
const int relayPin = 7;

int soilValue;
int threshold = 500;   // Adjust based on soil and sensor calibration

void setup() {
  pinMode(relayPin, OUTPUT);
  digitalWrite(relayPin, HIGH); // Relay OFF (active LOW)
  Serial.begin(9600);
}

void loop() {
  soilValue = analogRead(soilPin);
  Serial.println(soilValue);

  if (soilValue > threshold) {
    digitalWrite(relayPin, LOW);   // Pump ON
  } else {
    digitalWrite(relayPin, HIGH);  // Pump OFF
  }

  delay(1000);
}

```