#Projeto de Monitoramento de Temperatura com Arduino Uno
Este projeto utiliza um Arduino Uno para monitorar a temperatura ambiente utilizando um sensor DHT22. A temperatura medida é exibida em um display LCD 16x2. Além disso, dois LEDs (um vermelho e um verde) são usados para indicar o estado do sistema.

Componentes Necessários
1 x Arduino Uno
1 x Protoboard
1 x Sensor de Temperatura e Umidade DHT22
1 x Display LCD 16x2
1 x Resistor de 1 Ω
1 x Resistor de 10 Ω
1 x LED Vermelho
1 x LED Verde
Fios Jumper
Diagrama de Ligação

Montagem
Conecte o pino VCC do DHT22 em uma fonte positiva;
Conecte o pino GND do DHT22 em uma fonte negativa;
Conecte o pino de dados do DHT22 ao pino digital 13 do Arduino.
Conecte os pinos VCC e GND do LCD 16x2 aos pinos 5V e GND do Arduino, respectivamente.
Conecte os pinos RS, E, D4, D5, D6 e D7 do LCD aos pinos digitais 12, 11, 5, 4, 3 e 2 do Arduino, respectivamente.
Conecte um resistor de 1 Ω em série com o LED vermelho e ligue-o ao pino digital 8 do Arduino.
Conecte um resistor de 10 Ω em série com o LED verde e ligue-o ao pino digital 9 do Arduino.
#Código Fonte
#include <LiquidCrystal.h>
#include <DHT.h>
#include <Adafruit_Sensor.h> 
#include <DHT_U.h>


int ledVerde = 9;
int ledVermelho = 8;

#define DHT_TYPE      DHT22
#define DHT_PIN 13
DHT dht(DHT_PIN, DHT_TYPE);

LiquidCrystal lcd(12, 10, 5, 4, 3, 2);


void setup() {
  // put your setup code here, to run once:
  dht.begin();
  lcd.begin(16, 2);
  Serial.begin(9600);
  pinMode(ledVerde, OUTPUT);
  pinMode(ledVermelho, OUTPUT);

}

void loop() {
  // put your main code here, to run repeatedly:
  float temperature = dht.readTemperature();
  Serial.println("Temperature: ");
  Serial.println(temperature);
  lcd.setCursor(0, 0);
  lcd.print("Temp ");
  lcd.print(temperature);
  lcd.setCursor(15, 0);
  lcd.print("C");
  digitalWrite(ledVerde, HIGH);
  digitalWrite(ledVermelho, LOW);
  if (temperature >= 30){
    digitalWrite(ledVermelho, HIGH);
    digitalWrite(ledVerde, LOW);
  }

}

Funcionamento
O Arduino inicializa e exibe uma mensagem de inicialização no LCD.
O sensor DHT22 lê a temperatura ambiente.
A temperatura é exibida no LCD.
O LED verde acende se a temperatura estiver abaixo de 30°C, e o LED vermelho acende se a temperatura estiver igual ou superior a 30°C.
O sistema atualiza a leitura da temperatura a cada 2 segundos.
Conclusão
Este projeto demonstra como usar um Arduino Uno para monitorar a temperatura ambiente e exibir os dados em um display LCD 16x2, além de utilizar LEDs para indicar diferentes estados de temperatura. É um projeto básico e excelente para iniciantes aprenderem sobre sensores, displays e controle de LEDs com o Arduino.

Referências
- Arduino
- Biblioteca DHT
- Biblioteca LiquidCrystal
