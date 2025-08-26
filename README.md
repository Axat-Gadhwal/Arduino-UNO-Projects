
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












