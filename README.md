# Temperature-and-humidity-monitoring-system
🌡️ Temperature & Humidity Monitoring System

Arduino UNO | DHT11 Sensor | 16×2 I2C LCD | Real-Time Display


---

📝 1. Project Description

This project is a real-time Temperature and Humidity Monitoring System made using Arduino UNO, DHT11 sensor, and a 16×2 I2C LCD.
The sensor reads environmental temperature and humidity, the Arduino processes the data, and the values are displayed on the LCD screen continuously.
It is simple, reliable, and ideal for learning sensor interfacing and microcontroller programming.


---

🎯 2. Project Objectives

Measure temperature continuously

Measure humidity continuously

Display the values clearly on an LCD

Understand sensor + Arduino interfacing

Build a low-cost monitoring system



---

🔧 3. Components Used — Detailed Explanation

1️⃣ Arduino UNO

Arduino UNO is a microcontroller board based on ATmega328P.

Why it is used?

Acts as the brain of the system

Reads data from DHT11

Processes and displays values on LCD

Very easy for beginners



---

2️⃣ DHT11 Temperature & Humidity Sensor

A digital sensor that gives both temperature and humidity readings.

Why it is used?

Simple digital output

Very easy to interface

Accurate basic readings


Specifications

Temperature range: 0–50°C

Humidity range: 20–90%

1-second sampling rate



---

3️⃣ 16×2 I2C LCD Display

A 16×2 character LCD with an I2C module attached to reduce wiring.

Why I2C?

Normal LCD needs 16 wires

I2C LCD needs only 4 wires

Makes the setup neat and clean


Job

Shows temperature readings

Shows humidity readings

Backlight makes it readable anytime



---

4️⃣ Jumper Wires

Used to connect Arduino, LCD, and DHT11 directly.

Why needed?

No soldering

Flexible

Easy to connect and remove



---

🔌 4. Circuit Wiring (Without Breadboard)

👉 All components are connected directly using jumper wires.


---

🔹 DHT11 Sensor → Arduino UNO

DHT11 Pin	Arduino Pin

VCC	5V
GND	GND
DATA	D2



---

🔹 I2C LCD → Arduino UNO

LCD Pin	Arduino Pin

VCC	5V
GND	GND
SDA	A4
SCL	A5



---

⚙️ 5. Working of the Project

1. DHT11 sensor reads temperature and humidity.


2. It sends data to Arduino via the data pin.


3. Arduino processes the incoming readings.


4. Using I2C communication, Arduino sends the values to the LCD.


5. LCD displays:

Temperature in °C

Humidity in %



6. Readings refresh every 1 second.




🏆6.Applications

Home environment monitoring

Weather stations

Smart farming

Greenhouse monitoring

IoT-based temperature systems

Industrial humidity control



---

⭐ 7. Advantages

Simple and low-cost

No breadboard needed

Only 4 wires for LCD

Easy for beginners

Real-time monitoring

Portable and clean setup



---

⚠️ 8. Limitations

DHT11 has limited accuracy

Suitable only for normal indoor environments

Slow sampling rate



---

📌 9. Conclusion

The Temperature & Humidity Monitoring System is a simple and effective project for understanding sensor data processing, Arduino programming, and I2C communication.
It is easy to build, uses fewer wires, and can be upgraded to an IoT-enabled system in the future.



Arduino code
#include "DHT.h"
#include <LiquidCrystal_I2C.h>

// Define pin and sensor type
#define DHTPIN 2
#define DHTTYPE DHT11 // Change to DHT11 if using DHT11

DHT dht(DHTPIN, DHTTYPE);
// Format => (ADDRESS,Width,Height )
LiquidCrystal_I2C lcd(0x27, 16, 2);

void setup() {
  Serial.begin(9600); //Start serial monitor
  dht.begin();       // Initialize DHT sensor
  //Initialize the lcd
  lcd.init();
  // Turn on the Backlight
  lcd.backlight();
  lcd.setCursor(0,0);
}
void loop(){
  // Wait a few seconds between measurements
  delay(2000);

  // Read humidity and temperature
  float humidity = dht.readHumidity();
  float temperature = dht.readTemperature(); // Celsius
  float temperatureF = dht.readTemperature(true); // Fahrenheit

  // Check if any reading failed
  if (isnan(humidity) || isnan(temperature)) {
    Serial.println("Failed to read from DHT sensor!");
    return;
  }

  lcd.backlight();
  lcd.setCursor(0,0);
  lcd.print("Humidity=");
  lcd.setCursor(9,0);
  lcd.print(humidity);
  lcd.setCursor(15,0);
  lcd.print("% ");
  lcd.setCursor(0,1);
  lcd.print("Temp = ");
  lcd.setCursor(8,1);
  lcd.print(temperature);
  lcd.setCursor(13,1);
  lcd.println("C ");
}
