## <FONT COLOR=#007575>**Aspectos destacados**</font>
Se dispone de un tablero con una configuración de cuadrados de 5x5 cm numerados (el número está en el centro en un fuente de 12 puntos) con esta estructura: 
1       2       3
11     12     13
21      22     23
24      40      41
Los cuadrados están separados 13 mm en horizontal y 10 mm en vertical.
La idea es definir un juego que comience en el 1 y recorra el tablero asignando a los números 24, 40 y 41 el inicio, el fin y alguna otra tarea. No hay que dar nombre a las celdas de la matriz pues ya lo tienen con los números.
El juego lo debe resolver un robot capaz de identificar cada cuadrado por su número o ID. Dicho robot también sabe la orientación en grados que tiene sobre el tablero que sería así respecto a la parte delantera del robot situado en 12 mirando hacia 22:
12-Robot orientado a 22 -> 0 grados; 13 -> 90 grados; 2 -> 180 grados y 11 -> 270 grados.

Misión de Reconocimiento

Objetivo:
El robot comienza en la casilla 1 y debe completar una misión que incluye:
Recoger un objeto en la casilla 24 (inicio del objetivo).
Realizar un escaneo de datos en la casilla 41 (tarea intermedia).
Transportar y entregar el objeto en la casilla 40 (final de la misión).
El robot debe seguir el camino óptimo o cumplir con restricciones predefinidas (dependiendo del nivel de dificultad), reconociendo cada celda por su número (ID) y guiándose por su orientación.

Orientación del Robot

Según la orientación estándar:
Frente del robot en 12 mirando a 22 → 0° (Sur).
Mirando a 13 → 90° (Este).
Mirando a 2 → 180° (Norte).
Mirando a 11 → 270° (Oeste).

| Dirección del robot (desde 12) | Casilla destino | Nueva orientación | Ángulo   |
| ------------------------------ | --------------- | ----------------- | -------- |
| **Frente mirando a 22**        | **Norte**       | Frente            | **0°**   |
| **Frente mirando a 13**        | **Este**        | Derecha           | **90°**  |
| **Frente mirando a 2**         | **Sur**         | Atrás             | **180°** |
| **Frente mirando a 11**        | **Oeste**       | Izquierda         | **270°** |

Comandos disponibles:

avanzar() → se mueve una casilla en la dirección actual.
girar_derecha() → gira 90° en sentido horario.
girar_izquierda() → gira 90° en sentido antihorario.
esperar(segundos) → pausa de tiempo.
recoger() → activa señal de carga.
entregar() → finaliza misión.
escaneo() → realiza una lectura o espera en casilla.

acciones = [
    girar_izquierda,   # Desde 1 mirando a 2 (Norte 0°), gira a 270° (Oeste hacia 11)
    avanzar,           # Va a 11
    girar_izquierda,   # Mira hacia 21 (Sur, 180°)
    avanzar,           # Va a 21
    avanzar,           # Va a 24
    recoger,           # Recoge objeto
    girar_derecha,     # Mira a 40 (Este, 90°)
    avanzar,           # Va a 40
    avanzar,           # Va a 41
    escaneo,           # Escanea
    girar_izquierda,   # Mira hacia 40 (Norte, 0°)
    avanzar,           # Va a 40
    entregar           # Entrega objeto
]

Variables que usarás

posición → para guardar el ID de la casilla en la que está el robot (empieza en 1)

orientación → para guardar uno de {0°, 90°, 180°, 270°}, con la convención que definimos:

0° = Norte

90° = Este

180° = Sur

270° = Oeste

objetivo → “ninguno” / “24 recogida” / “41 escaneo” / “40 entrega”

acciones → lista de acciones pendientes, como “girar”, “avanzar”, “recoger”, etc.

índice_acciones → para llevar un seguimiento de en qué acción está

Lógica general

Al iniciar, configurar posición = 1, orientación = 180° (porque empieza mirando hacia la casilla 2 que es “Sur” bajo nuestra convención), objetivo = "24 recogida".

Definir la secuencia de acciones necesarias: la lista que determine moverse de casilla en casilla hasta 24, recoger, luego hasta 41, escanear, luego hasta 40, entregar.

Cada vez que se pulsa el Botón A, se toma la acción acciones[índice_acciones], se ejecuta, se incrementa índice_acciones.

Comprobar al llegar a ciertas casillas si se debe cambiar objetivo (por ejemplo, al llegar a 24 cambiar a “41 escaneo”, luego a “40 entrega”).

cuando se inicia:
  posición ← 1
  orientación ← 180   // mirando hacia casilla 2
  objetivo ← "24 recogida"
  acciones ← [
    girar_izquierda, avanzar, girar_izquierda, avanzar, avanzar,    // mover de 1 → 11 → 21 → 24
    recoger,
    girar_derecha, avanzar, avanzar,                                // ir de 24 → 40 → 41, asumiento rutas válidas
    escaneo,
    girar_izquierda, avanzar,                                       // volver de 41 → 40
    entregar
  ]
  índice_acciones ← 1

