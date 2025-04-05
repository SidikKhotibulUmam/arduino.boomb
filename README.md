PROJEK MEMBUAT BOM DETONATOR DENGAN ARDUINO

Cara Kerja:
1.Monitor akan menghitung mundur dari 10-1
2.Ketika angka sudah 0, maka monitor akan menampilkan BOOOOMM!
3.LED akan menyala, menandakan bom meledak

Komponen:
1.Arduino
2.LCD I2C
3.Breadboard
4.LED

Skematik:
1.PIN GND  arduino dipasangkan ke pin (-) breadboard
2.PIN 5v arduino dipasangkan ke pin (+) breadboard
3.PIN GND dan VCC LCD I2C dipasangkan ke pin (-) dan (+) breadboard
4.PIN SDA dan SCL LCD I2C dipasangkan ke pin SDA dan SCL arduino
5.Kaki negatif LED dipasangkan ke pin (-) breadboard
6.Kaki positif LED dipasangkan dahulu dengan transistor sebelum dipasangkan ke pin (+) breadboard

Kode:
//inisialisasi library 
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

// Inisialisasi LCD
LiquidCrystal_I2C lcd(0x27, 16, 2);
//inisialisasi LED dengan nomor pin
int red = 2;
int blue = 3;
//setup pengaturan led dan lcd
void setup() {
  pinMode(red, OUTPUT);
  pinMode(blue, OUTPUT);
  // Inisialisasi LCD
  lcd.init();
  lcd.setBacklight(1);

}
void loop() {
  lcd.setCursor(0,0); //posisi baris pertama,kolom pertama (atas paling pojok kiri)
  lcd.print("Hitungan mundur");
  delay(2000);
  lcd.clear(); //menghapus tulisan sebelumnya agar berganti ke tulisan berikutnya
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
