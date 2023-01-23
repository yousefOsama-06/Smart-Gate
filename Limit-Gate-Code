#include <LiquidCrystal.h>
LiquidCrystal lcd(11, 10, 5, 4, 3, 2);

int people = 0;
bool Sensed[2] = {false, false}, on = false, showed = false;

void setup() {
  // put your setup code here, to run once:
  pinMode(6, INPUT);
  pinMode(12, INPUT);
  pinMode(13, INPUT);
  pinMode(8, OUTPUT);
  lcd.begin(16, 2);
}

void loop() {
  // put your main code here, to run repeatedly:
  bool Button = digitalRead(12);
  if(Button) {
    if(!showed) {
        Show();
        showed = true;  
    }else {
      lcd.clear();
      people = 0;
      on = !on;
      if(on) {
        lcd.print("There are");
        lcd.setCursor(0, 1);
        if(people != 0)
          lcd.print(people);
        else
          lcd.print("no");
        lcd.print(" persons");
      }
      delay(250);
    }
  }
  
  if(on) {
    bool PIR[2] = {digitalRead(6), digitalRead(7)};

    for(int i = 0; i < 2; i++){
      if(PIR[i] && !PIR[1-i]) {
        Sensed[i] = true;
        if(Sensed[1-i]) {
          people += i? 1 : -1;
          lcd.clear();
          lcd.print(people == 1? "There is" : "There are");
          lcd.setCursor(0, 1);
          if(people != 0)
            lcd.print(people);
          else
            lcd.print("no");
          lcd.print(people == 1? " person" : " persons");
          tone(9, 700 + 200*i, 100);
          Sensed[0] = false;
          Sensed[1] = false;
          if(people <= 5)
            delay(3000);
        }
      }
    }

    if(people > 5) {
      alert();
    }
  }
}

void Show(){
  lcd.clear();
  String s[4] = {"Welcome to our", "Arduino project", "Press the Push", "Button to start"};
  for(int i = 0; i < 14; i++) {
    lcd.print(s[0][i]);
    if(s[0][i] != ' ' && s[0][i] != '\n')
      delay(200);
  }
  lcd.setCursor(0, 1);
  for(int i = 0; i < 15; i++) {
    lcd.print(s[1][i]);
    if(s[1][i] != ' ' && s[1][i] != '\n')
      delay(200);
  }
  delay(500);
  lcd.clear();
  for(int i = 0; i < 14; i++) {
    lcd.print(s[2][i]);
    if(s[2][i] != ' ' && s[2][i] != '\n')
      delay(200);
  }
  lcd.setCursor(0, 1);
  for(int i = 0; i < 15; i++) {
    lcd.print(s[3][i]);
    if(s[3][i] != ' ' && s[3][i] != '\n')
      delay(200);
  }
}

void alert(){
  tone(9, 1500, 150);
  digitalWrite(8, HIGH);
  delay(150);
  tone(9, 1000, 150);
  digitalWrite(8, LOW);
  delay(150);
}
