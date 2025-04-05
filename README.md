# arduino.boomb
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

// Inisialisasi LCD
LiquidCrystal_I2C lcd(0x27, 16, 2);
//inisialisasi LED dengan nomor pin
int red = 2;
int blue = 3;
//setup pengaturan pin dan lcd
void setup() {
  pinMode(red, OUTPUT);
  pinMode(blue, OUTPUT);
  // Inisialisasi LCD
  lcd.init();
  lcd.setBacklight(1);

}
void loop() {
  lcd.setCursor(0,0);
  lcd.print("Hitungan mundur");
  delay(2000);
  lcd.clear();
  digitalWrite(red, LOW);
  digitalWrite(blue, LOW);
  //looping untuk menghitung mundur
  for(int i = 10;i <= 10;i--){
    if(i > 0){//jika belum 0, maka akan menghitung mundur
      lcd.setCursor(0,0);
      lcd.print(i);
      delay(500);
      lcd.clear();
    }else{//ketika 0 maka akan BOOOOOMM!
      lcd.print("BOOOOOMM!");
      delay(1000);
      lcd.clear();
      digitalWrite(red, HIGH);
      delay(1000);
      digitalWrite(blue, HIGH);
      delay(1000);
    }
  }
}
