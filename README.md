# arduino-temp-lcd
This project uses an Arduino and temperature sensor (like TMP36) to measure real-time temperature and display it on a 16x2 LCD. It demonstrates analog data reading, processing, and output using embedded system design.
#include <LiquidCrystal.h>

// Initialize LCD pins: RS, E, D4, D5, D6, D7
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

// TMP36 sensor connected to A0
int sensorPin = A0;

void setup() {
  lcd.begin(16, 2);   // 16x2 LCD
  lcd.print("Temperature");
  delay(2000);
  lcd.clear();
}

void loop() {

  int reading = analogRead(sensorPin);

  // Convert analog reading to voltage
  float voltage = reading * (5.0 / 1023.0);

  // TMP36 temperature formula
  float temperatureC = (voltage - 0.5) * 100;

  lcd.setCursor(0, 0);
  lcd.print("Temperature:");

  lcd.setCursor(0, 1);
  lcd.print(temperatureC);
  lcd.print((char)223); // Degree symbol
  lcd.print("C    ");

  delay(1000);
}
