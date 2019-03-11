# ARDUINO PROGRAMA



#include <Wire.h>
#include <Adafruit_PWMServoDriver.h>
#include <TimerOne.h>

Adafruit_PWMServoDriver servos = Adafruit_PWMServoDriver(0x40);

#define SERVOMIN  150 // this is the 'minimum' pulse length count (out of 4096)
#define SERVOMAX  600 // this is the 'maximum' pulse length count (out of 4096)


const int button1 = 5;      // botoia 1
const int button2 = 6;      // botoia 2
const int button3 = 7;      // botoia 3
const int button4 = 8;      // botoia 4
const int led1 = 2;
const int led2 = 3;
const int led3 = 4;
const int led4 = 9;
int servonum = 0;

int posicion1 = 590;

int bat=0;       // Pultsagailu eta sentoreen egoeraren aldagaia
int bi=0;
int hiru=0;  
int lau=0;
int sen1=0;
int sen2=0;

int button1state = 0;
int button2state = 0;
int button3state = 0;
int button4state = 0;

void hasieraON();
void xixareaON();
void espiralaON();
void polikiON();
void bikoitibakoitiON(); 
void denakOFF();
void sensorea1();
void sensorea2();


int echo1 = 10;                // sensorea1
int trip1 = 12;               // sensorea1
long duracion1, distancia1;   // sensorea1

int echo2 = 11;               // sensorea2
int trip2 = 13;               // sensorea2
long duracion2, distancia2;   // sensorea2



void setup() {


  Timer1.initialize(250000);         // Dispara cada 250 ms
  Timer1.attachInterrupt(comprobar); // Activa la interrupcion y la asocia a comprobar
       
  Serial.begin(9600);
  Serial.println("16 channel Servo test!");

  servos.begin();
  
  servos.setPWMFreq(60);  // Analog servos run at ~60 Hz updates
 
  pinMode(button1,INPUT);       //botoiak
  pinMode(button2,INPUT);
  pinMode(button3,INPUT);
  pinMode(button4,INPUT);

  pinMode(echo1, INPUT);       // sensorea 1
  pinMode(trip1, OUTPUT); 
 
  pinMode(echo2, INPUT);       // sensorea 2
  pinMode(trip2, OUTPUT);

  pinMode(led1,OUTPUT);        // led-ak
  pinMode(led2,OUTPUT);
  pinMode(led3,OUTPUT);
  pinMode(led4,OUTPUT);
  
  servos.setPWM(0, 0, 150);
  servos.setPWM(1, 0, 150);
  servos.setPWM(2, 0, 150);  
  servos.setPWM(3, 0, 150); 
  servos.setPWM(4, 0, 150); 
  servos.setPWM(5, 0, 150);
  servos.setPWM(6, 0, 150);
  servos.setPWM(7, 0, 150);
  servos.setPWM(8, 0, 150); 
  servos.setPWM(9, 0, 150);
  servos.setPWM(10, 0, 150);
  servos.setPWM(11, 0, 150); 
  servos.setPWM(12, 0, 150); 
  servos.setPWM(13, 0, 150);
  servos.setPWM(14, 0, 150);
  servos.setPWM(15, 0, 150);
}

  // you can use this function if you'd like to set the pulse length in seconds
  // e.g. setServoPulse(0, 0.001) is a ~1 millisecond pulse width. its not precise!
  void setServoPulse(uint8_t n, double pulse) {
  double pulselength;
  
  pulselength = 1000000;   // 1,000,000 us per second
  pulselength /= 60;   // 60 Hz
  Serial.print(pulselength); Serial.println(" us per period"); 
  pulselength /= 4096;  // 12 bits of resolution
  Serial.print(pulselength); Serial.println(" us per bit"); 
  pulse *= 1000;
  pulse /= pulselength;
  Serial.println(pulse);
  servos.setPWM(n, 0, pulse);
}

void loop() {
 
  hasieraON();

 if (bat>0){
  xixareaON();
 }
 if (bi>0){
  espiralaON();
 }
 if (hiru>0){
  polikiON();
 }
 if (lau>0){
  bikoitibakoitiON(); 
 }
 if (sen1>0){
  sensorea1();
 }
 if (sen2>0){
  sensorea2();
 }

}

 
 
 //Funtzioak

