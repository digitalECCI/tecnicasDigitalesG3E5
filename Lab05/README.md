
# Tecnicas Digitales D3E5

# Descripción
 Este es el repositorio de la asignatura tecnicas digitales.

# Integrantes
* [Gianfranco Lopez Seguin](https://github.com/PeruLover123)
* [Jesus David Leyton Ramirez](https://github.com/RagSource)
* [Heidy Carolina Calderon Romero](https://github.com/)

# Informe

Indice:

1. [Divisor de frecuencia](#Divisor-de-frecuencia)
2. [Selector de Estados (FSM)](#Selector-de-Estados-FSM)
3. [Contador Unificado](#Contador-Unificado)
4. [Decodificador de Salidas](#Decodificador-de-Salidas)
5. [Semáforo Inteligente](#Semáforo-Inteligente)
6. [Evidencias de implementación](#evidencias-de-implementación)
7. [Conclusiones](#conclusiones)

## 1. Divisor de frecuencia

#### 1.1 Descripción

Generar un pulso periódico de habilitación (tick) de 1 Hz a partir del reloj principal de 50 MHz (clk).

Funcionamiento:

Utiliza un contador interno de **26 bits** (`reg [25:0] count`) que se incrementa en cada flanco de subida de clk. Se requieren 26 bits que es insuficiente para contar 50 millones de ciclos.

Cuando count alcanza el valor exacto **49999999**, reinicia el contador a 0 y genera un pulso `tick = 1` que dura solo un ciclo de reloj. En los demás ciclos, tick permanece en 0, sirviendo como base de tiempo precisa para el semáforo.

#### 1.2 Diagramas
![Diagrama 1](img/Div.png)

## 2. Selector de Estados (FSM)

#### 2.1 Descripción

Controlar la secuencia cíclica del semáforo mediante una Máquina de Estado Finito (FSM) tipo Moore, donde las salidas dependen exclusivamente del estado actual.

Funcionamiento:

Lógica secuencial (`always @(posedge clk)`): Evalúa el estado actual (`state`) y el contador de tiempo para determinar el siguiente estado (`next_state`).

  **Estados de 10s (Verde/Rojo):** Transicionan cuando el contador interno llega a 9 (0 a 9 = 10 ciclos).
  
  **Estados de 3s (Amarillos):** Transicionan cuando el contador interno llega a 2 (0 a 2 = 3 ciclos).

  #### 2.2 Diagramas

![Diagrama 1](img/Traffic.png)

## 3. Contador Unificado

#### 3.1 Descripción

Implementar un sistema de conteo de segundos compartido para todos los estados de la FSM, optimizando el uso de registros en la FPGA.

Funcionamiento:

Si `rst` está activo, el contador `count` se fuerza a 0.

Mientras la señal `tick` (1 Hz) sea verdadera:

Si se cumple la condición de fin de tiempo para el estado actual (ej: `state==VERDE && count==9`), se reinicia a 0 (rollover forzado por cambio de estado).

De lo contrario, se incrementa en 1 (`count <= count + 1`).

Si `tick` es 0, el contador conserva su valor actual, esperando el siguiente segundo.

## 4. Semáforo Inteligente

#### 4.1 Descripción

Integrar el divisor de frecuencia, el contador unificado y la FSM para representar un sistema de control vial completo con interacción peatonal.

Funcionamiento:

Instancia dos módulos principales: `divisor.v` y `traffic.v`.

Cascada de Control (Top-Level Logic):

`tick`: Recibe directamente la salida del divisor de 26 bits.

`state`: Evoluciona cíclicamente (Verde -> Amarillo -> Rojo -> Amarillo -> Verde) basado en el contador unificado.

#### 4.2 Diagramas
![Diagrama 1](img/All.png)

## Conclusiones

En conclusión, el desarrollo de este proyecto permitió poner en práctica el diseño de sistemas secuenciales complejos mediante la modularización en HDL. La implementación de un divisor de frecuencia de 26 bits demostró ser fundamental para obtener una base de tiempo precisa de 1 Hz a partir de los 50 MHz de la FPGA. Asimismo, la estrategia de unificar el contador de segundos dentro de la FSM, en lugar de usar contadores independientes por estado, optimizó significativamente el uso de recursos lógicos. Finalmente, la lógica de enclavamiento (latch) para la señal peatonal garantizó que ninguna petición se perdiera, validando la robustez del modelo Moore en aplicaciones de control vial.

