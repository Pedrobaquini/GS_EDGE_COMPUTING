# GS_EDGE_COMPUTING


Pedro Arao Baquini RM 559580

Cilas Pinto Macedo RM 560745

### LINK PARA O PROJETO: https://wokwi.com/projects/415290095208544257


Projeto: Sistema de Cálculo de Economia de Energia com LEDs e LCD
Descrição do Projeto
Este projeto foi desenvolvido para calcular a média de consumo de energia com base em três valores fornecidos pelo usuário e, em seguida, avaliar a redução percentual do consumo quando comparado com um quarto valor. Dependendo do resultado, o sistema ativa LEDs de diferentes cores para indicar a meta atingida e exibe informações no LCD.

# Funcionamento do Sistema

### Entrada de Dados:

O usuário insere três valores (por exemplo, consumo de energia nos últimos meses) pelo Monitor Serial.
O sistema calcula a média desses três valores.
O usuário fornece um quarto valor (consumo atual) para comparação.

### Cálculo de Redução:

Classificação e Indicação de Metas:

LED Vermelho: Não atingiu nenhuma meta (redução menor que 15%).

LED Laranja: Primeira meta atingida (redução entre 15% e 25%).

LED Amarelo: Segunda meta atingida (redução entre 25% e 30%).

LED Verde: Terceira meta atingida (redução acima de 30%).

Requisitos de Hardware

LCD I2C 16x2.

LEDs:
Vermelho, Laranja, Amarelo, Verde.

### Conexões do Circuito

LCD I2C:
Conecte os pinos SDA e SCL aos pinos A4 e A5 do Arduino, respectivamente.
LEDs:
Conecte os anodos dos LEDs aos pinos digitais 8 (vermelho), 9 (laranja), 10 (amarelo) e 11 (verde), utilizando resistores de 220 ohms.
Conecte os cátodos ao GND.

Dependências e Configuração

### Bibliotecas Necessárias

LiquidCrystal_I2C

### Configuração no WOKWI

No arquivo JSON do projeto WOKWI, adicione o seguinte codigo para que o Monitor Serial inicie aberto e aceite entradas:
 "serialMonitor": { "display": "always", "newline": "lf" },

# Codigo do Projeto:

#include <Wire.h>

#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);

int ledVermelho = 8; 

int ledLaranja = 9;  

int ledAmarelo = 10; 

int ledVerde = 11;   

void setup() {

  lcd.init();

  lcd.backlight();

  Serial.begin(9600);


  pinMode(ledVermelho, OUTPUT);

  pinMode(ledLaranja, OUTPUT);

  pinMode(ledAmarelo, OUTPUT);

  pinMode(ledVerde, OUTPUT);

  lcd.print("Calculo de Media");

  delay(2000);

  lcd.clear();
}

void loop() {

  float valor1, valor2, valor3, valor4, media, reducao;

  lcd.print("Insira valor 1:");

  valor1 = obterValor();

  lcd.print("Insira valor 2:");

  valor2 = obterValor();

  lcd.print("Insira valor 3:");

  valor3 = obterValor();

  media = (valor1 + valor2 + valor3) / 3;

  lcd.clear();

  lcd.print("Media: R$");

  lcd.setCursor(0, 1);

  lcd.print(media, 2); 

  delay(3000);

  lcd.clear();

  lcd.print("Insira valor 4:");

  valor4 = obterValor();

  reducao = ((media - valor4) / media) * 100;

  lcd.clear();

  lcd.print("Reducao: ");

  lcd.setCursor(0, 1);

  lcd.print(reducao, 1);

  lcd.print("%");

  delay(3000);

  lcd.clear();

  apagarTodosLeds();


  if (reducao < 15) {

    lcd.print("Abaixo");

    digitalWrite(ledVermelho, HIGH); 

  } else if (reducao >= 15 && reducao < 25) {

    lcd.print("Meta 1 cumprida!");

    digitalWrite(ledLaranja, HIGH);

  } else if (reducao >= 25 && reducao < 30) {

    lcd.print("Meta 2 cumprida!");

    digitalWrite(ledAmarelo, HIGH);

  } else {

    lcd.print("Meta 3 cumprida!");

    digitalWrite(ledVerde, HIGH);

  }

  delay(5000);

  lcd.clear();
}


float obterValor() {

  float valor = 0.0;

  while (Serial.available() == 0) {

  }

  valor = Serial.parseFloat();

  Serial.read(); 

  lcd.clear();

  return valor;

}


void apagarTodosLeds() {

  digitalWrite(ledVermelho, LOW);

  digitalWrite(ledLaranja, LOW);

  digitalWrite(ledAmarelo, LOW);

  digitalWrite(ledVerde, LOW);

}
