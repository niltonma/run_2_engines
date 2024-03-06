Este repositorio será utilizado para implementar o codigo da aplicação da ortese de menbros inferiores:

P. Kaur and S. Kaur, "**Study of Impact of Electric Vehicle Integration in Unbalanced Distribution System**," *2022 IEEE International Power and Renewable Energy Conference (IPRECON)*, Kollam, India, 2022, pp. 1-6, doi: 10.1109/IPRECON55716.2022.10059564.



Será utilizado o OpenDSS com a biblioteca [py_dss_interface](https://pypi.org/project/py-dss-interface/)



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
```
