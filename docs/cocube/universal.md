## <FONT COLOR=#007575>**Introducción**</font>
Se trata en realidad de dos CoMaps, uno en cada lámina, impresos en papel transparente montados sobre carpeta tipo dosier (imagen siguiente) de tamaño A3 con apertura superior y lateral.

<center>

![Carpeta tipo dosier](../img/CoCube/dosier.png)  

</center>

En una de sus caras lleva superpuesta la cuadricula de coordenadas detallada, tal y como vemos en la imagen siguiente:

<center>

![CoMap tipo dosier cara rejilla](../img/CoCube/comap_dosier_dosier_rejilla.png)  

</center>

En la otra cara solamente están visibles los valores de las coordenadas:

<center>

![CoMap tipo dosier cara coordenadas](../img/CoCube/comap_dosier_dosier_coord.png)  

</center>

No hay disponibles archivos para su descarga y se entiende que en un futuro serán comercializados.

Este elemento nos va a permitir dibujar cualquier tipo de tapete para jugar con CoCube. Dicho dibujo puede ser realizado tanto a mano alzada, con lápices de colores, como mediante software de diseño para su posterior impresión. Si se dibuja con lápices de colores es importante que los mismos no contengan carbono para evitar interferencias con el patrón de micropuntos. Este punto es bastante fácil de cumplir dado que en Europa, en los lápices de colores, sus minas suelen estar hechas a base de ceras y aceites exentas de carbono.

A continuación se muestra un gráfico con las coordenadas centrales de cada celda definida para el caso del CoMap **CON** rejilla.

<center>

![Valores de coordenadas centrales de las celdas](../img/CoCube/coordenadas_centrales_rejilla.png)  

</center>

A continuación se muestra un gráfico con las coordenadas centrales de cada celda definida para el caso del CoMap **SIN** rejilla.

<center>

![Valores de coordenadas centrales de las celdas](../img/CoCube/coordenadas_centrales.png)  

</center>

Ambos gráficos pueden servir de guía para el desarrollo de diferentes retos.

## <FONT COLOR=#007575>**Recorrer trazados**</font>
Se trata de introducir en el CoMap tipo dosier, orientado a cualquiera de sus lados, el siguiente diseño:

<center>

![Caminos o trazados de colores](../img/CoCube/caminos.png)  

</center>

Sobre un CoMap formado por 4 filas y seis columnas se han trazado los cuatro caminos de la imagen anterior, cumpliendo las siguientes condiciones:

1. Cada camino avanza de izquierda a derecha (una celda por columna).
2. Ningún camino tiene más de 3 celdas consecutivas en la misma fila.
3. Los caminos pueden cruzarse.
4. La unión de los 4 caminos cubre las 24 celdas (sin dejar ninguna libre).
5. Cada fila inicial es distinta.
6. Cada camino tiene su color y se trazan pasándo por los centros de las celdas

El conjunto con el CoMap con solo coordenadas tiene el aspecto siguiente:

<center>

![Caminos de colores + CoMap de coordenadas](../img/CoCube/caminos_coord.png)  

</center>

Y para el cajo del CoMap de rejilla el siguiente:

<center>

![Caminos de colores + CoMap de rejilla](../img/CoCube/caminos_rejilla.png)  

</center>

Existe un número elevado de posibles combinaciones para crear recorridos que el lector puede experimentar. A continuación se muestran dos variaciones:

<center>

![Variaciones de caminos de colores](../img/CoCube/variaciones.png)  

</center>

### <FONT COLOR=#AA0000>Programa</font>
!!! Warning "Aviso"
    Para que el programa funcione correctamente hay que añadir las bibliotecas PID y servomotor si no están ya agregadas

Se trata de un sencillo programa que permite escoger uno de los caminos utilizando el botón A y hacer que CoCube recorra dicho camino al pulsar el botón B. Una vez finalizado el recorrido realiza una espera de un segundo y medio y se mueve al centro del tablero (coordenadas 150,100) y se coloca en un ángulo de 180 grados.

La imagen siguiente muestra la pantalla inicial y las sucesivas pulsaciones del botón A.

<center>

![Pantallas](../img/CoCube/pantallas.png)  

</center>

El programa es el siguiente:

<center>

![Programa para recorrer los caminos](../img/CoCube/position.png)  
**[Descarga programa caminos.ubp](../program/cocube/caminos.ubp)**

</center>

En el video siguiente podemos ver el funcionamiento del programa anterior con CoCube conectado por Bluetooth y accionando los botones desde el IDE de Microblocks.

### <FONT COLOR=#AA0000>Resultados</font>

</center>

<iframe width="840" height="472" src="https://www.youtube.com/embed/iZxsYdf3P74?si=SU98Dmtb0xXCJyOu" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

</center>
