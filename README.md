📌 PROJECT TITLE

Automatic Wet and Dry Waste Bin Sorting System Using Arduino

📝 1. INTRODUCTION

Waste segregation is a major challenge in modern waste management systems. Mixing wet and dry waste leads to environmental pollution, difficulty in recycling, and health hazards. Manual segregation is time-consuming, unhygienic, and inefficient.

This project focuses on designing and implementing an automatic waste sorting system that separates wet and dry waste using sensors and automation. The system uses an Arduino microcontroller, an ultrasonic sensor for object detection, a capacitive moisture sensor for waste classification, and a servo motor for mechanical sorting. The system is powered using a 5V power bank, making it portable and safe.

🎯 2. OBJECTIVES OF THE PROJECT

-To automatically detect waste without human intervention
-To classify waste as wet or dry based on moisture content
-To mechanically direct waste into the correct bin
-To reduce manual effort and improve hygiene
-To design a low-cost, energy-efficient system

🧠 3. WORKING PRINCIPLE

-The system works in three main stages:
-Stage 1: Object Detection
-An ultrasonic sensor continuously measures the distance in front of the bin.
-When an object comes within a preset range (e.g., 10 cm), the system confirms the presence of waste and locks the ultrasonic sensor to prevent repeated triggering.

Stage 2: Moisture Detection

-After object detection, the system waits until the waste touches the capacitive moisture sensor.
  The moisture sensor measures the moisture content:
    -High sensor value → Dry waste
    -Low sensor value → Wet waste
       -his waiting logic ensures accurate classification and avoids false readings.

Stage 3: Waste Sorting

Based on the moisture sensor reading:

-If waste is dry, the servo rotates to the dry bin angle
-If waste is wet, the servo rotates to the wet bin angle
-After sorting, the servo returns to a neutral position, and the system resets to wait for the next object.

🔩 4. HARDWARE COMPONENTS USED
4.1 Arduino (Microcontroller)
  Acts as the brain of the system
  Reads sensor data
  Controls servo movement
  Implements decision-making logic

4.2 Ultrasonic Sensor (HC-SR04)

  Detects the presence of waste
  Uses sound waves to measure distance
  Helps in triggering the sorting process only when waste is present

4.3 Capacitive Moisture Sensor

  Detects moisture content in waste
  More durable than resistive sensors
  Used to classify waste as wet or dry

4.4 Servo Motor

  Controls the mechanical sorting mechanism
  Rotates to predefined angles for wet and dry bins
  Provides accurate and controlled movement

4.5 Power Bank (5V Supply)

  Powers the Arduino and servo
  Provides sufficient current for servo operation
  Makes the system portable and safe

🔌 5. POWER SUPPLY CONCEPT

-The power bank provides 5V to the system
-Servo motor is powered directly from the power bank
-All grounds are connected together (common ground)
-This prevents voltage drop and servo jitter

🧮 6. SOFTWARE LOGIC / ALGORITHM

-Start system
-Initialize sensors and servo
-Continuously check ultrasonic sensor
-If object detected → stop ultrasonic sensing
-Wait until moisture sensor detects valid reading
-Compare moisture value with threshold
-Rotate servo to wet or dry bin
-Return servo to neutral position
-Reset system
-Repeat process

📊 7. CALIBRATION DETAILS

Moisture Sensor Calibration
 -Dry waste value ≈ 800–900
 -Wet waste value ≈ 300–400
 -Threshold = average of dry and wet values

Servo Calibration

0° → Dry bin
90° → Wet bin
180° → Neutral position

🌍 8. APPLICATIONS

-Smart dustbins
-Waste segregation systems
-Smart city projects
-Public places (malls, schools, offices)
-Educational and mini projects

✅ 9. ADVANTAGES

-Automatic and hygienic
-Reduces human involvement
-Low cost and simple design
-Portable due to power bank usage
-Easy to upgrade and modify

🏁 10. CONCLUSION

The Automatic Wet and Dry Waste Bin Sorting System successfully demonstrates how embedded systems and sensors can be used to automate waste management. By combining ultrasonic detection, moisture sensing, and servo-based actuation, the system provides an effective solution for waste segregation. This project highlights the importance of automation in maintaining cleanliness and supports the vision of smart and sustainable cities.