void comprobar ()
{
  button1state=digitalRead(button1);
  button2state=digitalRead(button2);
  button3state=digitalRead(button3);
  button4state=digitalRead(button4);


  digitalWrite(trip1, LOW);             // 1 sentsorearen pultsua sartzeko
  delayMicroseconds(2);
  digitalWrite(trip1, HIGH);
  delayMicroseconds(10);
  digitalWrite(trip1, LOW);
  duracion1 = pulseIn(echo1, HIGH);
  distancia1 = (duracion1/2) /29;
 
  digitalWrite(trip2, LOW);              // 2 sentsorearen pultsua sartzeko
  delayMicroseconds(2);
  digitalWrite(trip2, HIGH);
  delayMicroseconds(10);
  digitalWrite(trip2, LOW);
  duracion2 = pulseIn(echo2, HIGH);
  distancia2 = (duracion2/2) /29;
 
  if (button1state== LOW)
   {bat++;
   digitalWrite(led3, HIGH);}
   if (button2state== LOW)
   {bi++;
    digitalWrite(led4, HIGH);}
   if (button3state== LOW)
    {hiru++;
    digitalWrite(led2, HIGH);}
   if (button4state== LOW)
  {lau++;
    digitalWrite(led1, HIGH); }
  if(distancia1 <=20 && distancia1 >=1){
  sen1++;
  digitalWrite(led3, HIGH); 
  digitalWrite(led4, HIGH); }
  if(distancia2 <=20 && distancia2 >=1){
  sen2++;
  digitalWrite(led1, HIGH); 
  digitalWrite(led2, HIGH); } 
}

void hasieraON(){           //Hasierako mugimenduak
 
  servos.setPWM(5, 0, 150);
  servos.setPWM(5, 0, 600);
  servos.setPWM(6, 0, 150);
  servos.setPWM(6, 0, 600);
  servos.setPWM(9, 0, 150);
  servos.setPWM(9, 0, 600);
  servos.setPWM(10, 0, 150);
  servos.setPWM(10, 0, 600);
  delay(500);
  servos.setPWM(3, 0, 150);
  servos.setPWM(3, 0, 600);
  servos.setPWM(7, 0, 150);
  servos.setPWM(7, 0, 600);
  servos.setPWM(11, 0, 150);
  servos.setPWM(11, 0, 600);
  servos.setPWM(15, 0, 150);
  servos.setPWM(15, 0, 600);
  servos.setPWM(14, 0, 150);
  servos.setPWM(14, 0, 600);
  servos.setPWM(13, 0, 150);
  servos.setPWM(13, 0, 600);
  servos.setPWM(12, 0, 150);
  servos.setPWM(12, 0, 600);
  servos.setPWM(8, 0, 150);
  servos.setPWM(8, 0, 600);   
  servos.setPWM(4, 0, 150);   
  servos.setPWM(4, 0, 600);
  servos.setPWM(0, 0, 150);
  servos.setPWM(0, 0, 600);
  servos.setPWM(1, 0, 150);
  servos.setPWM(1, 0, 600);
  servos.setPWM(2, 0, 150);
  servos.setPWM(2, 0, 600);
  delay(500);
  
  servos.setPWM(5, 0, 600);
  servos.setPWM(5, 0, 150);
  servos.setPWM(6, 0, 600);
  servos.setPWM(6, 0, 150);
  servos.setPWM(9, 0, 600);
  servos.setPWM(9, 0, 150);
  servos.setPWM(10, 0, 600);
  servos.setPWM(10, 0, 150);
  delay(500);
  servos.setPWM(3, 0, 600);
  servos.setPWM(3, 0, 150);
  servos.setPWM(7, 0, 600);
  servos.setPWM(7, 0, 150);
  servos.setPWM(11, 0, 600);
  servos.setPWM(11, 0, 150);
  servos.setPWM(15, 0, 600);
  servos.setPWM(15, 0, 150);
  servos.setPWM(14, 0, 600);
  servos.setPWM(14, 0, 150);
  servos.setPWM(13, 0, 600);
  servos.setPWM(13, 0, 150);
  servos.setPWM(12, 0, 600);
  servos.setPWM(12, 0, 150);
  servos.setPWM(8, 0, 600);
  servos.setPWM(8, 0, 150);   
  servos.setPWM(4, 0, 600);   
  servos.setPWM(4, 0, 150);
  servos.setPWM(0, 0, 600);
  servos.setPWM(0, 0, 150);
  servos.setPWM(1, 0, 600);
  servos.setPWM(1, 0, 150);
  servos.setPWM(2, 0, 600);
  servos.setPWM(2, 0, 150);
  delay(500);
}

