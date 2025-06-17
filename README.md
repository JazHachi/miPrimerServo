# Código pre-examen
mi primer servo controlado con arduino

## Descripccion de funcionamiento

Este proyecto consistira en conectar un LDR que controle el movimiento de un Servomotor

#include <Servo.h>

Servo miServo;
const int pinSensor = A0;
const int pinServo = 9;

const int umbralSombra = 800;

void setup() {
  Serial.begin(9600);
  miServo.attach(pinServo);
  miServo.write(90);  // Posicion inicial
}

void loop() {
  int valorLuz = analogRead(pinSensor);
  Serial.println(valorLuz);

  if (valorLuz < umbralSombra) {
    Serial.println("Latido");

    // Llevar el servo al angulo inicial antes de comenzar
  miServo.write(0);
    delay(20);

    // Contraccion rapida
  for (int angulo = 0; angulo <= 110; angulo++) {
      miServo.write(angulo);
      delay(4);
    }

    // Relajacion mas lenta
  for (int angulo = 110; angulo >= 0; angulo--) {
      miServo.write(angulo);
      delay(5);
    }

    // Pausa entre latidos
  delay(5);
  } else {
    
  miServo.write(0); 
  }

  delay(5);
}



