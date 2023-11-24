Outputs :-
CODE :-#define BLYNK_TEMPLATE_ID "TMPL3wpFP3MEc"
#define BLYNK_TEMPLATE_NAME "medicine reminder"
#define BLYNK_AUTH_TOKEN "zBneVJLkNr4pI6J3mKTwEQEGImWETtuP"

#define BLYNK_PRINT Serial
#include <WiFi.h>
#include <BlynkSimpleEsp32.h>

const int soundSensorPin = A0;
const int motionSensorPin = 2;

char auth[] = BLYNK_AUTH_TOKEN;
char ssid[] = "Redmi Note 10S";
char pass[] = "12345678";

BlynkTimer timer;
int soundFlag = 0;
int motionFlag = 0;

void sendSoundSensor() {
  int soundValue = analogRead(soundSensorPin);
  Serial.print("Sound sensor value: ");
  Serial.println(soundValue);

  int soundThreshold = 500;  // Adjust as needed

  if (soundValue > soundThreshold && soundFlag == 0) {
    Serial.println("Sound detected!");
    
    soundFlag = 1;
  } else if (soundValue <= soundThreshold) {
    Serial.println("No sound detected");
    soundFlag = 0;
  }
}

void sendMotionSensor() {
  int motionValue = digitalRead(motionSensorPin);

  if (motionValue == HIGH && motionFlag == 0) {
    Serial.println("Motion detected!");
    Blynk.logEvent("motion_alert", "Motion Detected");
    motionFlag = 1;
    Blynk.logEvent("medicine_reminder");
  } else if (motionValue == LOW) {
    Serial.println("No motion detected");
    motionFlag = 0;
  }
}

void setup() {
  pinMode(soundSensorPin, INPUT);
  pinMode(motionSensorPin, INPUT);

  Serial.begin(115200);
  Blynk.begin(auth, ssid, pass);

  timer.setInterval(5000L, sendSoundSensor);  // Adjust the interval as needed
  timer.setInterval(5000L, sendMotionSensor); // Adjust the interval as needed
}

void loop() {
  Blynk.run();
  timer.run();
}


![WhatsApp Image 2023-11-23 at 10 21 27 PM](https://github.com/sujanyashetty/Output/assets/149661923/7cfcf479-9cad-4020-a633-191ccb3b4dd8)
![WhatsApp Image 2023-11-24 at 4 46 46 AM](https://github.com/sujanyashetty/Output/assets/149661923/f23320c8-4f07-4049-87a5-419a3b72cdc7)
![WhatsApp Image 2023-11-23 at 9 40 19 PM](https://github.com/sujanyashetty/Output/assets/149661923/3a372c1d-c8a8-410d-b2e7-748e3a0f14b1)
![WhatsApp Image 2023-11-23 at 9 44 21 PM](https://github.com/sujanyashetty/Output/assets/149661923/823492e4-8f0c-47b9-b32a-a988e5d73f2d)


https://github.com/sujanyashetty/Output/assets/149661923/bdef51b5-aa06-455f-9ee8-5c9dbe6add1b

