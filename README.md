## 📋 Documentación del DOJO Nº2 Sistemas de procesamiento de datss - UTN Tecnicatura superior en Programación.  

Trabajo práctico donde se busca simular el recorrido de las estaciones de subte de la linea C en Buenos Aires.

![Imagen no encontrada](./img/ArduinoTinkercad.jpg "Tinkercad")

## Autores ⌨️
***
* **Martin Garcia** 
* **Camila Gargiulo** 
* **Massimo Bosco** 
* **Emmanuel Hermosilla** 
* **Nicolás Hruszczak** 
 
with ❤️ 

## Proyecto: Señalizador de estaciónes de subte.

***
![Imagen no encontrada](./img/Arduino-conexiones.png "DOJO Nº2 SPD - UTN")

## Comenzando 🚀
***

En este proyecto simula un viaje en la línea C del subterraneo de Buenos Aires,  desde la estación Constitución hasta la de Moreno:
- Al presionar el pulsador da por comienzo la simulación.
- El sistema consta de 3 indicadores:   
  - Luces leds que indican la estación en donde se encuentra el pasajero.  
  - En el display se muestran la cantidad de estaciones faltantes para llegar hasta destino.
  - Una señal sonora (buzzer) indica que el subterraneo llega a una estación. 
 

Las siguientes instrucciones te permitirán comprender el funcionamiento del proyecto. Además, se incluye el enlace del proyecto en TinkerCad para poder copiarlo y modificarlo: 

