# PRACTICA-NIVEL-DE-AGUA
ESTE REPOSITORIO MUESTRA EL ENCENDIDO DE LUCES LED POR MEDIO DE UN NIVEL DE AGUA CON AYUDA DE UN ULTRASONICO

## INTRODUCCION

### DESCRIPCION

La Esp32 la utilizamos en un entorno de adquision de datos, lo cual en esta practica ocuparemos un ultrasonico para adquirir la distancia. Esta distancia nos ayudara para representar el nivel de agua:
- 1% AL 25%
- 26% AL 50%
- 51% AL 75%
- 76% AL 99%
- VACIO
- LLENO

Este nivel de agua podrá ser representado por medio de leds con sus respectivas resistencias.
Se agregará asi mismo un LCD I2C para observar dichos datos en cada cierto tiempo; Cabe aclarar que esta practica se usara un simulador llamado WOKWI.

## MATERIAL NECESARIO

Para realizar esta practica necesitas lo siguiente:

-[WOKWI](https://wokwi.com/)

-Tarjeta ESP 32

-HC-SR04 ULTRASONIC Distance sensor

-LCD 16X2 (I2C)

-6 LEDS

-6 RESISTENCIAS DE 220 OHMS

## INSTRUCCIONES

### Requisitos previos

Para poder usar este repositorio necesitas entrar a la plataforma [WOKWI](https://wokwi.com/)

### Instrucciones de preparación de entorno

1.Abrir la terminal de programación y colocar la siguente programación:

```
// defines pins numbers
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4
const int trigPin = 4;
const int echoPin = 15;
const int led1 = 16;
const int led2 = 0;
const int led3 = 2;
const int led4 = 17;
const int led5 = 5;
const int led6 = 18;
// defines variables
long duration;
int distance;
int safetyDistance;
LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);
void setup() {
pinMode(trigPin, OUTPUT); // Sets the trigPin as an Output
pinMode(echoPin, INPUT); // Sets the echoPin as an Input
pinMode(led1, OUTPUT);
pinMode(led2, OUTPUT);
pinMode(led3, OUTPUT);
pinMode(led4, OUTPUT);
pinMode(led5, OUTPUT);
pinMode(led6, OUTPUT);
Serial.begin(9600); // Starts the serial communication
lcd.init();
lcd.backlight();
  }
void loop() {
  long t; //timepo que demora en llegar el eco
long d; //distancia en centimetros
// Clears the trigPin
digitalWrite(trigPin, LOW);
delayMicroseconds(2);
// Sets the trigPin on HIGH state for 10 micro seconds
digitalWrite(trigPin, HIGH);
delayMicroseconds(10);
digitalWrite(trigPin, LOW);
// Reads the echoPin, returns the sound wave travel time in microseconds
duration = pulseIn(echoPin, HIGH);
// Calculating the distance
distance= duration*0.034/2; 
safetyDistance = distance;
if (safetyDistance>=3 && safetyDistance<=100)
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
  digitalWrite(led5, LOW);
  digitalWrite(led6, LOW); 
}
else if(safetyDistance>=101 && safetyDistance<=200) 
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
  digitalWrite(led5, LOW);
   digitalWrite(led6, LOW);
}
else if(safetyDistance>=201 && safetyDistance<=300)
{
 digitalWrite(led1,  HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, LOW);
  digitalWrite(led5, LOW);
   digitalWrite(led6, LOW);

}
else if(safetyDistance>=301 && safetyDistance<=398)
{
 digitalWrite(led1,  HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, HIGH);
  digitalWrite(led5, LOW);
   digitalWrite(led6, LOW);
}
else if(safetyDistance>=399 && safetyDistance<=400)
{
 digitalWrite(led1,  LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
  digitalWrite(led5, HIGH);
   digitalWrite(led6, LOW);
}
else if(safetyDistance>=1 && safetyDistance<=2)
{
 digitalWrite(led1,  LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
  digitalWrite(led5, LOW);
   digitalWrite(led6, HIGH);
}
else
{
 digitalWrite(led1,  LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
  digitalWrite(led5, LOW);
   digitalWrite(led6, LOW);
}
// Prints the distance on the Serial Monitor
 Serial.print("Distance: ");
Serial.println(distance);
delay (2000);
  lcd.setCursor(0, 0);
  lcd.print("   DIPLOMADO");
  lcd.setCursor(0, 1); 
  lcd.print(" AUTOMATIZACION");
   delay(2000);
  lcd.clear();
   lcd.setCursor(0, 0);
  lcd.print(" JAQUELINE R.H");
  lcd.setCursor(0, 1); 
  lcd.print("   INDUSTRIAL");
   delay(2000);
  lcd.clear();
   lcd.setCursor(0, 0);
  lcd.print("   07-06-2025");
 delay(2000);
  lcd.clear();
   if (safetyDistance>=3 && safetyDistance<=100)
{
  lcd.setCursor(0,0);
  lcd.print("Distancia: "+ String (distance)+"cm");
  lcd.setCursor(0,1);
  lcd.print("   1% AL 25%");
  delay(2000);
  lcd.clear();
  }
else if(safetyDistance>=101 && safetyDistance<=200) 
{ lcd.setCursor(0,0);
  lcd.print("Distancia: "+ String (distance)+"cm");
  lcd.setCursor(0,1);
    lcd.print("   26% AL 50%");
  delay(2000);
  lcd.clear();
}
else if(safetyDistance>=201 && safetyDistance<=300) 
{
  lcd.setCursor(0,0);
  lcd.print("Distancia: "+ String (distance)+"cm");
  lcd.setCursor(0,1);
    lcd.print("   51% AL 75%");
  delay(2000);
  lcd.clear();
}
else if(safetyDistance>=301 && safetyDistance<=398) 
{
   lcd.setCursor(0,0);
  lcd.print("Distancia: "+ String (distance)+"cm");
  lcd.setCursor(0,1);
   lcd.print("   76% AL 99%");
  delay(2000);
  lcd.clear();
}
else if(safetyDistance>=1 && safetyDistance<=2) 
{
   lcd.setCursor(0,0);
  lcd.print("Distancia: "+ String (distance)+"cm");
  lcd.setCursor(0,1);
   lcd.print("    VACIO");
  delay(2000);
   lcd.clear();
   }
   else if(safetyDistance>=399 && safetyDistance<=400) 
{
   lcd.setCursor(0,0);
  lcd.print("Distancia: "+ String (distance)+"cm");
  lcd.setCursor(0,1);
   lcd.print("     LLENO");
  delay(2000);
   lcd.clear();
   }
}
```


2. Instalar la libreria de LiquidCrystal I2C como se muestra en la siguiente imagen



![]()



4.Hacer la conexion de HC-SR04 ULTRASONIC Distance sensor
 con la ESP32 como se muestra en la siguente imagen.

![](https://github.com/jaquelineriverh/PRACTICA-NIVEL-DE-AGUA/blob/main/ULTRASONICO%20CONEXION.png)


5.Hacer la conexion de LCD con la ESP32 como se muestra en la siguente imagen.


![](https://github.com/jaquelineriverh/PRACTICA-NIVEL-DE-AGUA/blob/main/ULTRASONIC%20CON%20LCD.png)


6. Agregar los 6 focos led con sus respectivas resistencias con la conexion ESP32, estos se representaran con colores, los azules para un nivel de agua, el verde lleno y rojo para el vacio.


![](https://github.com/jaquelineriverh/PRACTICA-NIVEL-DE-AGUA/blob/main/focos%20led.png)



### Instrucciónes de operación
1.Iniciar simulador.

2.Visualizar los datos en el LCD 16x2 y en los focos led

3.Colocar LA DISTANCIA a simular dando doble click al HC-SR04 ULTRASONIC Distance sensor


## Resultados

Cuando haya funcionado, verás los valores dentro del LCD 16x2 y en los focos led como se muestra en la siguente imagen.

**VACIO**


![](https://github.com/jaquelineriverh/PRACTICA-NIVEL-DE-AGUA/blob/main/vacio.png)

1% AL 25%


![]()
![]()
![]()
![]()
![]()

### EVIDENCIAS






https://github.com/user-attachments/assets/0810382c-b727-44f3-96a9-bb41cb41fe4a







# Créditos

Desarrollado por **RIVERA HERNANDEZ JAQUELINE**

-[GITHUB](https://github.com/jaquelineriverh)
