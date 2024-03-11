Este repositorio será utilizado para implementar o codigo da aplicação da ortese de menbros inferiores:



Será utilizado Arduino para rodar a aplicação: [arduino.cc](https://www.arduino.cc/en/software)

Segue alguns link uteis:
- [Usar servo Motor](https://blogmasterwalkershop.com.br/arduino/como-usar-com-arduino-servo-motor-mg995)
- [Usar Ponte H](https://cdn.instructables.com/ORIG/FCN/YABW/IHNTEND4/FCNYABWIHNTEND4.pdf)
- [Usar button-latching](https://forum.arduino.cc/t/button-latching/321499/5)
- [Simulador Online](https://www.tinkercad.com/things/03YL3OztVVv-cool-krunk-crift/editel?sharecode=2el-GQnrRGlfAO1Q8Jp-CKXd9CBgFvJOoVfT7K-9hf0)
```cpp
#include <Servo.h> //INCLUSÃO DA BIBLIOTECA NECESSÁRIA

// usar servo motor
const int pinoServo = 6; //PINO DIGITAL UTILIZADO PELO SERVO  
 
Servo s; //OBJETO DO TIPO SERVO
int pos; //POSIÇÃO DO SERVO

uint32_t start, dbStart;
const byte btn = 3, btn2 = 13, led = 7, led2 = 10, dbTime = 15;
bool pinState = true,
     pinState2 = true,
     btnState = true,
     btnState2 = true,
     prevBtnState = true,
     prevBtnState2 = true,
     latch = false;
int ButtonValue = 0;
int ButtonValue2 = 0;

void walkForward(){

 for(pos = 0; pos < 180; pos++){ //PARA "pos" IGUAL A 0, ENQUANTO "pos" MENOR QUE 180, INCREMENTA "pos"
    s.write(pos); //ESCREVE O VALOR DA POSIÇÃO QUE O SERVO DEVE GIRAR
    delay(15); //INTERVALO DE 15 MILISSEGUNDOS
}
}
void walkBackward(){

    for(pos = 180; pos >= 0; pos--){ //PARA "pos" IGUAL A 180, ENQUANTO "pos" MAIOR OU IGUAL QUE 0, DECREMENTA "pos"
    s.write(pos); //ESCREVE O VALOR DA POSIÇÃO QUE O SERVO DEVE GIRAR
    delay(15); //INTERVALO DE 15 MILISSEGUNDOS
  }
  
}
void setup() {
  delay(500);
  s.attach(pinoServo); //ASSOCIAÇÃO DO PINO DIGITAL AO OBJETO DO TIPO SERVO
  s.write(0); //INICIA O MOTOR NA POSIÇÃO 0º
  Serial.begin(9600);
  pinMode(btn,INPUT);
  pinMode(led,OUTPUT);
  pinMode(btn2,INPUT);
  pinMode(led2,OUTPUT);

}

void loop() {
  // XXXXXXXXXXXXXXXXXXXXXXXXX
  
  ButtonValue = digitalRead(btn);
  ButtonValue2 = digitalRead(btn2);
  if(ButtonValue !=0){
    digitalWrite(led, HIGH);
    //Serial.println(" if");
    walkBackward();
 
  }
  else{
    digitalWrite(led, LOW);
    //Serial.println(" else");
    
   }

   if(ButtonValue2 !=0){
    digitalWrite(led2, HIGH);
    //Serial.println(" if");

    walkForward();
 
  }
  else{
    digitalWrite(led2, LOW);
    //Serial.println(" else");
    
   }
 
   
  
  // XXXXXXXXXXXXXXXXXXXXX
  // debounce button ++++++++++++++++
  if (digitalRead(btn) != pinState)  // get state of pin 2
  {
    dbStart = millis();     // reset db timer
    pinState = !pinState;   // now they are equal, won't enter
  }                         // here again unless pin state changes
  if (millis() - dbStart > dbTime) // db timer has elapsed
    btnState = pinState;           // button state is valid 
//+++++++++++++++++++++++++++++++++++  
  if(btnState != prevBtnState && btnState == HIGH) // btnState changed
  {
    // if button pressed and NOT latched
    if(!latch)
    {
      latch = true;    // prevents entry while latched
      digitalWrite(led,HIGH);
    }  
    else
    {
      // if button pressed while latched,
      latch = false;
      digitalWrite(led,LOW);
    }
    Serial.print( "LED is ");
    if(latch)
    {
      Serial.println("ON ==> run engine");
    }
    else
    {
      Serial.println("OFF ==> stop engine");  
    }
  }
  prevBtnState = btnState;

// botao 2

  // XXXXXXXXXXXXXXXXXXXXX
  // debounce button ++++++++++++++++
  if (digitalRead(btn2) != pinState2)  // get state of pin 2
  {
    dbStart = millis();     // reset db timer
    pinState2 = !pinState2;   // now they are equal, won't enter
  }                         // here again unless pin state changes
  if (millis() - dbStart > dbTime) // db timer has elapsed
    btnState2 = pinState2;           // button state is valid 
//+++++++++++++++++++++++++++++++++++  
  if(btnState2 != prevBtnState2 && btnState2 == HIGH) // btnState changed
  {
    // if button pressed and NOT latched
    if(!latch)
    {
      latch = true;    // prevents entry while latched
      digitalWrite(led2,HIGH);
    }  
    else
    {
      // if button pressed while latched,
      latch = false;
      digitalWrite(led2,LOW);
    }
    Serial.print( "LED blue is ");
    if(latch)
    {
      Serial.println("ON ==> run engine 2");
    }
    else
    {
      Serial.println("OFF ==> stop engine 2");  
    }
  }
  prevBtnState2 = btnState2;



}
```