void xixareaON(){         // 1- Xixarea goiko ezkerretik hasita ON funtzioa
 
  servos.setPWM(0, 0, 150);
  servos.setPWM(0, 0, 600);
  delay(250);
  servos.setPWM(1, 0, 150);
  servos.setPWM(1, 0, 600);
  delay(250);
  servos.setPWM(2, 0, 150);
  servos.setPWM(2, 0, 600);
  delay(250);
  servos.setPWM(3, 0, 150);
  servos.setPWM(3, 0, 600);
  delay(250);
  servos.setPWM(7, 0, 150);
  servos.setPWM(7, 0, 600);
  delay(250);
  servos.setPWM(6, 0, 150);
  servos.setPWM(6, 0, 600);
  delay(250);
  servos.setPWM(5, 0, 150);
  servos.setPWM(5, 0, 600);
  delay(250);
  servos.setPWM(4, 0, 150);
  servos.setPWM(4, 0, 600);
  delay(250);
  servos.setPWM(8, 0, 150);
  servos.setPWM(8, 0, 600);
  delay(250);
  servos.setPWM(9, 0, 150);
  servos.setPWM(9, 0, 600);
  delay(250);
  servos.setPWM(10, 0, 150);
  servos.setPWM(10, 0, 600);
  delay(250);
  servos.setPWM(11, 0, 150);
  servos.setPWM(11, 0, 600);
  delay(250);
  servos.setPWM(15, 0, 150);
  servos.setPWM(15, 0, 600);
  delay(250);
  servos.setPWM(14, 0, 150);
  servos.setPWM(14, 0, 600);
  delay(250);
  servos.setPWM(13, 0, 150);
  servos.setPWM(13, 0, 600);
  delay(250);
  servos.setPWM(12, 0, 150);
  servos.setPWM(12, 0, 600);
  
  delay(1000);

  servos.setPWM(12, 0, 600);
  servos.setPWM(12, 0, 150);
  delay(250);
  servos.setPWM(13, 0, 600);
  servos.setPWM(13, 0, 150);
  delay(250);
  servos.setPWM(14, 0, 600);
  servos.setPWM(14, 0, 150);
  delay(250);
  servos.setPWM(15, 0, 600);
  servos.setPWM(15, 0, 150);
  delay(250);
  servos.setPWM(11, 0, 600);
  servos.setPWM(11, 0, 150);
  delay(250);
  servos.setPWM(10, 0, 600);
  servos.setPWM(10, 0, 150);
  delay(250);
  servos.setPWM(9, 0, 600);
  servos.setPWM(9, 0, 150);
  delay(250);
  servos.setPWM(8, 0, 600);
  servos.setPWM(8, 0, 150);
  delay(250);
  servos.setPWM(4, 0, 600);
  servos.setPWM(4, 0, 150);
  delay(250);
  servos.setPWM(5, 0, 600);
  servos.setPWM(5, 0, 150);
  delay(250);
  servos.setPWM(6,0 ,600);
  servos.setPWM(6, 0 ,150);
  delay(250);
  servos.setPWM(7,0 ,600);
  servos.setPWM(7,0 ,150);
  delay(250);
  servos.setPWM(3,0 ,600);
  servos.setPWM(3,0 ,150);
  delay(250);
  servos.setPWM(2,0 ,600);
  servos.setPWM(2,0 ,150);
  delay(250);
  servos.setPWM(1,0 ,600);
  servos.setPWM(1,0 ,150);
  delay(250);
  servos.setPWM(0,0 ,600);
  servos.setPWM(0,0 ,150);
  digitalWrite(led3, LOW);
  delay(1000);
  bat=0;
 }


