1-Identifique as entradas e saidas do sistema:

3 botões = sinais digitais 
1 potenciometro = sinal analogico
saidas:
LEDs acionados pelos arduinos conforme a lógica

2-Apresente todos os componentes do sistema e para que eles servem:

arduino uno- controlador do sistema lendo as entradas e definindo as saidas 
3 botões envia-comandos digitais (alto = ativo) 
1 potenciometro-controla a intencidade dos LEDs gerando um valor analogico
resistores, impedem o circuito e estabilizam os sinais LEDs ( entradas 9, 10 e 11 )
jumpers-montagem do circuito

3-Apresente as regras de funcionamento a serem implementadas:
3 luzes que são controladas por 3 botões individuais 
1 botão controla a luz vermelha
outro a luz verde
e outro a luz amarela
não é possivel precionar 2 botões ao mesmo tempo
o potenciometro controla a intencidade do LED que estiver ativo

4-Explique como você utilizaria estruturas if para controlar o sistema:
o circuito usa if para averiguar se cada botão esta pressionado.
EX-if (botao1 == alto)=executar ações LED 11 if (botao2 == alto)=executar ações LED 10 if (botao3 == alto)=executar ações LED 9 

IMAGEM DO CIRCUITO
<p allign="center">
<img src"imagem_2026-05-05_213803332.png" width="50%">


CODIGO DO CIRCUITO:
// C++ code
//
int controleINTENSIDADE = 0;

int bot1 = 0;

int bot2 = 0;

int bot3 = 0;

void setup()
{
  pinMode(A1, INPUT);
  pinMode(2, INPUT);
  pinMode(3, INPUT);
  pinMode(4, INPUT);
  pinMode(11, OUTPUT);
  pinMode(10, OUTPUT);
  pinMode(9, OUTPUT);
}

void loop()
{
  controleINTENSIDADE = analogRead(A1);
  bot1 = digitalRead(2);
  bot2 = digitalRead(3);
  bot3 = digitalRead(4);
  if (bot1 == HIGH) {
    digitalWrite(11, HIGH);
    digitalWrite(10, LOW);
    digitalWrite(9, LOW);
    analogWrite(11, map(controleINTENSIDADE, 0, 1023, 0, 200));
  } else {
    digitalWrite(9, LOW);
    digitalWrite(11, LOW);
  }
  if (bot2 == HIGH) {
    digitalWrite(10, HIGH);
    digitalWrite(11, HIGH);
    digitalWrite(9, HIGH);
    analogWrite(11, map(controleINTENSIDADE, 0, 1023, 0, 241));
    analogWrite(10, map(controleINTENSIDADE, 0, 1023, 0, 7));
    analogWrite(9, map(controleINTENSIDADE, 0, 1023, 0, 244));
  } else {
    digitalWrite(9, LOW);
    digitalWrite(10, LOW);
  }
  if (bot3 == HIGH) {
    digitalWrite(9, HIGH);
    digitalWrite(10, LOW);
    digitalWrite(11, LOW);
    analogWrite(9, map(controleINTENSIDADE, 0, 1023, 0, 200));
  } else {
    digitalWrite(9, LOW);
  }
  delay(10); // Delay a little bit to improve simulation performance
}
