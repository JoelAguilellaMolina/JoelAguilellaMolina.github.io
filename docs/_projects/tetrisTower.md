---
layout: post
title: Tetris Tower
description: with no page entry here
tile_image: "/assets/images/IconTetrisTower.png"
---

<iframe width="740" height="400" src="https://www.youtube.com/embed/5s236t3_euY" frameborder="0" allowfullscreen></iframe>

<div style="text-align: right;"><p style="font-size: 40px;"> <a href="https://isg-games.itch.io/tetris-tower"><b><i><u>Enlace al Juego</u></i></b></a></p></div>

Tetris Tower es un proyecto de Unity desarrollado para la [UJI Game Jam 2024 (Veranito Edition)](https://itch.io/jam/uji-game-jam-veranito-edition) desarrollado en 5 días. Trabajé como diseñador principal y programador,  al igual que propuse la idea a partir de la temática de la jam: **Keep it Going Up!**. 

A partir del concepto de Keep it Going Up, planteé una propuesta a partir de uno de los juegos más conocidos de la historia de los videojuegos, el Tetris, solo que buscando justo lo contrario: ¡Apilar la mayor cantidad de bloques posibles! 

A partir de esta simple premisa, evidentemente hay una gran cantidad de cosas que se tienen que tener en cuenta para hacer que el Core loop sea divertido, así que la primera cuestión que planteé a resolver fue la siguiente: 

> "Si el objetivo es hacer la mayor "torre" posible, ¿porqué simplemente no se dejan caer los bloques al instante nada más aparecer?"

Para responder esta respuesta, planteé un sistema más moderno en el que el "grid de juego" es en esencia exactamente el mismo que en el tetris normal, 10 columnas y 20 filas. Sin embargo, una vez el jugador consigue que una pieza sobresalga a nivel vertical (de más de 20 filas), el sobrante se guarda y pasa a la parte más baja del grid, haciendo que se suba una pantalla y pase un "nivel" de la torre. En ese espacio de carga entre niveles, ocurren el siguiente orden de eventos: 

1. Se añade una **desventaja**.
2. Aparece un nivel **jefe**.
3. Se añade una **ventaja**.

Esto ocurre en todas las pantallas del juego a excepción de el nivel 1 en el que se añade una desventaja obligatoria relacionada con no conectar piezas de **ciertos colores**.

El sistema de colores de las piezas de tetris lo hemos cambiado para añadirlo como elemento del jugador a tener en cuenta, ya que ahora el juego funciona por **vidas**, el jugador empieza con 3 vidas y hay 3 distintas maneras de perder vidas:

1. Hacer una línea horizontal en el grid.
2. Dejar caer una pieza de tetris al vacío después del primer nivel.
3. Romper una regla a seguir propuesta por una desventaja o jefe.

El primer punto es para mantener la idea que Tetris Tower es un juego inverso (hacer lineas en el tetris es justo lo contrario que hay que hacer en Tetris Tower). La segunda es para mantener la idea que estás haciendo una torre y, por lo tanto, lanzar piezas al vacío podría servir para descartar las piezas que no te son útiles, por ello tratamos de penalizar este comportamiento, especialmente por la desventaja principal que había planteado anteriormente que será una de las desventajas principales que el jugador deberá jugar alrededor de ella:

![TetrisTowerDesventajaPrincipal](/assets/images/TetrisTowerDesventajaPrincipal.png)

Esta desventaja y otras como el cambio de tamaño de piezas, incapacidad de rotar piezas, de guardar piezas... Se van acumulando y exigen al jugador tomar decisiones estratégicas que promueven no hacer directamente una columna de piezas en vertical pero a la vez penalizan también hacerse plataformas de piezas muy grandes pues además de que se pierde tiempo, generan el peligro de hacer una línea sin querer y perder vidas.

Es por ello que las ventajas ofrecen herramientas positivas como **recompensa** de finalizar un nivel de boss (donde hay una modificación potente del juego que solo dura ese nivel en concreto) y otras herramientas como por ejemplo añadir una vida o que cada 8 piezas la propia pieza no tenga color (por tanto no es afectada por las reglas de perder vida si x color hace contacto con y).

Diseñé casi todas las desventajas y ventajas del juego al igual que dibujé iconos para la mayoría de los modificadores. A nivel de programación programé y me aseguré que la funcionalidad de los modificadores afectaban al contador de vida o al color/tamaño de la pieza en los eventos concretos.

El nombre de **Tetras Peak** fue cambiado por una propuesta de una transformación del proyecto a una aplicación movil y una investigación del mercado actual y competidores para el curso de *"Monetization & Marketing in Games"* del programa de intercambio de Hanze University of Applied Sciences (Hanze UAS) 2024-2025. A continuación se muestra el pitch deck de la propuesta de transformación a producto:

<embed src="/assets/pdfs/TetrasPeakPitchDeck.pdf" width="1000" height="1500" 
 type="application/pdf">