void espiralaON(){                // 2- Espirala goitik ezkerretik hasita ON funtzioa
 
  servos.setPWM(0, 0, 150);
  servos.setPWM(0, 0, 600);
  delay(250);
  servos.setPWM(1, 0, 150);
  servos.setPWM(1, 0, 600);
  delay(250);
  servos.setPWM(2, 0, 150);
  servos.setPWM(2, 0, 600);
  delay(250);
  servos.setPWM(3, 0, 150);
  servos.setPWM(3, 0, 600);
  delay(250);
  servos.setPWM(7, 0, 150);
  servos.setPWM(7, 0, 600);
  delay(250);
  servos.setPWM(11, 0, 150);
  servos.setPWM(11, 0, 600);
  delay(250);
  servos.setPWM(15, 0, 150);
  servos.setPWM(15, 0, 600);
  delay(250);
  servos.setPWM(14, 0, 150);
  servos.setPWM(14, 0, 600);
  delay(250);
  servos.setPWM(13, 0, 150);
  servos.setPWM(13, 0, 600);
  delay(250);
  servos.setPWM(12, 0, 150);
  servos.setPWM(12, 0, 600);
  delay(250);
  servos.setPWM(8, 0, 150);
  servos.setPWM(8, 0, 600);
  delay(250);
  servos.setPWM(4, 0, 150);
  servos.setPWM(4, 0, 600);
  delay(250);
  servos.setPWM(5, 0, 150);
  servos.setPWM(5, 0, 600);
  delay(250);
  servos.setPWM(6, 0, 150);
  servos.setPWM(6, 0, 600);
  delay(250);
  servos.setPWM(10, 0, 150);
  servos.setPWM(10, 0, 600);
  delay(250);
  servos.setPWM(9, 0, 150);
  servos.setPWM(9, 0, 600);  
  delay(1000);
  servos.setPWM(9, 0, 600);
  servos.setPWM(9, 0, 150);
  delay(250);
  servos.setPWM(10, 0, 600);
  servos.setPWM(10, 0, 150);
  delay(250);
  servos.setPWM(6, 0, 600);
  servos.setPWM(6, 0, 150);
  delay(250);
  servos.setPWM(5, 0, 600);
  servos.setPWM(5, 0, 150);
  delay(250);
  servos.setPWM(4, 0, 600);
  servos.setPWM(4, 0, 150);
  delay(250);
  servos.setPWM(8, 0, 600);
  servos.setPWM(8, 0, 150);
  delay(250);
  servos.setPWM(12, 0, 600);
  servos.setPWM(12, 0, 150);
  delay(250);
  servos.setPWM(13, 0, 600);
  servos.setPWM(13, 0, 150);
  delay(250);
  servos.setPWM(14, 0, 600);
  servos.setPWM(14, 0, 150);
  delay(250);
  servos.setPWM(15, 0, 600);
  servos.setPWM(15, 0, 150);
  delay(250);
  servos.setPWM(11,0 ,600);
  servos.setPWM(11,0 ,150);
  delay(250);
  servos.setPWM(7,0 ,600);
  servos.setPWM(7,0 ,150);
  delay(250);
  servos.setPWM(3,0 ,600);
  servos.setPWM(3,0 ,150);
  delay(250);
  servos.setPWM(2,0 ,600);
  servos.setPWM(2,0 ,150);
  delay(250);
  servos.setPWM(1,0 ,600);
  servos.setPWM(1,0 ,150);
  delay(250);
  servos.setPWM(0,0 ,600);
  servos.setPWM(0,0 ,150);
  digitalWrite(led4, LOW);
  delay(1000);
  bi=0; 
}


void polikiON(){          //  3- Motorrak mantxotuaraziz irudiak. Funtzioa
  
  for (int posicion=150; posicion<1200; posicion=posicion+20){
    if (posicion < 600){
    servos.setPWM(0, 0, posicion);
    servos.setPWM(4, 0, posicion);
    servos.setPWM(8, 0, posicion);
    servos.setPWM(12,0, posicion);
    servos.setPWM(3, 0, posicion);
    servos.setPWM(7, 0, posicion);
    servos.setPWM(11,0, posicion);
    servos.setPWM(15,0, posicion);
    }
    if (posicion > 600){
    servos.setPWM(0, 0, (1200 - posicion));
    servos.setPWM(4, 0, (1200 - posicion));
    servos.setPWM(8, 0, (1200 - posicion));
    servos.setPWM(12,0, (1200 - posicion));
    servos.setPWM(3, 0, (1200 - posicion));
    servos.setPWM(7, 0, (1200 - posicion));
    servos.setPWM(11,0, (1200 - posicion));
    servos.setPWM(15,0, (1200 - posicion));
    }
    servos.setPWM(1, 0, (posicion/2));
    servos.setPWM(5, 0, (posicion/2));
    servos.setPWM(9, 0, (posicion/2));
    servos.setPWM(13,0, (posicion/2));
    servos.setPWM(2, 0, (posicion/2));
    servos.setPWM(6, 0, (posicion/2));
    servos.setPWM(10,0, (posicion/2));
    servos.setPWM(14,0, (posicion/2));
    
  }
    delay(100);
    
    posicion1 = 590;
    for (int posicion=1200; posicion>150; posicion=posicion-20){
    if (posicion > 600){
    servos.setPWM(0, 0, (1350 - posicion));
    servos.setPWM(4, 0, (1350 - posicion));
    servos.setPWM(8, 0, (1350 - posicion));
    servos.setPWM(12,0, (1350 - posicion));
    servos.setPWM(3, 0, (1350 - posicion));
    servos.setPWM(7, 0, (1350 - posicion));
    servos.setPWM(11,0, (1350 - posicion));
    servos.setPWM(15,0, (1350 - posicion));
    }
    if (posicion < 600){
    servos.setPWM(0, 0, posicion);
    servos.setPWM(4, 0, posicion);
    servos.setPWM(8, 0, posicion);
    servos.setPWM(12,0, posicion);
    servos.setPWM(3, 0, posicion);
    servos.setPWM(7, 0, posicion);
    servos.setPWM(11,0, posicion);
    servos.setPWM(15,0, posicion);
    }
    servos.setPWM(1, 0, posicion1);
    servos.setPWM(5, 0, posicion1);
    servos.setPWM(9, 0, posicion1);
    servos.setPWM(13,0, posicion1);
    servos.setPWM(2, 0, posicion1);
    servos.setPWM(6, 0, posicion1);
    servos.setPWM(10,0, posicion1);
    servos.setPWM(14,0, posicion1);
    
    posicion1 = posicion1-10;
    digitalWrite(led2, LOW);
    delay(100);
    hiru=0;
}
  }

