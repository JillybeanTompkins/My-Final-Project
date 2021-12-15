//# My-Final-Project
//My final project for Creative Coding II. I based it off of these: https://www.etechnophiles.com/5-arduino-ultrasonic-sensor-projects-with-code-circuit-diagram-and-more/ and, https://www.hackster.io/christian-madlansacay/nano-piano-8da96d

/* 
Name: Jillian Tompkins
NMD 211 Lab 13
Assignment / Question: Final Project
Date: 12/15/2021
*/

  #define echo 2
  #define trig 3
  #define outA 8// yellow LED
  #define outB 9// blue LED
  #define outC 10// Buzzer
  
  float  duration;
  float  distance;
  const int intruderDistance = 10;

  void setup() {
    pinMode(act, OUTPUT);
    pinMode(echo, INPUT);
    pinMode(outA, OUTPUT);
    digitalWrite(outA, LOW);
    pinMode(outB, OUTPUT);
    digitalWrite(outB, LOW);
    pinMode(outC, OUTPUT);
    digitalWrite(outC, LOW);
    Serial.begin(9600);
  }
  
  void loop() {
    time_Measurement();
    distance = (float)duration * (0.0343) / 2;
    Serial.println(distance);
    alarm_condition(); 
  }
  
  void time_Measurement()
  { digitalWrite(act, LOW);
    delayMicroseconds(2);
    digitalWrite(act, HIGH);
    delayMicroseconds(10);
    digitalWrite(act, LOW);
    duration = pulseIn(echo, HIGH);
  }

  void alarm_condition()
  { if(distance<=intruderDistance)
    { digitalWrite(outA,HIGH);
      digitalWrite(outB,LOW);
      analogWrite(outC,20000);}
    else
    {  digitalWrite(outA,LOW);
       digitalWrite(outB,HIGH);
       analogWrite(outC,0);
       }
  }