[Link del proyecto en Tinkercad ](https://www.tinkercad.com/things/8A87vszVlUQ "Enlace del proyecto en Tinkercad")

## Consigna 🔩

Consigna SUBTE:
La empresa  “UTN FRA Robotics” ganó la licitación de un proyecto, y deberá Implementar un sistema que permita al usuario saber a qué estación de subte está llegando, aparte  el sistema muestra las estaciones que faltan hasta llegar a destino, para ello debemos utilizar 4 LEDs y el display de 7 segmentos.  
Esta vez el buzzer deberá emitir un sonido diferente cada vez que se llegue a una estación.
El sistema deberá arrancar apagado, luego de presionar el botón empezará y hará lo pedido.

Para realizar el proyecto deberán usar mínimamente:  
1 ARDUINO UNO.  
1 Display 7 segmentos.  
4 LEDS.  
1 BUZZER (Piezo).  
1 BOTÓN  
RESISTENCIAS NECESARIAS PARA CADA COMPONENTE.

## Código del programa: 🔩

* * *

 ~~~ C (Lenguaje del código)
#define ledConstitucion 6
#define ledSanJuan 5
#define ledIndependencia 4
#define ledMoreno 3
#define buzzer 2
#define pulsador 19
#define A 7
#define B 8
#define C 9
#define D 10
#define E 11
#define F 12
#define G 13


void setup()
{
  Serial.begin(9600);
  pinMode(ledConstitucion, OUTPUT);
  pinMode(ledSanJuan, OUTPUT);
  pinMode(ledIndependencia, OUTPUT);
  pinMode(ledMoreno, OUTPUT);
  pinMode(buzzer, OUTPUT);
  pinMode(pulsador, INPUT_PULLUP);
  pinMode(A, OUTPUT);
  pinMode(B, OUTPUT);
  pinMode(C, OUTPUT);
  pinMode(D, OUTPUT);
  pinMode(E, OUTPUT);
  pinMode(F, OUTPUT);
  pinMode(G, OUTPUT);
}

// INICIO FUNCIONES
void recorrido(int numeroEstacion, int tiempoEspera)
{

	switch(numeroEstacion)
    {
      case 1:
      	uno(1);
        digitalWrite(6, 1);// Constitución
      	digitalWrite(buzzer,1);
        tone(buzzer,1200,200);
      	Serial.println("Estación Constitucion.");
        break;
      case 2:
        dos(1);
        digitalWrite(5, 1); // San Juan
      	digitalWrite(buzzer,1);
		tone(buzzer,1000,200);
      	Serial.println("Estacion San Juan.");
        break;
      case 3:
        tres(1);
        digitalWrite(4, 1); // Independencia
      	digitalWrite(buzzer,1);
      	tone(buzzer,700,200);
      	Serial.println("Estacion Independencia.");
        break;
      case 4:
        cuatro(1);
      	digitalWrite(3, 1); // Moreno
      	digitalWrite(buzzer,1);
      	tone(buzzer,500,200);
      	Serial.println("Estacion Moreno.");
        break;
    }
	
  	displayOff();
    ledEstacionesOff();
  	digitalWrite(buzzer, 0);
	delay(tiempoEspera);

}


void ledEstacionesOff()
{
  digitalWrite(6, 0);
  digitalWrite(5, 0);
  digitalWrite(4, 0);
  digitalWrite(3, 0);
}

void displayOff()
{
  digitalWrite(A, LOW);
  digitalWrite(B, LOW);
  digitalWrite(C, LOW);
  digitalWrite(D, LOW);
  digitalWrite(E, LOW);
  digitalWrite(F, LOW);
  digitalWrite(G, LOW);
}

void cero(int onOff)
{
  digitalWrite(A, onOff);
  digitalWrite(B, onOff);
  digitalWrite(C, onOff);
  digitalWrite(D, onOff);
  digitalWrite(E, onOff);
  digitalWrite(F, onOff);
}

void uno(int onOff)
{
  digitalWrite(B, onOff);
  digitalWrite(C, onOff);
}

void dos(int onOff)
{
  digitalWrite(A, onOff);
  digitalWrite(B, onOff);
  digitalWrite(D, onOff);
  digitalWrite(E, onOff);
  digitalWrite(G, onOff);
}

void tres(int onOff)
{
  digitalWrite(A, onOff);
  digitalWrite(B, onOff);
  digitalWrite(C, onOff);
  digitalWrite(D, onOff);
  digitalWrite(G, onOff);
}

void cuatro(int onOff)
{
  
  digitalWrite(B, onOff);
  digitalWrite(C, onOff);
  digitalWrite(G, onOff);
  digitalWrite(F, onOff);
}

void todos(int onOff)
{
  digitalWrite(A, HIGH);
  digitalWrite(B, HIGH);
  digitalWrite(C, HIGH);
  digitalWrite(D, HIGH);
  digitalWrite(E, HIGH);
  digitalWrite(F, HIGH);
  digitalWrite(G, HIGH);
}

// FIN FUNCIONES




// INICIO LOOP PRINCIPAL
void loop()
{
  int estadoBoton = digitalRead(pulsador); // 1 o 0
  if (estadoBoton == 0)
  {
  
   	for (int i=0; i <= 4; i++) // Muestra las estaciones restantes.
   	{
      	recorrido(i, 1000);
   	}
    Serial.println("Fin del recorrido.");
  }	
} // FIN LOOP
 ~~~

### void loop():
~~~ C
 void loop()
{
  int estadoBoton = digitalRead(pulsador); // 1 o 0
  if (estadoBoton == 0)
  {
  
   	for (int i=0; i <= 4; i++) // Muestra las estaciones restantes.
   	{
      	recorrido(i, 1000);
   	}
    Serial.println("Fin del recorrido.");
  }	
} 
~~~
- Si se presiona el pulsador da comienzo al viaje:   
    - Se anuncia por monitor serial el inicio del viaje.
    - Inicia un contador del 0 al 4 indicando la estación en la que se encuentra.  
    - El monitor serial anuncia al parar en cada estación y al final del recorrido.


## 🤖 Link al proyecto 
---

 Proyecto [Estaciones de subte ](https://www.tinkercad.com/things/8A87vszVlUQ "Enlace del proyecto en Tinkercad") TinkerCad.
 - - - 

##  📘 Fuentes
---
- [Tecnicatura Universitaria en Programación - UTN](http://www.sistemas-utnfra.com.ar/#/pages/carrera/tecnico-programacion/resumen).
