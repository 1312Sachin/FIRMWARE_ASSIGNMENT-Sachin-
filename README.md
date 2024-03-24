# FIRMWARE_ASSIGNMENT-Sachin-

#include <TimerOne.h>
const int sensorPin = A0; 
const int ledPin = 13;    
volatile bool ledState = false;

void setup() {
  pinMode(ledPin, OUTPUT);          
  Timer1.initialize(250000);        
  Timer1.attachInterrupt(toggleLed); 
}

void loop() {
  int sensorValue = analogRead(sensorPin);         
  float voltage = sensorValue * 5.0 / 1023;           
  float temperature = voltage * 100;                  

  if (temperature < 30) {
    Timer1.setPeriod(250000);                         
  } else {
    Timer1.setPeriod(500000);                          
  }
}


void toggleLed() {
  ledState = !ledState;                                
  digitalWrite(ledPin, ledState);                     
}
