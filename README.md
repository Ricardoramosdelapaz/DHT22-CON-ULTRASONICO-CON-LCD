# DHT22-CON-ULTRASONICO-CON-LCD

# Practica ESP32 con DHT22, HC-SR04 y LCD
Este repositorio muestra como podemos programar una ESP32 con los sensores DHT22 y HC-SR04 y al mismo tiempo una pantalla LCD que nos muestre la información recibida por ambos sensores, ademas de cierta informacion personal.

## Introducción

### Descripción

La ```ESP32``` la utilizamos en un entorno de adquisición de datos, en esta práctica ocuparemos los sensores (```DTH22 y HC-SR04```) para adquirir los datos de temperatura , humedad y distancia del entorno y una pantalla LCD para poder visualizar los datos leídos por dichoS sensorES.  Cabe aclarar que esta practica se usara un simulador llamado [WOKWI](https://https://wokwi.com/).


## Material Necesario

Para realizar esta practica necesitas lo siguiente

- [WOKWI](https://https://wokwi.com/)
- Tarjeta ESP 32
- Sensor DHT22
- Sensor HC-SR04
- Pantalla LCD 16x2 ILC



## Instrucciones

### Requisitos previos

Para poder usar este repositorio necesitas entrar a la plataforma [WOKWI](https://https://wokwi.com/).


### Instrucciones de preparación de entorno 

1. Abrir la terminal de programación y colocar la siguente programación:

```
const int Trigger = 4;   
const int Echo = 0; 
const int DHT_PIN = 15;   

#include <LiquidCrystal_I2C.h> //Libreria de LCD
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4
#include "DHTesp.h" //Libreria de DHT

DHTesp dhtSensor;
LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {

  Serial.begin(115200);
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
  lcd.init();
  lcd.backlight();
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0

}

void loop() {

  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
 
  TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 1) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");
  //delay(2000); 
  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print("cm");
  Serial.println();
  Serial.println("---");
  delay(2000);          //Hacemos una pausa de 200ms

  lcd.clear(); 
  lcd.setCursor(4, 0); //Coordenadas para imprimir en la LCD
  lcd.print("MODULO V");
  lcd.setCursor(6, 1);
  lcd.print("AIyM");
 delay(2000);

lcd.clear(); //Limpiar el texto en la LCD
  lcd.setCursor(2, 0);
  lcd.print("RICARDO RAMOS");
  lcd.setCursor(2, 1);
  lcd.print("ING. MECANICA");
  delay(2000);

 lcd.clear(); 
  lcd.setCursor(0, 0);
  lcd.print("  Temp: " + String(data.temperature, 1) + "\xDF"+"C  ");
  lcd.setCursor(0, 1);
  lcd.print(" Humidity: " + String(data.humidity, 1) + "% ");
  delay(2000);

  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Distancia: " + String(d) + "cm");
  delay(2000);

}

```
2. Instalar las librerías:
-  **DHT sensor library for ESPx**
- **LiquidCrystal I2C**

![](https://github.com/Ricardoramosdelapaz/DHT22-CON-LCD/blob/main/Captura%20lib.PNG?raw=true).

3. Hacer la conexion de **DHT2** con los sensores **ESP32 y HC-SR04**, junto con la pantalla LCD como se muestra en la siguiente imagen.

![](https://github.com/Ricardoramosdelapaz/DHT22-CON-LCD/blob/main/Captura%20con.PNG?raw=true).

### Instrucciónes de operación

1. Iniciar simulador.
2. Visualizar los datos en el monitor serial.
3. Colocar la temperatura y humedad dando *click* al sensor **DHT22**
4. colocar la distancia dando click* al sensor ultrasonico **HC-SR04**

## Resultados

Al iniciar la simulacion, verás los valores dentro del monitor serial y la pantalla LCD como se muestra en la siguente imagen.

![](https://github.com/Ricardoramosdelapaz/DHT22-CON-LCD/blob/main/res.PNG?raw=true).



# Créditos

Desarrollado por Ing. Ricardo Ramos De la paz

- [GitHub](https://github.com/Ricardoramosdelapaz)
