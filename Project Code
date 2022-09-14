#include <LiquidCrystal.h>
#include <IRremote.h>
#include <KickSort.h>

IRrecv IR(5);  //Sets pin 3 to receive IRremote signals
#define force_pin A0  //replace with #define force_pin A0

int mode = 0;  //force pin modes
int x = 0;
bool timerControl = true;
bool leaderControl = true;
bool leaderControl0 = true;
long startTime;
double score;
double speeds[6] = {1000, 1000, 1000, 1000, 1000, 1000};


LiquidCrystal lcd(12, 6, 10, 9, 8, 7);  //replace with lcd(12, 11, 5, 4, 3, 2);


void setup() {
  Serial.begin(115200);
  pinMode(A0, INPUT);  //change when force sensor

  //sets up the lcd display
  lcd.begin(16, 2);
  lcd.clear();
  lcd.print("1. Start Game!!!");
  lcd.setCursor(0, 1);
  lcd.print("2. Leaderboard");

  //start receiving signals from remote
  IR.enableIRIn();
}


void sortSpeeds(){    //function to sort the speeds in array
  KickSort<double>::quickSort(speeds, 6); 
}



bool pressed = false;

void loop() {
  lcd.setCursor(0, 1);  //sets the cursor to second line
  if(IR.decode()){  //for testing receiving remote data

    Serial.println(IR.decodedIRData.decodedRawData, HEX);
    IR.resume();
  }

    switch(IR.decodedIRData.decodedRawData){  //switch to control the remote controller

    case 0xF30CFF00:    //press 1 to start the challenge
      lcd.clear();
      lcd.print("Start Challenge");
    }

      while(timerControl){
        int analogReading = analogRead(force_pin);
      

        if(analogReading > 200){    //if there is a force, change pressed to true
          pressed = true;
        }

        if(analogReading < 50 && pressed){  //if force is lifted and pressed is true
          mode = 1;
          startTime = millis();
          delay(400);
          pressed = false; 
        }

        if(mode == 1){  //starts counting time with millis when mode is 1
          lcd.setCursor(0, 1);
          lcd.print((millis() - startTime) / 1000.0);
          score = (millis() - startTime) / 1000.0;
        } 

        if(analogReading > 200 && mode == 1){
          mode = 2;
        }
    }
}
