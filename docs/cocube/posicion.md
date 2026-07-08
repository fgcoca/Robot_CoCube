
## <FONT COLOR=#007575>**Introducción**</font>
El ejercicio consiste en primer lugar en crear un programa que muestre las coordenadas X e Y y la orientación en grados del robot en cualquier posición de un CoMap. En segundo lugar se programa la resolución del laberinto partiendo de la posición A(20,20) con orientación 180º y saliendo del mismo por la posición (150,185). Los requisitos son:

* Si el robot no está sobre un CoMap o no lo lee correctamente, CoCube debe mostrar:

![Mensaje de CoCube fuera de tablero](../img/CoCube/fuera_CoMap.png){.center-img50}

* Con el robot sobre un CoMap el aspecto de la pantalla será:

![Mensaje de la posición de CoCube](../img/CoCube/posicion_CoMap.png){.center-img50}

## <FONT COLOR=#007575>**Programa**</font>
!!! Warning "Aviso"
    Para que el programa funcione correctamente hay que añadir las bibliotecas PID y servomotor si no están ya agregadas

![Programa para mostrar coordenadas X e Y y orientación](../img/CoCube/position.png){.center-img}

*[Descarga programa position.ubp](../program/cocube/position.ubp)*

## <FONT COLOR=#007575>**Laberinto**</font>
Utilizando el programa anterior leemos las coordenadas y orientaciones necesarias para que CoCube realice el siguiente trazado en el CoMap "Maze Challenge", partiendo desde cualquier punto del mismo, cuando se pulse el botón A.

![Recorrido a realizar en el CoMap "Maze Challenge"](../img/CoCube/recorrido_CoMap.png){.center-img}

Comenzamos por definir la función "recorrido", que tiene el siguiente aspecto:

![Función "recorrido"](../img/CoCube/funcion_recorrido_CoMap.png){.center-img50}

Una vez finalizado el recorrido se envía el mensaje broadcast "fin" para indicar durante 5 segundos que el recorrido ha finalizado y después llamar, también por bradcast a "inicio", que a continuación se verá en que consiste.

![Broadcast "fin"](../img/CoCube/funcion_fin.png){.center-img50}

Creamos el programa "al comenzar" utilizándo una llamada de boradcast que denominamos "inicio" para poder invocar esta parte una vez finalizado el recorrido y así dejar CoCube listo para comenzar de nuevo. "inicio" se encarga de mostrar el mensaje "Para empezar pulsa A" junto una flecha que apunta al botón del robot.

!["Al comenzar" y boradcast "inicio"](../img/CoCube/P_al_comenzar.png){.center-img}

Ahora se muestra el programa "cuando se pulse el botón A" que a su vez utiliza el broadcast "adelante!". Aquí se realizada la llamada a la función "recorrido". "adelante!" se encarga de asignar los datos de la posición actual del robot sobre el CoMap y mostrarlos tanto en pantalla como en el IDE de forma continuada.

!["cuando se pulse el botón A" y boradcast "adelante!"](../img/CoCube/P_botonA.png){.center-img}

Finalmente se utiliza un bloque "cuando" siempre verdadero que se encargará de mostrar el mensaje por pantalla de que el robot no está sobre el tablero y si la comprobación es cierta simplemente llama a la función "recorrido".

![Bloque "cuando"](../img/CoCube/P_cuando.png){.center-img}

A continuación se ve el programa completo junto al enlace de descarga del mismo.

![Programa para recorrer el laberinto](../img/CoCube/position_maze.png){.center-img}

*[Descarga programa position_maze.ubp](../program/cocube/position_maze.ubp)*

En el video siguiente podemos observar el funcionamiento del programa anterior con pequeños errores de posicionamiento.

<iframe width="700" height="394" src="https://www.youtube.com/embed/ZkNkMW1lv10?si=-3FpylIPe9AuZWUB" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
