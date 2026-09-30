        
# Tecnicas Digitales D3E5

# Descripción
 Este es el repositorio de la asignatura tecnicas digitales.

# Integrantes
* [Gianfranco Lopez Seguin](https://github.com/PeruLover123)
* [Jesus David Leyton Ramirez](https://github.com/RagSource)
* [Heidy Carolina Calderon Romero](https://github.com/)
  
# Informe

Indice:

1. [Decodificador de 4 bit](#decodificador-de-4-bit)
2. [7 Segmentos](#7-Segmentos)
3. [Simulaciones](#simulaciones)
4. [Evidencias de implementación](#evidencias-de-implementación)
5. [Conclusiones](#conclusiones)

## Documentación del diseño implementado

## 1. Decodificador de 4 bit

#### 1.1 Descripción

El decodificador de 4 bits es un circuito que recibe una entrada de cuatro bits y la convierte en una salida que permite representar diferentes valores numéricos. En la FPGA, este decodificador puede utilizarse para determinar qué número debe mostrarse en el display de 7 segmentos. Dependiendo de la combinación de los cuatro bits de entrada, el sistema identifica el valor correspondiente y activa los segmentos necesarios para mostrarlo. De esta manera, se puede controlar el display de forma sencilla mediante la programación de la FPGA.

#### 1.2 Diagramas

![Diagrama 1](img/imagen1.jpg)

## 2. 7 Segmentos

#### 2.1 Descripción

El display de 7 segmentos integrado en la tarjeta FPGA permite mostrar diferentes números utilizando siete segmentos LED, identificados como a, b, c, d, e, f y g. En este caso, no es necesario conectar un display externo, ya que la propia tarjeta FPGA cuenta con uno y sus segmentos están conectados directamente a pines de la FPGA. Mediante el código HDL, se controla el estado de cada segmento para formar los números del 0 al 9. Al tratarse de un display de ánodo común, los segmentos se activan mediante un nivel lógico bajo (0) y se desactivan con un nivel lógico alto (1).

#### 2.2 Diagramas

## Simulaciones

### 1. Simulacion de Decodificador de 4 bit

![Diagrama 2](img/imagen2.png)

## Evidencias de implementación



## Conclusiones


