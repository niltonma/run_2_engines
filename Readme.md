Este repositorio será utilizado para implementar o codigo da aplicação da ortese de menbros inferiores:



Será utilizado Arduino para rodar a aplicação: [arduino.cc](https://www.arduino.cc/en/software)



```cpp
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
void setup() {
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
 
  }
  else{
    digitalWrite(led, LOW);
    //Serial.println(" else");
    
   }

   if(ButtonValue2 !=0){
    digitalWrite(led2, HIGH);
    //Serial.println(" if");
 
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

}
```
