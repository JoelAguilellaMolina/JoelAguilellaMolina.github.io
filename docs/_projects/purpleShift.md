---
layout: post
title: Purple Shift
description: another project
tile_image: "/assets/images/IconPurpleShift.png"
---

<iframe width="740" height="400" src="https://www.youtube.com/embed/TXeJokgI_mg" frameborder="0" allowfullscreen></iframe>
<div style="text-align: right;"><p style="font-size: 40px;"> <a href="https://rabbid95.itch.io/purple-shift-demo"><b><i><u>Enlace al Juego</u></i></b></a></p></div>

Purple Shift es un videojuego de Unity diseñado y desarrollado conjuntamente con [Dani Domenech](https://gamedev.thedm.es/) como planteamiento para desarrollar un videojuego de puzzles lógicos como producto a publicar en Steam gracias a una base simple pero potente y un gran pulido en el diseño de niveles, enfocándonos como filosofía en "show don't tell" a la hora de generar curvas de aprendizaje y dificultad para buscar una satisfacción dentro del aprendizaje y la astucia del propio jugador.

Purple Shift se plantea como un videojuego de puzzles y sigilo Top-Down 3D con una leve componente de acción que se plantea en un futuro distópico donde la banda protagonista, Purple Shift, debe entrar en las discotecas sin ser detectados, las cuales son el mayor cúmulo de dinero y drogas en la sociedad corrupta que se mueve por la noche, para conseguir robar el dinero y escapar de la discoteca. Cada discoteca está dividida en varios niveles, conjuntos de salas conectadas con gran énfasis en las puertas azules y rojas, que se activan y desactivan de un color a otro al atravesar por ellas. 

A parte de los elementos de las puertas rojas y azules, se presentan otras tres mecánicas sencillas pero fundamentales que dan una complejidad que enriquece el contexto del uso de las puertas como elemento principal, estas son:

 * **Zona de reset:** Es un elemento que se introduce desde el inicio del juego, al interactuar con la zona, todas las puertas rojas y azules se activan.

{:style="text-align:center;"}
![PurpleShiftReset](/assets/images/PurpleShiftReset.png){: width="150" }

 * **Botones:** Se presentan al principio de la segunda discoteca, muy similares a las puertas, solo que al presionarlos puedes atravesarlos en vez de ser un obstáculo como son las puertas.

{:style="text-align:center;"}
![PurpleShiftBoton](/assets/images/PurpleShiftBoton.png){: width="150" }

 * **Enemigos:** Se presentan al principio de la tercera discoteca, son obstáculos fijos que generan un cono de visión que, al estar en dicho rango, te atrapan y fuerzan a reiniciar el nivel, los objetos sólidos no le permiten ver a través.

{:style="text-align:center;"}
![PurpleShiftEnemy](/assets/images/PurpleShiftEnemy.png){: width="150" }

Dani es el principal creador de la idea del proyecto y se especializa en gran medida en el apartado técnico (base de motor, programación de mecánicas principales, solución de errores y efectos de partículas, unity analytics...), al igual que diseñador de niveles y de gameplay. 

Yo, por mi parte, aporto trabajo de diseño de iconos y elementos visuales, manteniendo una dirección artística sencilla pero clara, mientras que también soy en gran parte diseñador de niveles y principal organizador del proyecto en herramientas como Trello, Miro, documentación de investigación... y **diseñador de sistemas**.

Cuando estabamos diseñando propuestas de niveles y generando una progresión a partir de los bocetos y blockouts que habíamos desarrollado, siempre nos venía a la mente un punto que es uno de los más difíciles de solucionar como diseñador de niveles de puzzle:

 >¿Estamos haciendo una progresión adecuada, sin que se sienta demasiado estresante o notablemente aburrida?

Al estar tanto tiempo generando, testeando y, sobretodo, conociendo sobre cada detalle de los sistemas de movimientos, mecánicas y detalles de todo el juego, como diseñadores nos **intoxicamos** y no podemos juzgar con una visión totalmente limpia que tan difícil es un nivel para un jugador que no ha tocado el proyecto aún, una de las soluciones para resolver este punto es **via playtesting**, sin embargo, dada los contactos limitados que teníamos en ese momento y una inseguridad a la hora de valorar objetivamente los niveles, propuse antes de pasar a playtesting desarrollar un sistema de cálculo de dificultad automática, basada en los elementos que tiene cada nivel y cómo están distribuidos.

Gracias a la naturaleza sencilla del videojuego, propuse calcular la dificultad de cada nivel a partir de una simple fórmula que englobaría todos los objetos y mecánicas del juego, **la fórmula del cálculo de dificultad:**

$$\text{Dificultad} = \left( \frac{\text{Caminos Posibles} \times \text{Peso Caminos Posibles}}{\text{Caminos Victoriosos} \times \text{Peso Caminos Victoriosos}} \right) \times \begin{bmatrix}
\text{Cant. Puertas} \times \text{Peso Puerta} \\
+ \text{Cant. Mecánicas} \times \text{Peso Mecánicas} \\
+ \text{Cant. Interacciones} \times \text{Peso Interacción} \\
+ \text{Cant. Softlock} \times \text{Peso Softlock} \\
+ \text{Tamaño en Tiles} \times \text{Peso Tiles} \\
+ \text{Cant. Enemigos} \times \text{Peso Enemigos} \\
+ \text{Cant. Botones} \times \text{Peso Botones} \\
+ \text{Cant. Puerta Doble} \times \text{Peso Puerta Doble} \\
+ \text{Cant. Shifts Mínimos} \times \text{Peso Shifts} \\
+ \text{Cant. Derrota} \times \text{Peso Derrota}
\end{bmatrix}
$$

Si bien puede parecer compleja, es en esencia coger uno de los elementos principales a la hora de diseñar un nivel (ej. las puertas que hay, los enemigos que hay, las cantidades de caminos que se bifurcan, los espacios transitables o tiles...) Y valorar dicho elemento con un peso mayor o menor, luego sumarlos y contrastarlos con la cantidad de caminos victoriosos como denominador, este numero tenderá a ser 1 pero en el hecho de que haya 2 o más aumentará bastante la dificultad ya que hará que una gran cantidad de caminos secundarios te lleven a una o la otra solución.

![PurpleShiftGrafica](/assets/images/PurpleShifGráfica.png)

A partir de esta fórmula generamos una gráfica que presentaba la curva de dificultad en base a la dificultad planteada, todos estos picos y valles que se generan son investigados y, además, son arreglados en futuras actualizaciones, sirviéndonos como herramienta para intentar mantener un sesgo objetivo sobre una progresión lógica al diseñar niveles y forzarnos a trabajar con una cantidad de elementos y espacio limitado en los niveles, buscando no la saturación si no la funcionalidad con pocos elementos.

![PurpleShiftValoresExcel](/assets/images/PurpleValoresExcel.png)
<div style="text-align: center;"><p style="font-size: 20px;">Valores detectados para cada nivel registrados en el excel para aplicar la fórmula.</p></div>


En cuanto al desarrollo del proyecto actual, se está trabajando en el pulido y diseño agradable visualmente del juego, añadiendo opciones y simplificando la legibilidad y mejorando el gamefeel del gameplay, con expectativas de seguir ampliando y enriqueciendo el gameplay con los últimos detalles.

Se adjunta a continuación un documento que plantea un análisis extenso y explica el sistema de puntuaje de cada variable de la fórmula de la dificultad, al igual que interpreta los datos y propone soluciones para arreglar los niveles irregulares:

<embed src="/assets/pdfs/PurpleShiftSistemaDeDificultad.pdf" width="1000" height="1500" 
 type="application/pdf">