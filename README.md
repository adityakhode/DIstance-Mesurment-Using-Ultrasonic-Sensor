/*# DIstance-Mesurment-Using-Ultrasonic-Sensor*/
#include <LiquidCrystal.h>
 
#define trigger 9
#define echo 8
#define buzzerPin 7
#define X 6

LiquidCrystal lcd(12,11,5,4,3,2);
 
float time=0,distance=0;
 
void setup()
{
    Serial.begin(9600);
    lcd.begin(16,2);
    pinMode(trigger,OUTPUT);
    pinMode(echo,INPUT);
    lcd.print(" Ultra sonic");
    lcd.setCursor(0,1);
    lcd.print("Distance Meter");
    delay(2000);
    lcd.clear();
    lcd.print(" ");
    delay(2000);
    pinMode(7,OUTPUT);
    Serial.begin(9600);
}
 
void loop()
{
    lcd.clear();
    digitalWrite(trigger,LOW);
    delayMicroseconds(2);
    digitalWrite(trigger,HIGH);
    delayMicroseconds(2);
    digitalWrite(trigger,LOW);
    delayMicroseconds(2);
    time=pulseIn(echo,HIGH);
    distance=time*340/20000;
    Serial.println(distance);
    lcd.clear();
    lcd.print("Distance:");
    lcd.print(distance);
    lcd.print("cm");
    delay(10);
 /*Buzzer Function*/
    if(distance<=20)
    {
        digitalWrite(buzzerPin,HIGH);
        lcd.setCursor(0,1);
        lcd.print("    Warning!!");
        digitalWrite(6,HIGH);
        delay(100);
    }
    else
    {
        digitalWrite(buzzerPin,LOW);
        lcd.setCursor(0,1);
        lcd.print("      Safe");
        delay(50);
    } 
}
