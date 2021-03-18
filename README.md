// include the library code:
#include <LiquidCrystal.h>

// initialize the library with the numbers of the interface pins
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

int sensePin = A0;  //This is the Arduino Pin that will read the sensor output
int sensorInput;    //The variable we will use to store the sensor input
double temp;        //The variable we will use to store temperature in degrees. 
 
void setup() {

  lcd.begin(16, 2);// set up the LCD's number of columns and rows:
  lcd.print("#MYOWNSENSOR");// Print a message to the LCD
  pinMode(9, OUTPUT);//digital pin 9
  pinMode(8, OUTPUT);//digital pin 8
  Serial.begin(9600); //TROUBLESHOOT
}

void loop() {
  
  lcd.setCursor(0,1);
  lcd.print("TEMP : ");
  sensorInput = analogRead(A0);     //read the analog sensor and store it
  temp = (double)sensorInput / 1024;//find percentage of input reading
  temp = temp * 5;                  //multiply by 5V to get voltage
  temp = temp - 0.5;                //Subtract the offset 
  temp = temp * 100;                //Convert to degrees 
 
  Serial.print("Current Temperature: "); // prints in lcd screen
  Serial.println(temp);
  lcd.print(temp);
  lcd.print("C"); // prints in lcd screen
  
  if(temp>=40)
  {
    digitalWrite(9,HIGH); //RED LED
    digitalWrite(8,LOW); //GREEN LED
    lcd.setCursor(0,2);
    lcd.print("HOT !! "); // prints in lcd screen
    delay(1000); // delays by 1 milisecond
  }
else if(temp<40)
  {
    digitalWrite(9,LOW); //RED LED
    digitalWrite(8,HIGH); //GREEN LED
  }

 
}
