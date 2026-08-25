---
layout: post
title: Just 5 Minutes
description: another project
tile_image: "/assets/images/IconJust5Minutes.png"
---

![Just5MinCaptura1](/assets/images/Just5MinutesCaptura1.png)
![Just5MinCaptura2](/assets/images/Just5MinutesCaptura2.png)

<div style="text-align: right;"><p style="font-size: 40px;"> <a href="https://isg-games.itch.io/just-5-minutes"><b><i><u>Enlace al Juego</u></i></b></a></p></div>

Just 5 Minutes es un videojuego desarrollado con Unity en 4 días en un equipo de 6 personas para la Game Jam de [Game Maker's Toolkit 2026](https://itch.io/jam/gmtk-jam-2026). En este proyecto he trabajado como principal diseñador de gameplay y dirección narrativa de éste, siendo el creador de la idea principal de gameplay a partir de la temática de la jam que se propuso para el desarrollo: **Countdown**.

El juego se ambienta en un primer momento en una estación de despegue de un cohete, teniendo que encender la cuenta atrás de la nave antes de que despegue de 5 minutos. No obstante, cada ciertos segundos el juego va presentando eventos y escenarios **negativos** que van afectando a la propia cuenta atrás (velocidad de segundos más lenta, cambio de minutos a segundos, un minuto son 99 segundos...) A las cuales el propio jugador se le proponen **mejoras** al contador para contrarrestar, siendo la propia elección y observación de los efectos en el reloj el core principal del gameplay, generando una experiencia pseudo-roguelike muy intuitiva con muy poca interacción pero notable para el avance.

Como diseñador, diseñé los **24 buffs y debuffs** que se encuentran en la pool de eventos a ocurrir en el contador, al igual que los tiempos en los cuales volvían a aparecer un evento de buff y otro evento de debuff (siendo un cooldown menor en el inicio del juego, para presentar las mecánicas principales a los jugadores en los primeros segundos). Una cosa a destacar de este diseño es que, por definción, los buffs a parte de ser levemente más potentes que los debuffs, directamente los neutralizan o **buscan contrarrestarlos** para hacer que el jugador reflexione gracias a la pantalla de consultar buffs y debuffs cuáles pueden contrarrestar una posible penalización. (p.e. uno de los debuffs más peligrosos es la Death Hour, que por cada segundo tiene una probabilidad de un 0.01% que añada una hora al contador, sin embargo, una vez te sale **Death Hour**, hay una gran probabilidad que puedas elegir el buff **Odd one out**, que pasa los unos a ceros en un 10% si el contador de segundos es impar, indirectamente eliminando la penalización en un tiempo mucho menor.)

{:style="text-align:center;"}
![Just5Miniconosheet](/assets/images/sheetJust5Minutes.png)
<div style="text-align: center;"><p style="font-size: 20px;">Parte de la spritesheet de iconos que diseñé e ilustré.</p></div>

Una de las bases que queríamos ajustar de una manera dura a la hora del diseño era el hecho que, si bien evidentemente el jugador no va a pasar 5 minutos sólo en el juego ya que se van a aplicar buffs y debuffs que dan saltos a ese tiempo, teníamos planteada que la experiencia durase como media una sesión de **10-12 minutos.** Por lo tanto, como se puede suponer, si bien se ha comentado que los buffs tienden a ser más fuertes que los debuff, un jugador puede tener notable mala suerte y podría no acabar nunca el juego. Es por ello que ideé un sistema llamado ***"Tiempo Secreto"***.

El tiempo secreto es en esencia el tiempo real que empieza a contar al momento que el jugador comienza la partida y no es modificado por la velocidad o añadir o desgrabar segundos por parte de los eventos del contador. Este temporizador, además de servir como puntuación final al acabar el juego, también aporta al jugador en la cola de eventos que aparecen ciertos **eventos duros** que siempre ocurrirán al llegar a un tiempo concreto en la partida, a continuación se muestra una lista del "guión" de eventos que diseñé, independientemente de los eventos de buffs y debuffs aleatorios que pueden ocurrir alrededor de la partida:

{:style="text-align:center;"}
![Just5MinScriptedBuffsyDebuffs](/assets/images/Just5MinutesScriptedBuffsYDebuffs.png)

Evidentemente esta lista implica que se entienden cuáles son los buffs y debuffs que se mencionan en cada minuto, pero en esencia, se ha diseñado el juego para que haya ciertos buffs mucho más poderosos que otros y, al igual, debuffs más potentes que otros, por ejemplo, **Minute Swap** cambia el contador de minutos y segundos al pasar 1 segundo con un 1% de probabilidades y **Not How Time Works** cambia los minutos a 99 segundos y las horas a 99 minutos. Estos debuffs son cruciales y basicamente dividen el early del mid game y mid del lategame y por lo tanto no pueden aparecer en la pool de aleatorios porque desbalancearían por completo el juego, pero al aparecer una vez proponen un desafío para los jugadores que tienen que superar en ciertos puntos concretos, y separados con otros rangos de tiempo para que se puedan acostumbrar y puedan experimentar el cambio. Al acercarse a los 10 minutos notarás se puede destacar que la cantidad de buffs y debuffs que aparecen son mucho mayores que en la progresión habitual, esto es porque en este momento se debería llegar al **"tiempo de descuento"** donde he preparado que aparezcan una gran cantidades de buffs muy potentes al igual que debuffs muy **caóticos** (por ejemplo Glorping Around que remueve todos los dígitos del timer aleatoriamente.) Dando una sensación cada vez más estropeada del contador que hace saltos cada vez más bruscos y más rápidos (con los dos fast timers seguidos), pero al final llegando a la marca de menos de 15 segundos, donde todos los efectos se descartan y se activa la cinemática de despuegue final del juego, dando paso a la cuenta atrás desde 10 del personaje principal. 

A continuación, se adjunta un documento que describe el funcionamiento de cada buff y debuff propuesto en el juego, para más información y contexto que también podría ayudar a entender el guión del tiempo secreto:

<embed src="/assets/pdfs/Just5MinutesBuffsAndDebuffs.pdf" width="760" height="1000" 
 type="application/pdf">


{% comment %}
H1 Header
============

Paragraphs are separated by a blank line.

2nd paragraph. *Italic*, **bold**, and `monospace`. Itemized lists
look like:

  * this one
  * that one
  * the other one

Note that the actual text
content starts at 4-columns in.

> Block quotes are
> written like so.
>
> They can span multiple paragraphs,
> if you like.


H2 Header
------------

Here's a numbered list:

 1. first item
 2. second item
 3. third item

Note again how the actual text starts at 4 columns in (4 characters
from the left side). Here's a code sample:

    # Let me re-iterate ...
    for i in 1 .. 10 { do-something(i) }

As you probably guessed, indented 4 spaces. By the way, instead of
indenting the block, you can use delimited blocks, if you like:

~~~
define foobar() {
    print "Welcome to flavor country!";
}
~~~

(which makes copying & pasting easier). You can optionally mark the
delimited block for Pandoc to syntax highlight it by specifying the languagae after the start of a block (e.g. `~~~python`) which would look like :

~~~python
import time
# Quick, count to ten!
for i in range(10):
    # (but not *too* quick)
    time.sleep(0.5)
    print(i)
~~~

### An H3 header ###

Now a nested list:

 1. First, get these ingredients:

      * carrots
      * celery
      * lentils

 2. Boil some water.

 3. Dump everything in the pot and follow
    this algorithm:

        find wooden spoon
        uncover pot
        stir
        cover pot
        balance wooden spoon precariously on pot handle
        wait 10 minutes
        goto first step (or shut off burner when done)

    Do not bump wooden spoon or it will fall.

Notice again how text always lines up on 4-space indents (including
that last line which continues item 3 above).

Here's a footnote [^1].

[^1]: Some footnote text.

Tables can look like this:

| Header 1 | Header 2                   | Header 3 |
|:--------:|:--------------------------:|:--------:|
| data1a   | Data is longer than header | 1        |
| d1b      | add a cell                 |          |
| lorem    | ipsum                      | 3        |
|          | empty outside cells        |          |
| skip     |                            | 5        |
| six      | Morbi purus                | 6        |


A horizontal rule follows.

***

Here's a definition list:

apples
  : Good for making applesauce.

oranges
  : Citrus!

tomatoes
  : There's no "e" in tomatoe.

Again, text is indented 4 spaces. (Put a blank line between each
term and  its definition to spread things out more.)

Here's a "line block" (note how whitespace is honored):

| Line one
|   Line too
| Line tree

and images can be specified like so:

![example image](https://images.unsplash.com/photo-1488190211105-8b0e65b80b4e?w=300&h=300&fit=crop "An exemplary image")

Inline math equation: $\omega = d\phi / dt$. Display
math should get its own line like so:

$$I = \int \rho R^{2} dV$$

{% endcomment %}