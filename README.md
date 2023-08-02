# Final-Year-Project
Charging Electrical Vehicle using PV System 
#include<LiquidCrystal.h>

LiquidCrystal lcd(12,11,6,5,4,3);

int abc=0;

float vol=0.0;

double freq=70000.0;

double duty=50.0;

float sensorvalue=0;

void setup() {
   
  // put your setup code here, to run once:
  
  
  pinMode(9,OUTPUT);
  
  pinMode(2,OUTPUT);
 
 pinMode(8,OUTPUT);
 
 pinMode(10,OUTPUT);
 
 lcd.begin(16,2);
 
 Serial.begin(9400);
  
lcd.setCursor(1,0);

 lcd.print("Solar Charger");
  
TCCR1A=_BV(COM1A1);
TCCR1B=_BV(WGM13) | _BV(CS10);
}

void loop(){
  
sensorvalue=analogRead(A2);

   if(sensorvalue>400){

  digitalWrite(2,HIGH);

  digitalWrite(10,LOW);

  digitalWrite(8,HIGH);
  
 }
    else

    {
     
 digitalWrite(8,LOW);
        
digitalWrite(2,LOW);
        
digitalWrite(10,HIGH);
    }
  
  // put your main code here, to run repeatedly:
 
 volt=5.0*(analogRead(A0)/1023.0)*(7.5/5);

  delay(200);   

  /* 
sensorvalue=analogRead(A2);

   if(sensorvalue>3){

  digitalWrite(2,LOW);

  digitalWrite(8,HIGH);
  
 }
    else
    {
      
digitalWrite(8,LOW);

        digitalWrite(2,HIGH);
    }

//delay(5000);   

*/ 

//  FWM(freq, duty);

  lcd.setCursor(2,1);

  lcd.print(volt);

  lcd.setCursor(7,1);

  lcd.print("Volts");

  /*
if(volt<4.5){

 duty=duty+1.0;

}

if(volt>5.2){ 
 
 duty=duty-1.0;
                      }
                      */
}

void FWM(float freq, float duty){
  
ICR1=16000000.0/(2.0*freq);
  
OCR1A=ICR1*(duty/100.0);
}
