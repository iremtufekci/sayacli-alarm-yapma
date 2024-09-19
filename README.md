# sayacli-alarm-yapma
#include <LiquidCrystal.h>
#include <virtuabotixRTC.h>


int clk = 6;
int data = 7;
int reset = 8;
virtuabotixRTC myRTC(clk, data, reset);
int buzzer=1;

int rs = 12, en = 11, d4 = 5, d5 = 4, d6 = 3, d7 = 2;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);

void setup() {
  lcd.begin(16, 2); 
  pinMode(buzzer,OUTPUT);

}

void loop() {
  myRTC.updateTime();  

  
  static int previousSecond = -1;
  if (myRTC.seconds != previousSecond) {
    previousSecond = myRTC.seconds;  
    lcd.clear(); 


    lcd.setCursor(0, 0); 
    lcd.print("Tarih:12/09/2024 ");
  

    
    lcd.setCursor(0, 1); 
    lcd.print("Sayac: ");
    if (myRTC.hours < 10) lcd.print("0");
    lcd.print(myRTC.hours);
    lcd.print(":");
    if (myRTC.minutes < 10) lcd.print("0");
    lcd.print(myRTC.minutes);
    lcd.print(":");
    if (myRTC.seconds < 10) lcd.print("0");
    lcd.print(myRTC.seconds);
  }

 
  delay(500);
  if(myRTC.minutes>17){
    digitalWrite(buzzer,HIGH);
  }
  else{
    digitalWrite(buzzer,LOW);
  }
}
