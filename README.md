
# Project 1 : Smart Maths City

## Weather Station 

### Codes

      #include <LiquidCrystal.h>
      #include <DHT.h>
      
      #define DHTPIN 7
      #define DHTTYPE DHT22
      DHT dht(DHTPIN, DHTTYPE);
      
      // Initialize the LCD library with the numbers of the interface pins
      LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
      
      const int ledPin = 8;
      
      void setup() {
        lcd.begin(16, 2);
        dht.begin();
        pinMode(ledPin, OUTPUT);
      
        lcd.print("Weather Station");
        delay(2000);
        lcd.clear();
      }
      
      void loop() {
        float humidity = dht.readHumidity();
        float temperature = dht.readTemperature();
      
        if (isnan(humidity) || isnan(temperature)) {
          lcd.clear();
          lcd.print("Sensor error");
          delay(2000);
          return;
        }
      
        float probability = calculateProbability(humidity);
      
        // Display temperature and humidity
        lcd.setCursor(0, 0);
        lcd.print("T:");
        lcd.print(temperature, 1);
        lcd.print("C H:");
        lcd.print(humidity, 0);
        lcd.print("%   ");
      
        // Display rain probability
        lcd.setCursor(0, 1);
        lcd.print("RainProb:");
        lcd.print(probability, 1);
        lcd.print("% ");
      
        // Blink LED if probability > 50%
        if (probability > 50.0) {
          digitalWrite(ledPin, HIGH);
          delay(500);
          digitalWrite(ledPin, LOW);
          delay(500);
        } else {
          digitalWrite(ledPin, LOW);
        }
      
        lcd.clear();
      }
      
      // Simple rain probability calculation based on humidity only
      float calculateProbability(float humidity) {
        if (humidity > 80) {
          return 80.0;
        }
        else if (humidity > 60) {
          return 50.0;
        }
        else {
          return 10.0;
        }
      }


### Pin Mapping

<img width="514" height="461" alt="Screenshot 2025-08-26 184249" src="https://github.com/user-attachments/assets/0f5ac37f-91ed-4652-9158-de4d4a06dd46" />

Pin Connections Summary


#### Component	Arduino Pin


##### DHT22 sensor

Pin 1 (VCC): Connect to +5V or +3.3V on Arduino

Pin 2 (Data): Connect to Arduino digital input pin (e.g., pin 7)

Pin 3 (NC): Leave unconnected or check your specific module datasheet

Pin 4 (GND): Connect to Arduino ground (GND   

## Links

https://wokwi.com/projects/440359752595341313
 
## Traffic Light and Street Lights

<img width="842" height="653" alt="image" src="https://github.com/user-attachments/assets/e1eeb45b-59ea-435b-8f0b-5f7f79600c88" />


### Link

https://wokwi.com/projects/440350426734654465

# Resistor Info

Here’s a quick parts count (with typical resistor values) for your setup:

### Traffic lights (R–Y–G)

* **3 LEDs ⇒ 3 resistors**

  * **220 Ω** each (one in series with each LED)

### Street lights (you said 5 LEDs)

* **5 LEDs ⇒ 5 resistors**

  * **220 Ω** each (one per LED)

### LDR / light sensing

* If you use a **4-pin LDR module** (VCC, GND, AO, DO): **0 extra resistors** (it has its own divider onboard).
* If you use a **bare LDR**: **1 resistor** for the voltage divider (typically **10 kΩ** to GND, LDR to 5 V, junction to analog pin).

### “Weather tower” (no LCD)

Assuming simple LED indicators (e.g., Sunny/Cloudy/Rain or an RGB LED):

* **Three separate LEDs**: **3 × 220 Ω** (one per LED), **total 3 resistors**.
* **OR one RGB LED** (common cathode/anode): **3 × 220 Ω** (one per color).

### Buzzer, ultrasonic, DHT/rain modules

* **Active buzzer**: usually **no resistor needed** (optional \~**100 Ω** in series if you want to soften volume).
* **HC-SR04 ultrasonic**: **no resistors**.
* **DHT11/DHT22** and **rain sensor module**: modules typically **no external resistor** needed (bare DHT sometimes uses a 10 kΩ pull-up, but not on breakout boards).

---

## Totals for your current build

* Traffic (3) + Street (5) LEDs = **8 × 220 Ω**
* LDR: **0** (module) **or** **1 × 10 kΩ** (bare LDR)
* Weather tower (example with 3 status LEDs): **+3 × 220 Ω** (or 3 for an RGB)

So, typical total = **11 × 220 Ω** (+**1 × 10 kΩ** only if using a bare LDR).

---

# More Projects

## 1) Ultrasonic Parking Assistant

### Components

* Arduino UNO
* HC-SR04 ultrasonic sensor
* 3 LEDs (green, yellow, red)
* 3 × 220 Ω resistors
* Buzzer (active)

### What it does

Measures distance to an obstacle and gives visual/audio feedback:

* **Green LED**: safe distance
* **Yellow LED**: getting close
* **Red LED + buzzer**: too close

### Wokwi starter link

https://wokwi.com/projects/new/arduino-uno

---

## 2) Automatic Plant Watering Alert

### Components

* Arduino UNO
* Soil moisture sensor module
* 16x2 LCD (optional)
* 1 LED + 220 Ω resistor
* Buzzer

### What it does

Reads soil moisture and alerts when soil is dry:

* LED turns ON when moisture falls below threshold
* Buzzer beeps for dry soil
* Optional LCD displays moisture percentage

### Wokwi starter link

https://wokwi.com/projects/new/arduino-uno

---

## 3) PIR Motion Security Light

### Components

* Arduino UNO
* PIR motion sensor (HC-SR501)
* Relay module or LED lamp simulation
* 1 LED + 220 Ω resistor (status)

### What it does

Detects movement and turns on light for a fixed duration:

* Motion detected → light ON for 10–20 seconds
* No motion → light OFF
* Great for home/garage security demo

### Wokwi starter link

https://wokwi.com/projects/new/arduino-uno

---

## 4) Smart Dustbin (Servo + Ultrasonic)

### Components

* Arduino UNO
* HC-SR04 ultrasonic sensor
* Servo motor (SG90)
* Optional buzzer/LED status

### What it does

When hand comes near bin lid, servo opens the lid automatically:

* Distance < threshold → servo opens lid
* After delay → servo closes lid

### Wokwi starter link

https://wokwi.com/projects/new/arduino-uno










