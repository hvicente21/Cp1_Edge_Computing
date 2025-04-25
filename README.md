# Sistema de Monitoramento de Luminosidade com Arduino
Este projeto implementa o Checkpoint 01 do caso “Vinheria Agnello” para monitorar a luminosidade de um ambiente de armazenamento de vinhos. Utiliza um sensor LDR, três LEDs de status e um buzzer, tudo simulado no Tinkercad e documentado em Arduino C/C++.
# Visão geral
O objetivo desse projeto se trata em capturar valores de luminosidade e sinalizar, via LEDs e buzzer, quando o ambiente está dentro de parâmetros aceitáveis, em alerta ou em condição crítica. A motivação para se criar um projeto como esse é porque as diversas condições de luz podem afetar a qualidade do vinho, e este sistema alerta quando a luminosidade ultrapassa faixas seguras.

# Componentes

- *Arduino Uno*  
- *Sensor de luminosidade (LDR)*  
- *Resistor de 10 kΩ* (para divisor de tensão do LDR)  
- *LED Verde* (OK)  
- *LED Amarelo* (Alerta)  
- *LED Vermelho* (Problema)  
- *Resistores de 220 Ω* (para cada LED)  
- *Buzzer passivo*  
- *Protoboard e jumpers*

# CODIGO DO ARDUINO

int led_3 = 13; // LED Vermelho - Problema
int led_2 = 12; // LED Amarelo - Alerta
int led_1 = 11; // LED Verde - OK
int ldr = A0;   // Entrada analógica para o sensor LDR
int ldrVal = 0;
int piezo = 2;  // Buzzer
 
void setup() {
  Serial.begin(9600);
  pinMode(led_1, OUTPUT);
  pinMode(led_2, OUTPUT);
  pinMode(led_3, OUTPUT);
  pinMode(piezo, OUTPUT);
}
 
void loop() {
  ldrVal = analogRead(ldr); // Leitura do valor de luminosidade
  Serial.println(ldrVal); // Exibe no monitor serial
 
  if (ldrVal <200) { // Ambiente escuro - OK
    digitalWrite(piezo, HIGH);
    digitalWrite(led_3, HIGH);
    digitalWrite(led_2, LOW);
    digitalWrite(led_1, LOW);
  } else if (ldrVal < 600) { // Alerta
    digitalWrite(led_1, LOW);
    digitalWrite(led_3, LOW);
    digitalWrite(led_2, HIGH);
    digitalWrite(piezo, HIGH);
    delay(100); // Buzzer soa por 3 segundos
    digitalWrite(piezo, LOW);
  } else { // Muita luz - Problema
    digitalWrite(led_1, HIGH);
    digitalWrite(led_2, LOW);
    digitalWrite(led_3, LOW);
    digitalWrite(piezo, LOW); // Alarme
  }
}

# LINK TINKERCAD
https://www.tinkercad.com/things/9ekSgkH0Qzu-cp1edgecomputing-2/editel?returnTo=https%3A%2F%2Fwww.tinkercad.com%2Fdashboard&sharecode=H-0n_tPBmX1mYFvxORChFUasPD_-DNlzyGDCBBhnkc4
