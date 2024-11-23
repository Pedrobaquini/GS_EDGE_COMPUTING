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
Conecte os anodos dos LEDs aos pinos digitais 8 (vermelho), 9 (laranja), 10 (amarelo) e 11 (verde).
Conecte os cátodos ao GND.

Dependências e Configuração

### Bibliotecas Necessárias

LiquidCrystal_I2C

### Configuração no WOKWI

No arquivo JSON do projeto WOKWI, adicione o seguinte codigo para que o Monitor Serial inicie aberto e aceite entradas:
 "serialMonitor": { "display": "always", "newline": "lf" },