void bikoitibakoitiON(){     //  4- Bikoiti/ bakoiti txandaka funtzioa
   
  servos.setPWM(1, 0, 150);
  servos.setPWM(1, 0, 600);
  servos.setPWM(5, 0, 150);
  servos.setPWM(5, 0, 600);
  servos.setPWM(9, 0, 150);
  servos.setPWM(9, 0, 600);
  servos.setPWM(13, 0, 150);
  servos.setPWM(13, 0, 600); 
  delay(250);
  servos.setPWM(3, 0, 150);
  servos.setPWM(3, 0, 600);
  servos.setPWM(7, 0, 150);
  servos.setPWM(7, 0, 600);
  servos.setPWM(11, 0, 150);
  servos.setPWM(11, 0, 600);
  servos.setPWM(15, 0, 150);
  servos.setPWM(15, 0, 600);
  delay(1000);
  servos.setPWM(0, 0, 150);
  servos.setPWM(0, 0, 600);
  servos.setPWM(4, 0, 150);
  servos.setPWM(4, 0, 600);
  servos.setPWM(8, 0, 150);
  servos.setPWM(8, 0, 600);
  servos.setPWM(12, 0, 150);
  servos.setPWM(12, 0, 600);
  delay(250);
  servos.setPWM(2, 0, 150);
  servos.setPWM(2, 0, 600);
  servos.setPWM(6, 0, 150);
  servos.setPWM(6, 0, 600);
  servos.setPWM(10, 0, 150);
  servos.setPWM(10, 0, 600);
  servos.setPWM(14, 0, 150);
  servos.setPWM(14, 0, 600);
  delay(1000);
  servos.setPWM(2, 0, 150);
  servos.setPWM(6, 0, 150);
  servos.setPWM(10, 0, 150);
  servos.setPWM(14, 0, 150);
  delay(250);
  servos.setPWM(0, 0, 150);
  servos.setPWM(4, 0, 150);
  servos.setPWM(8, 0, 150);
  servos.setPWM(12, 0, 150);
  delay(1000);
  servos.setPWM(3, 0, 150);
  servos.setPWM(7, 0, 150);
  servos.setPWM(11, 0, 150);
  servos.setPWM(15, 0, 150);
  delay(250);
  servos.setPWM(1, 0, 150);
  servos.setPWM(5, 0, 150);
  servos.setPWM(9, 0, 150);
  servos.setPWM(13, 0, 150); 
  digitalWrite(led1, LOW);
  delay(1000);
  lau=0;
}

