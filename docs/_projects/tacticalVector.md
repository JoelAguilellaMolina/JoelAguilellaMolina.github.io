---
layout: post
title: Tactical Vector
description: another project
tile_image: "/assets/images/IconTacticalVector.png"
---

<iframe width="740" height="400" src="https://www.youtube.com/embed/Jth5xsuxBLs" frameborder="0" allowfullscreen></iframe>
<div style="text-align: right;"><p style="font-size: 40px;"> <a href="https://gamejamer76.itch.io/tactical-vector"><b><i><u>Enlace al Juego</u></i></b></a></p></div>

Tactical Vector es un proyecto de Unity creado como TFG para la carrera de [Diseño y Desarrollo de Videojuegos de la Universitat Jaume I](https://www.uji.es/estudis/base/2024/graus/videojocs/?urlRedirect=https://www.uji.es/estudis/base/2024/graus/videojocs/&url=/estudis/base/2024/graus/videojocs/) para el curso 2024-2025. 

Tactical Vector es un juego de móviles de estrategia por turnos con vista cenital en 3D, en el que el jugador debe superar una serie de niveles controlando a Descartes, el avatar. En estos niveles, el jugador combate en un mapa repleto de obstáculos y enemigos; utilizando funciones en el plano real, deberá esquivar los obstáculos y atacar a los enemigos resolviendo problemas matemáticos para avanzar y derrotar a Thue-Morse, el último enemigo y villano principal del juego.

Antes de todo y la razón de la creación del videojuego es que Tactical Vector es un videojuego serio de matemáticas, especialmente interesado por el target adolescente (12-16) estudiante de la Educación Secundaria Obligatoria, ya que es un sector que tenía una capacidad matemática inferior que la media europea [^1], haciendo que me interesara por proponer un juego con el objetivo de funcionar como una herramienta lúdica para que los alumnos aprendieran como elemento educativo y que complementara a la clase, es por ello que la aplicación actual propone una serie de 12 niveles en los cuales cada uno de ellos son temas que se deben estudiar en el plan de estudios español general para el nivel de tercero de la eso y además ordenado, siendo el último nivel una especie de "examen" o boss final que recoge el material de todos los niveles que se han jugado. Planteando los niveles como elementos de estudio que se puede mandar como deberes o como práctica curricular para reforzar los conocimientos aprendidos en el tema y sesiones.

![TacticalVectorTematica](/assets/images/TacticalVectorTematica.png)
<div style="text-align: center;"><p style="font-size: 20px;">Captura del juego donde se menciona el tema a trabajar en el nivel concreto.</p></div>

El sistema de movimiento es uno de los puntos más complicados que tuve que desarrollar, en esencia era el reto a nivel de programación y diseño que quería centrarme al proponer este proyecto al tutor. En un principio, la idea de la programación iba a ser que, a partir de ciertas variables, utilizaría el módulo math y simplificaría las equaciones como fórmulas para calcular la función $y=f(x)$ con pura matemática, haciendo que cada punto fuera exactamente el numero concreto que se conseguiría alrededor del radio de una circunferencia, para ello lo que hice fue hacer un sistema de ecuaciones donde se planteaba la ecuación de la circunferencia con sus puntos de corte y la ecuación a calcular en concreto en base de y, luego se sustituía y por la función en concreto y se simplificaba, sin embargo, esto tomaba una complejidad de cálculo notable:

$$ x^2 + y^2 = r^2 $$

<div style="text-align: center;"><p style="font-size: 20px;">Forma estándar que define una circunferencia con centro en el origen \((0,0)\) y un radio \(r\)</p></div>

$$y = \sqrt{r^2 − x^2} $$
 
 <div style="text-align: center;"><p style="font-size: 20px;">Simplificación despejando la \(y\)</p></div>

$$y = mx + n $$
 
 <div style="text-align: center;"><p style="font-size: 20px;">Ecuación de la recta, notando que $n < r$ (pues sino saldría del rango de ataque)</p></div>

$$\sqrt{r^2 − x^2} = mx + n $$

 <div style="text-align: center;"><p style="font-size: 20px;">Al tener en igualdad la ecuación de la circunferencia y la ecuación de la recta, buscamos la igualdad para la solución \(x1\) y \(x2\)</p></div>

$$x1 =  \frac{−m ∗ n + \sqrt{ r^2 + m^2r^2 − n^2} }{m^2 + 1}$$

$$x2 =  \frac{−(m ∗ n + \sqrt{ r^2 + m^2r^2 − n^2}) }{m^2 + 1}$$

Si bien al adjuntar esta fórmula en código funcionaba completamente precisa, al añadir ya un poco más de complejidad como, por ejemplo, calcular los puntos de cortes con la función cuadrática: $y = ax^2 + bx + c$, tuve que incluso simplificarla a $y = mx^2 + n$ y, aun así, despejar la x en la igualdad de ecuaciones era un trabajo demasiado costoso:

$$\sqrt{r^2 − x^2} = mx^2 + n $$

$$x1 = \frac{\sqrt{\sqrt{4m^2r^2 + 4mn + 1} - 1 - 2nm}}{m\sqrt{2}}$$

$$x2 = -\frac{\sqrt{\sqrt{4m^2r^2 + 4mn + 1} - 1 - 2nm}}{m\sqrt{2}}$$

Es por ello que aborde el uso de colisiones, usando un sphere collider alrededor del radio y dejando que la función siguiera su curso a partir de un gameobject que a partir de detectar el indicador y el personaje fuera de la esfera, los detenía en el último punto. Esto hizo que se tuviera que cambiar el cálculo de colisiones de dicha esfera a continuo en vez de discreto, ya que en fórmulas de un crecimiento exponecial muy destacable (como las cuadráticas), el punto salía demasiado externo a la esfera. A continuación se puede ver un snipet de código mucho más limpio que simplemente aplicar las fórmulas anteriores, que ayudaba también a la legibilidad del mismo:

~~~c#
else if (aplicarMovimiento)
{
  if (isMoving)
  {
    if (m < 1.5f && m > −1.5f) 
      x = x + (direccion) ∗ (VELOCIDAD ∗ 2);
    else
      x = x + (direccion) ∗ VELOCIDAD; 
      /* Se reduce la velocidad en funciones empinadas para evitar 
         que el sistema de colisiones no lo detecte correctamente */
    

    if (convertTo == "")
      y = m ∗ x + n;
    else if (convertTo == ”log”)
      y = m ∗ Mathf.Log10(x) + n;
    else if (convertTo == ”sen”) 
      y = m ∗ Mathf.Sin(x)+ n;
    else if (convertTo == ”ˆ2”) 
      y = m ∗ (x ∗ x) + n;
    if (! isEnemyTurn)
    {
      if(isMoveState)
      avatarPosition.position = new Vector3(
        temporalPosition.position.x + x,
        VELOCIDAD,
        temporalPosition.position.z + y);
      else
      ataquePosition.position = new Vector3(
        temporalPosition.position.x + x,
        1,
        temporalPosition.position.z + y);
    }
[ . . . ]

~~~

A parte de estos puntos, es un proyecto fundamentalmente singular en casi todos los aspectos, todo código, concepto, investigación y gran parte de arte 2D es creación mía para el proyecto. Todo asset externo (como la música y los modelos 3D), están correctamente citados en la categoría de créditos de la aplicación.

Para más información y una descripción técnica del proceso de creación y objetivo del proyecto, se adjunta la memoria de desarrollo del videojuego a continuación:

<embed src="/assets/pdfs/TacticalVectorMemoria.pdf" width="1000" height="1500" 
 type="application/pdf">

[^1]: [RESULTADOS DE TIMSS 2023: INFORME ESPAÑOL](https://inee.educacion.es/2024/12/04/resultados-de-timss-2023-informe-espanol/)
