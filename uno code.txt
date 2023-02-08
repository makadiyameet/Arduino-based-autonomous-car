#include<HCSR04.h>

UltraSonicDistanceSensor ultrasonic(A3,A4);
float distance;

// For Left Motor
int LMspeedpin = 5;
int LMforwardpin = 6;
int LMbackwardpin = 7;

//For Right Motor
int RMspeedpin = 8;
int RMforwardpin = 12;
int RMbackwardpin =13;

void setup() {
 
 pinMode(LMspeedpin, OUTPUT);
 pinMode(LMforwardpin, OUTPUT);
 pinMode(LMbackwardpin, OUTPUT);
 pinMode(RMspeedpin, OUTPUT);
 pinMode(RMforwardpin, OUTPUT);
 pinMode(RMbackwardpin, OUTPUT);

 Serial.begin(9600);

 digitalWrite(LMspeedpin, HIGH);
 digitalWrite(RMspeedpin, HIGH);

}

void loop() {

   distance = ultrasonic.measureDistanceCm();
   Serial.println(distance);

   if (distance > -1 && distance <25)
   {
     stop();
     delay(800);
     Gobackward();
     delay(500);
     stop();
     delay(800);

      if(random(0,2) == 0)
      {
        Goleft();        
      }
      else
      {
        Goright();
      }

      delay(400);
      stop();
      delay(600);
   }
   else
   {
     Goforward();
   }
    
}

void Goforward()
{
  digitalWrite(LMforwardpin, HIGH);
  digitalWrite(LMbackwardpin, LOW);
  digitalWrite(RMforwardpin, HIGH);
  digitalWrite(RMbackwardpin, LOW);
}

void Gobackward()
{
  digitalWrite(LMforwardpin, LOW);
  digitalWrite(LMbackwardpin, HIGH);
  digitalWrite(RMforwardpin, LOW);
  digitalWrite(RMbackwardpin, HIGH);
}

void stop()
{
  digitalWrite(LMforwardpin, LOW);
  digitalWrite(LMbackwardpin, LOW);
  digitalWrite(RMforwardpin, LOW);
  digitalWrite(RMbackwardpin, LOW);
}

void Goright()
{
  digitalWrite(LMforwardpin, HIGH);
  digitalWrite(LMbackwardpin, LOW);
  digitalWrite(RMforwardpin, LOW);
  digitalWrite(RMbackwardpin, LOW);
}

void Goleft()
{
  digitalWrite(LMforwardpin, LOW);
  digitalWrite(LMbackwardpin, LOW);
  digitalWrite(RMforwardpin, HIGH);
  digitalWrite(RMbackwardpin, LOW);
}