*************************************

Supuestos

Para este programa asumo:

Tienes la biblioteca de bloques de CoCube instalada. (Mover, girar, botón A, orientación, posición) 

Que CoCube puede detectar su orientación y posición mediante CoMaps/CoTags etc. 

Que hay un bloque para detectar “Botón A presionado” en CoCube. (Botón físico trasero A) 


Bloques / Componentes que vas a usar

Aquí una lista de bloques que necesitarás:
* Cuando se inicia / “on start”
* Cuando Botón A presionado (“when button A pressed”)

Bloques de movimiento:
* avanzar() → mover una casilla (o distancia breve) en la orientación actual
* girar_derecha() → girar 90° horario
* girar_izquierda() → girar 90° antihorario

Bloques de tarea especial:

* recoger()
* escaneo()
* entregar()

Bloque de espera / pausa: esperar(segundos)

Variables:

* posición (inicializada en 1)
* orientación (inicializada en lo que corresponda; con tu convención: 0° = Norte, 90° = Este, etc.)
* acciones (una lista)
* índice_acciones

Estructura del programa

1. Bloque “Cuando se inicia”

Configura las variables:

posición ← 1
orientación ← 0° (supongamos que empieza mirando hacia casilla 22 que aquí definimos como Norte)
índice_acciones ← 1
acciones ← lista con los pasos (como antes):

2. Bloque “Cuando Botón A presionado”

Se ejecuta cada vez que presionas botón A:

3. Bloque “ejecutar_acción(acción)”

Un bloque que realice la acción correspondiente:

4. Bloque auxiliar: mover_un_paso_en_orientación(orientación)

Este bloque/método debe saber, para cada orientación, a qué casilla adyacente ir. Tendrás que mapear internamente el tablero:

Ejemplo:

si posición = 1 y orientación = Este (90°) entonces nueva posición ← 2
si posición = 1 y orientación = Sur (180°) entonces nueva posición ← 11

Montaje visual en MicroBlocks

En MicroBlocks tendrías algo así:

En la paleta de “Control”: bloques cuando se inicia, cuando Botón A presionado

En la paleta de “Variables”: crear variables posición, orientación, índice_acciones, acciones

En la paleta de “Listas”: bloque lista para acciones

Bloques de acción específicos de CoCube de movimiento y tareas

+---------------------------------------------------------+
|                   Bloque “Cuando se inicia”            |
|---------------------------------------------------------|
| posición ← 1                                           |
| orientación ← 0°     // Norte                          |
| índice_acciones ← 1                                    |
| acciones ← lista [                                       |
|    girar_izquierda, avanzar, girar_izquierda, avanzar, avanzar, |
|    recoger,                                             |
|    girar_derecha, avanzar, avanzar,                     |
|    escaneo,                                             |
|    girar_izquierda, avanzar,                            |
|    entregar                                             |
| ]                                                       |
+---------------------------------------------------------+

          │
          │   (dependiente del botón A)
          ▼

+---------------------------------------------------------+
|           Bloque “Cuando Botón A presionado”           |
|---------------------------------------------------------|
| si índice_acciones ≤ longitud(acciones) entonces       |
|    acción_actual ← acciones[índice_acciones]            |
|    ejecutar_acción(acción_actual)                      |
|    índice_acciones ← índice_acciones + 1               |
| fin si                                                 |
+---------------------------------------------------------+

          │
          │   (llama a:)

          ▼

+---------------------------------------------------------+
|        Bloque “ejecutar_acción(acción)”                |
|---------------------------------------------------------|
| si acción = "avanzar" entonces                          |
|    mover_un_paso_en_orientación(orientación)            |
|    actualizar posición según orientación                |
| sino si acción = "girar_derecha" entonces               |
|    orientación ← (orientación + 90) mod 360             |
| sino si acción = "girar_izquierda" entonces             |
|    orientación ← (orientación − 90) mod 360             |
|    si orientación < 0 entonces orientación ← orientación + 360 |
| sino si acción = "recoger" entonces                     |
|    [acción de recolección]                              |
| sino si acción = "escaneo" entonces                      |
|    esperar(3 segundos)                                   |
| sino si acción = "entregar" entonces                     |
|    [acción de entrega / señal fin]                       |
| fin si                                                  |
+---------------------------------------------------------+

          │
          │   (auxiliar si “avanzar”)

          ▼

+---------------------------------------------------------+
|     Bloque auxiliar “mover_un_paso_en_orientación(orientación)” |
|---------------------------------------------------------|
| // aquí condicionales para cada casilla + orientación     |
| si posición = 1 y orientación = Este entonces posición ← 2 |
| si posición = 1 y orientación = Sur entonces posición ← 11 |
| … etc. para todas las combinaciones                    |
+---------------------------------------------------------+
