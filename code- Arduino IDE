#include <Wire.h>
#include <LiquidCrystal_I2C.h>

const int piezoPin = A0;
const int threshold = 50; // Lowered for testing
int prev = 0, stepCount = 0;
unsigned long previousMillis = 0;
const long interval = 1000;

float vout, vin = 5.0;

LiquidCrystal_I2C lcd(0x27, 16, 2);

void setup() {
  Serial.begin(9600); // Added for debugging
  lcd.init();
  lcd.backlight();
  lcd.print("Footstep Energy");
  lcd.setCursor(3, 1);
  lcd.print("Generator");
  delay(1500);
  lcd.clear(); 
  lcd.setCursor(0, 0);
  lcd.print("Steps: 0");
  lcd.setCursor(0, 1);
  lcd.print("Voltage: 0V");
}

void loop() {
  unsigned long currentMillis = millis();
  int sensorValue = analogRead(piezoPin);
  Serial.println(sensorValue); // Print raw values for debugging

  if (currentMillis - previousMillis >= interval) {
    previousMillis = currentMillis;

    if (sensorValue > threshold && prev == 0) {
      stepCount++;
      lcd.setCursor(7, 0);
      lcd.print(stepCount);

      vout = (sensorValue * vin) / 1023.0;
      lcd.setCursor(9, 1);
      lcd.print("    "); // Clear previous voltage
      lcd.setCursor(9, 1);
      lcd.print(vout, 1);
      lcd.print("V");

      prev = 1;
    } else {
      prev = 0;
    }
  }
}