void sensorea1(){                             //sensorea 1 funtzioa. Alde batetik bestera behe eskubitik ezker gora.
  
  servos.setPWM(3, 0, 150);
  servos.setPWM(3, 0, 600);
  delay(500);
  servos.setPWM(2, 0, 150);
  servos.setPWM(2, 0, 600);
  servos.setPWM(7, 0, 150);
  servos.setPWM(7, 0, 600);
  delay(500);
  servos.setPWM(1, 0, 150);
  servos.setPWM(1, 0, 600);
  servos.setPWM(6, 0, 150);
  servos.setPWM(6, 0, 600); 
  servos.setPWM(11, 0, 150);
  servos.setPWM(11, 0, 600);
  delay(500);
  servos.setPWM(0, 0, 150);
  servos.setPWM(0, 0, 600);
  servos.setPWM(5, 0, 150);
  servos.setPWM(5, 0, 600);
  servos.setPWM(10, 0, 150);
  servos.setPWM(10, 0, 600);
  servos.setPWM(15, 0, 150);
  servos.setPWM(15, 0, 600);
  delay(500);
  servos.setPWM(4, 0, 150);
  servos.setPWM(4, 0, 600);
  servos.setPWM(9, 0, 150);
  servos.setPWM(9, 0, 600);
  servos.setPWM(14, 0, 150);
  servos.setPWM(14, 0, 600);
  delay(500);
  servos.setPWM(8, 0, 150);
  servos.setPWM(8, 0, 600);
  servos.setPWM(13, 0, 150);
  servos.setPWM(13, 0, 600);
  delay(500);
  servos.setPWM(12, 0, 150);
  servos.setPWM(12, 0, 600);
  digitalWrite(led3, LOW); 
  digitalWrite(led4, LOW); 
  delay(1000);
  servos.setPWM(0, 0, 150);
  servos.setPWM(1, 0, 150);
  servos.setPWM(2, 0, 150);  
  servos.setPWM(3, 0, 150); 
  servos.setPWM(4, 0, 150); 
  servos.setPWM(5, 0, 150);
  servos.setPWM(6, 0, 150);
  servos.setPWM(7, 0, 150);
  servos.setPWM(8, 0, 150); 
  servos.setPWM(9, 0, 150);
  servos.setPWM(10, 0, 150);
  servos.setPWM(11, 0, 150); 
  servos.setPWM(12, 0, 150); 
  servos.setPWM(13, 0, 150);
  servos.setPWM(14, 0, 150);
  servos.setPWM(15, 0, 150);
  delay(1000);
  sen1=0;
}

void sensorea2(){                             //sensorea 2 funtzioa. Alde batetik bestera goi ezkerretik hasita behe eskubira.

  servos.setPWM(0, 0, 150);
  servos.setPWM(0, 0, 600);
  delay(500);
  servos.setPWM(1, 0, 150);
  servos.setPWM(1, 0, 600);
  servos.setPWM(4, 0, 150);
  servos.setPWM(4, 0, 600);
  delay(500); 
  servos.setPWM(8, 0, 150);
  servos.setPWM(8, 0, 600);
  servos.setPWM(5, 0, 150);
  servos.setPWM(5, 0, 600);
  servos.setPWM(2, 0, 150);
  servos.setPWM(2, 0, 600);
  delay(500);
  servos.setPWM(12, 0, 150);
  servos.setPWM(12, 0, 600);
  servos.setPWM(9, 0, 150);
  servos.setPWM(9, 0, 600);
  servos.setPWM(6, 0, 150);
  servos.setPWM(6, 0, 600);
  servos.setPWM(3, 0, 150);
  servos.setPWM(3, 0, 600);
  delay(500);
  servos.setPWM(13, 0, 150);
  servos.setPWM(13, 0, 600);
  servos.setPWM(10, 0, 150);
  servos.setPWM(10, 0, 600);
  servos.setPWM(7, 0, 150);
  servos.setPWM(7, 0, 600);
  delay(500);
  servos.setPWM(14, 0, 150);
  servos.setPWM(14, 0, 600);
  servos.setPWM(11, 0, 150);
  servos.setPWM(11, 0, 600);
  delay(500);
  servos.setPWM(15, 0, 150);
  servos.setPWM(15, 0, 600);
  digitalWrite(led1, LOW); 
  digitalWrite(led2, LOW); 
  delay(1000);
  servos.setPWM(0, 0, 150);
  servos.setPWM(1, 0, 150);
  servos.setPWM(2, 0, 150);  
  servos.setPWM(3, 0, 150); 
  servos.setPWM(4, 0, 150); 
  servos.setPWM(5, 0, 150);
  servos.setPWM(6, 0, 150);
  servos.setPWM(7, 0, 150);
  servos.setPWM(8, 0, 150); 
  servos.setPWM(9, 0, 150);
  servos.setPWM(10, 0, 150);
  servos.setPWM(11, 0, 150); 
  servos.setPWM(12, 0, 150); 
  servos.setPWM(13, 0, 150);
  servos.setPWM(14, 0, 150);
  servos.setPWM(15, 0, 150);
  delay(1000);
  sen2=0;
