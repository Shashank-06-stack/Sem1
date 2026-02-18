                     ------------BRIEF DESCRIPTION ABOUT WASTE SORTING BIN----------------
                     PROJECT DESCRIPTION

This project presents an automatic bin sorting system that separates waste into wet and dry categories using sensors and a servo mechanism. The system is designed to reduce manual waste segregation and promote smart waste management.

An ultrasonic sensor is used to detect the presence of an object near the bin. Once an object is detected, the system pauses and waits until the object comes in contact with a capacitive moisture sensor. Based on the moisture content of the object, the Arduino classifies it as wet or dry waste.

A servo motor then rotates to a predefined angle to direct the waste into the appropriate bin. After sorting, the servo returns to its neutral position, and the system resets to handle the next object. The entire setup is powered using a 5V power bank, making it portable and energy efficient.

This project demonstrates the application of embedded systems, sensors, and automation in smart waste management.

🎯 KEY FEATURES

-Automatic wet and dry waste segregation
-Contact-based moisture detection for accuracy
-Servo-based mechanical sorting
-Portable power-bank operation
-Low-cost and easy to implement

🌍 APPLICATIONS

-Smart dustbins
-Waste management systems
-Public places and institutions
-Smart city projects
-Educational mini-projects


#include <Servo.h>

// ---------------- PINS ----------------
#define TRIG_PIN 9
#define ECHO_PIN 8
#define MOISTURE_PIN A0
#define SERVO_PIN 10

// ---------------- OBJECTS ----------------
Servo sorterServo;

// ---------------- MOISTURE CALIBRATION ----------------
int dryValue = 450;
int wetValue = 250;
int threshold;

// ---------------- VARIABLES ----------------
long duration;
int distance;
int moisture;

// ---------------- STATES ----------------
bool objectDetected = false;
bool sortingDone = false;

void setup() {
  Serial.begin(9600);

  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);

  sorterServo.attach(SERVO_PIN);
  sorterServo.write(45);   // neutral

  threshold = (dryValue + wetValue) / 2;

  Serial.println("SYSTEM READY – WAITING FOR OBJECT");
}

void loop() {

  // ================= STEP 1: WAIT FOR OBJECT =================
  if (!objectDetected) {

    digitalWrite(TRIG_PIN, LOW);
    delayMicroseconds(2);
    digitalWrite(TRIG_PIN, HIGH);
    delayMicroseconds(10);
    digitalWrite(TRIG_PIN, LOW);

    duration = pulseIn(ECHO_PIN, HIGH, 30000);
    distance = duration * 0.034 / 2;

    Serial.print("Distance: ");
    Serial.println(distance);

    if (distance > 0 && distance <= 10) {
      objectDetected = true;   // LOCK ultrasonic
      Serial.println("Object detected → waiting for moisture contact");
      delay(500);
    }

    return;  // 🔴 STOP HERE (ultrasonic waits)
  }

  // ================= STEP 2: WAIT FOR MOISTURE =================
  if (!sortingDone) {

    moisture = analogRead(MOISTURE_PIN);
    Serial.print("Moisture reading: ");
    Serial.println(moisture);

    // wait until sensor touches object
    if (moisture >= wetValue && moisture <= dryValue) {

      if (moisture > threshold) {
        Serial.println("DRY OBJECT → DRY BIN");
        sorterServo.write(0);
      } else {
        Serial.println("WET OBJECT → WET BIN");
        sorterServo.write(90);
      }

      sortingDone = true;
      delay(2000);

      sorterServo.write(45);   // neutral
      delay(1500);

      Serial.println("SORTING DONE");
    }

    return;  // 🔴 STOP HERE (waits for moisture)
  }

  // ================= STEP 3: RESET SYSTEM =================
  objectDetected = false;
  sortingDone = false;
  Serial.println("SYSTEM RESET – WAITING FOR NEXT OBJECT");
  delay(1000);
}
