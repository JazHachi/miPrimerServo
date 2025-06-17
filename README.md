# Pre-examen de Electronica
servomotor controlado con arduino

## Descripccion de funcionamiento

Este proyecto consistira en conectar un LDR que controle el movimiento de un Servomotor. Sera utilizado para mover una escultura blanda con el ritmo de un corazon.

## Codigo
~~~
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
~~~

*el codigo de arriba tiene un latido mas mecanico, constante que no le aporta de manera positiva a la obra, uno que sea mas aleatorio y organico puede ser mejor.

## Segundo codigo
~~~
#include <Servo.h>

Servo miServo;
const int pinSensor = A0;
const int pinServo = 9;

const int umbralSombra = 800;

void setup() {
  Serial.begin(9600);
  randomSeed(analogRead(1));  // Para generar numeros aleatorios únicos
  miServo.attach(pinServo);
  miServo.write(90);  // Posición inicial
}

void loop() {
  int valorLuz = analogRead(pinSensor);
  Serial.println(valorLuz);

  if (valorLuz < umbralSombra) {
    Serial.println("Latidooo");

    // angulo maximo aleatorio entre 90 y 130
    int anguloMax = random(90, 130);

    // Velocidades aleatorias
    int velocidadContraccion = random(1, 8);  // rapido
    int velocidadRelajacion = random(4, 40);  // lento

    // probabilidad de latido doble
    int repeticiones = (random(0, 100) < 20) ? 2 : 1;

    for (int i = 0; i < repeticiones; i++) {
      // contraccion
      for (int angulo = 0; angulo <= anguloMax; angulo++) {
        miServo.write(angulo);
        delay(velocidadContraccion);
      }

      // Relajacion
      for (int angulo = anguloMax; angulo >= 0; angulo--) {
        miServo.write(angulo);
        delay(velocidadRelajacion);
      }

      delay(random(80, 500));  // Pausa aleatoria entre repeticiones
    }

    delay(random(700, 1400));  // Pausa final antes del siguiente latido
  } else {
    // Estado en reposo
    miServo.write(0);
    delay(50);
  }

  delay(10);  // Pequeño delay para estabilizar lectura
}

~~~
*Con este codigo creo que puede haber un mejor acercamineto a lo que quiero.




