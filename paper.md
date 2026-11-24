# La pecera dimensional: paper de uso y guía de la idea

## Resumen

Este documento acompaña a **Dimensional Fishbowl**, una página interactiva que plantea una pregunta: si nuestro universo fuera una pecera dentro de una dimensión que no vemos, ¿cómo podríamos deducirlo sin salir nunca de ella? La primera parte es un paper de uso: explica cada control, resuelve un ejemplo con los números que da la herramienta y marca sus límites. La segunda parte es una guía de la idea: recorre la tradición que va de *Flatland* de Edwin Abbott (1884) a la geometría intrínseca de Gauss y Riemann, el principio de Cavalieri y la tomografía de Radon, la pregunta de Ehrenfest sobre por qué el espacio tiene tres dimensiones, la teoría de Kaluza y Klein, los modelos de dimensiones extra grandes de Arkani-Hamed, Dimopoulos y Dvali y los experimentos de balanza de torsión que buscan desviaciones de la ley 1/r² a escalas de micrómetros.

La tesis de la herramienta es que hay al menos dos maneras de detectar una dimensión escondida desde adentro: **por lo que entra y sale** del mundo visible (objetos que aparecen de la nada, cambian de forma y desaparecen) y **por cómo se diluyen las fuerzas** (una ley de fuerza que cambia de exponente a distancias cortas). La primera es la de los cuentos; la segunda es la que la física busca de verdad.

## Parte I. Paper de uso

### 1. Qué es la herramienta

Dimensional Fishbowl es una página estática sin dependencias. Se abre desde la [demo en vivo](https://loiaconobruno.github.io/dimensional-fishbowl/) o con doble clic en `index.html`. Tiene dos pistas:

1. **Pista 1: cosas que aparecen de la nada.** Un objeto tridimensional atraviesa un plano. Cuatro paneles muestran la escena desde afuera (de costado), lo que ve un ser plano desde adentro, el registro del área a lo largo del tiempo y la reconstrucción del perfil del objeto apilando los cortes.
2. **Pista 2: una fuerza que "se escapa".** Un gráfico logarítmico de la fuerza de una masa puntual en función de la distancia, en un mundo con una dimensión extra enrollada de tamaño L. Dos recuadros muestran la pendiente de la curva cerca (r = 0,01) y lejos (r = 100).

La lógica está en `src/pecera.js` (sin acceso al DOM), los dibujos en `src/grafico.js` y la interacción en `src/app.js`. Los tests se corren con `npm test` en Node 18 o más nuevo.

### 2. Instalación

```bash
git clone https://github.com/LoiaconoBruno/dimensional-fishbowl.git
cd dimensional-fishbowl
npm test
```

Después se abre `index.html` con doble clic. No hay paso de build.

### 3. Pista 1, control por control

| Control | Qué hace |
|---|---|
| Objeto | Elige entre esfera, cono con la punta arriba, cubo y "dos esferas a distinta altura" |
| Pasar por el plano | Anima el objeto atravesando el plano a velocidad constante |
| Posición del objeto | Deslizador de 0 % a 100 % para mover el objeto a mano |

Los cuatro paneles:

- **Desde afuera (vista de costado, 3D):** el objeto y el plano como los vería alguien con una dimensión más.
- **Desde adentro (el plano visto desde arriba):** las figuras planas que existen en ese instante para el habitante del plano. Pueden ser círculos o cuadrados, y puede haber más de una.
- **Lo que registra el ser plano:** el área total de los cortes en función del tiempo, desde que no hay nada hasta que vuelve a no haber nada.
- **La deducción (apilando los cortes):** el perfil reconstruido. Al final de la pasada se muestra el "volumen" estimado, la suma de área por espesor de cada corte.

### 4. Pista 2, control por control

| Control | Rango | Qué representa |
|---|---|---|
| Mundo | Planilandia (2D + 1 escondida) o el nuestro (3D + 1 escondida) | Cuántas dimensiones visibles tiene el mundo, n = 2 o n = 3 |
| Tamaño de la dimensión escondida L | 0,1 a 10 (escala logarítmica) | La circunferencia de la dimensión enrollada |

El gráfico muestra, en escala logarítmica en ambos ejes, la fuerza real (la suma sobre todas las copias), la recta 1/rⁿ (la ley de un mundo con una dimensión más) y la recta 1/r^(n−1) (la ley de siempre). La pendiente de la curva real en escala logarítmica es el exponente efectivo de la ley de fuerza.

### 5. Ejemplo resuelto

**Pista 1 con la esfera.** Se elige "Esfera" y se aprieta "Pasar por el plano". La esfera tiene radio 1. Cuando el plano está a altura z del centro, el corte es un círculo de radio √(1 − z²) y área π(1 − z²). El habitante del plano ve un punto que aparece de la nada, un círculo que crece hasta radio 1 y después se achica hasta desaparecer. El registro de área es una parábola invertida. Al final, la suma de área por espesor da **4,19**, que es 4π/3, el volumen de la esfera. El ser plano calculó un volumen que nunca pudo ver.

Los otros objetos dan, con el mismo procedimiento:

| Objeto | Lo que se ve en el plano | Volumen inferido |
|---|---|---|
| Esfera | Círculo que crece y se achica | 4,19 (= 4π/3) |
| Cono | Círculo que se achica linealmente hasta un punto | 2,09 (= 2π/3) |
| Cubo | Cuadrado que aparece de golpe, no cambia y desaparece de golpe | 8,00 |
| Dos esferas | Dos círculos separados que crecen y se achican desfasados | 8,38 (= 8π/3) |

**Pista 1 con dos esferas.** Con la posición al 50 %, el habitante del plano ve **2 figuras separadas**. Desde adentro no hay manera de saber, mirando solo ese instante, que son dos partes de un mismo objeto (o dos objetos que viajan juntos). Esa es la intuición más inquietante de la pecera: lo que adentro parecen cosas distintas puede ser una sola afuera.

**Pista 2 en nuestro mundo.** Con "El nuestro" y L = 1, la página informa una pendiente de **−3** cerca (r = 0,01) y **−2** lejos (r = 100). Lejos se ve la ley de Newton, F ∝ 1/r². Cerca, la fuerza crece como 1/r³, la ley de un mundo de cuatro dimensiones espaciales.

**Pista 2 en Planilandia.** Con "Planilandia", las pendientes pasan a **−2** cerca y **−1** lejos. En un mundo plano la gravedad cae como 1/r; si hubiera una tercera dimensión escondida, a distancias cortas caería como 1/r².

### 6. Cómo leer los resultados

- El cambio de pendiente ocurre alrededor de r ≈ L. Para L = 1 y n = 3, a r = 0,3 la pendiente ya es −2,95 y a r = 1 vale −2,14. Si L fuera de una décima de milímetro, habría que medir la gravedad a esa distancia para notar algo.
- El exponente cercano no depende de L; solo cambia **dónde** ocurre la transición. Por eso los experimentos reales se expresan como "no hay dimensión extra más grande que tantos micrómetros".
- La pista 1 no prueba que exista una dimensión extra; muestra qué tipo de observación sería sospechosa: objetos que aparecen y desaparecen sin causa visible, que cambian de tamaño sin que nada los toque, o piezas separadas que se comportan como una sola.

#### 6.1 Preguntas frecuentes

**¿Por qué el cubo no cambia de tamaño al cruzar?** Porque está apoyado de cara contra el plano. Todos sus cortes horizontales son el mismo cuadrado. Si el cubo cruzara apoyado sobre un vértice, el habitante del plano vería un punto que se convierte en triángulo, luego en hexágono, luego en triángulo invertido y otra vez en punto. La página no incluye ese caso; está en los próximos pasos (objetos que rotan).

**¿El "volumen inferido" es exacto?** Es una suma de Riemann con 4000 cortes, así que coincide con el valor exacto hasta la tercera cifra decimal. El cubo da 7,9992 en vez de 8 porque los bordes abruptos se discretizan.

**¿Por qué la fuerza de la pista 2 no tiene unidades?** Porque lo que importa es la forma de la curva, no su escala. Se usa G = 1 y masa 1. Las pendientes son adimensionales.

**¿Qué pasa si L es muy chico?** La transición se corre hacia la izquierda del gráfico. Con L = 0,1, a r = 0,01 la pendiente todavía es casi −3, pero la región donde se nota es diez veces más angosta. En el límite L → 0 la dimensión extra se vuelve invisible a todas las distancias accesibles.

### 7. Limitaciones

- Es una visualización para pensar, no una prueba de nada.
- La pista 1 usa objetos rígidos que cruzan el plano en línea recta y sin rotar.
- La pista 2 usa el modelo más simple: una sola dimensión extra, plana y circular, y una fuerza que se propaga igual en todas las dimensiones. Los modelos físicos reales (Arkani-Hamed, Dimopoulos y Dvali, 1998; Randall y Sundrum, 1999) son más complejos: pueden tener varias dimensiones extra, geometrías curvadas o fuerzas que solo la gravedad siente.
- Hasta hoy, los experimentos no encontraron desviaciones de la ley 1/r² de la gravedad por encima de unas decenas de micrómetros, ni señales de dimensiones extra en el LHC.

## Parte II. Guía de la idea

### 8. La idea: una pecera que no se ve desde adentro

Un pez en una pecera vive en un mundo con bordes. Puede chocar contra el vidrio, ver formas distorsionadas del otro lado y, si es muy curioso, preguntarse qué hay afuera. La idea que dio origen a la herramienta lleva esa imagen al extremo: ¿y si nuestro universo fuera una pecera dentro de una dimensión que no podemos ver ni tocar? El pez tiene al menos el vidrio. Nosotros, ni eso.

La pregunta interesante no es si eso es posible (filosóficamente, casi cualquier cosa lo es) sino **cómo se podría deducir desde adentro**. Esa formulación cambia todo: obliga a pensar qué huellas dejaría un afuera en las cosas que sí podemos medir. Y resulta que la física lleva más de un siglo haciendo exactamente esa pregunta.

### 9. Planilandia y sus descendientes

#### 9.1 Abbott, 1884

Edwin Abbott Abbott, director de escuela y teólogo inglés, publicó en 1884 *Flatland: A Romance of Many Dimensions*, firmado con el seudónimo "A Square". El narrador es un cuadrado que vive en un plano. Un día lo visita una esfera, que desde el punto de vista del cuadrado es un punto que aparece de la nada, se convierte en un círculo que crece, se achica y desaparece. El cuadrado no entiende qué está viendo hasta que la esfera lo saca del plano y le muestra su mundo desde arriba.

Esa escena es literalmente la pista 1 de la herramienta. Abbott la usó también como sátira de la rígida jerarquía social victoriana (en Planilandia, el rango depende del número de lados) y como argumento por la humildad epistemológica: el cuadrado, después de ver la tercera dimensión, pregunta por la cuarta, y la esfera, que se creía la cima, se niega a imaginarla.

#### 9.2 Hinton y el teseracto

Charles Howard Hinton, matemático británico contemporáneo de Abbott, publicó entre 1884 y 1886 los *Scientific Romances*, cuyo primer ensayo se titula "What is the Fourth Dimension?". En 1904 escribió *The Fourth Dimension*, donde introdujo la palabra **teseracto** para el hipercubo de cuatro dimensiones y propuso ejercicios con cubos de colores para "entrenar" la intuición tetradimensional. Hinton tomó en serio la pregunta de cómo un ser de n dimensiones podría razonar sobre n + 1: por analogía, por cortes y por proyecciones.

#### 9.3 Burger, Dewdney y Rucker

La tradición siguió. Dionys Burger, profesor de física holandés, escribió *Sphereland* (1957, traducido al inglés en 1965), una secuela en la que los habitantes de Planilandia descubren que su mundo es en realidad la superficie de una esfera enorme: los triángulos grandes tienen ángulos que suman más de 180°. Alexander Keewatin Dewdney publicó *The Planiverse* (1984), un mundo bidimensional con física, química y biología coherentes, y se encontró con problemas que la herramienta deja ver: en 2D, un tubo digestivo que atraviesa el cuerpo lo partiría en dos. Rudy Rucker, matemático y escritor, recopiló la historia y la matemática de estas ideas en *The Fourth Dimension: A Guided Tour of the Higher Universes* (1984). Thomas Banchoff, de la Universidad Brown, hizo las primeras animaciones por computadora de hipercubos rotando en los años setenta y lo resumió en *Beyond the Third Dimension* (1990).

Todos comparten la estructura de la pecera: un ser que no puede salir, y la pregunta de qué señales le llegan de afuera.

### 10. Pista 1: cortes, Cavalieri y tomografía

#### 10.1 Reconstruir un volumen con rebanadas

El habitante del plano de la herramienta registra el área de los cortes en función del tiempo. Si sabe que el objeto se mueve a velocidad constante, el tiempo es proporcional a la altura del corte, y puede sumar área por espesor:

$$ V ≈ Σ A(zᵢ) · Δz → ∫ A(z) dz $$

Esta idea tiene nombre: el **principio de Cavalieri**. Bonaventura Cavalieri, discípulo de Galileo, lo publicó en *Geometria indivisibilibus continuorum nova quadam ratione promota* (1635): dos sólidos con la misma altura cuyas secciones a cada altura tienen la misma área tienen el mismo volumen. Pero la idea es más antigua. Arquímedes, en *El método*, un tratado perdido durante siglos y redescubierto en 1906 por Johan Ludvig Heiberg en un palimpsesto, calculó el volumen de la esfera comparando sus cortes con los de un cilindro y un cono, equilibrándolos en una palanca imaginaria. El resultado, V = 4πR³/3, es el 4,19 que muestra la herramienta para R = 1.

El dato importante para la pecera es que **el ser plano no necesita ver el objeto entero**. Le alcanza con medir lo que pasa por su mundo y suponer algo sobre cómo se mueve. Es razonamiento por inferencia, no por observación directa.

#### 10.2 Lo que la suma de áreas no puede saber

Hay información que se pierde. El volumen sale bien, pero la forma no del todo: la herramienta apila los cortes centrados, así que reconstruye el **perfil de revolución**. Si el objeto fuera un elipsoide inclinado, la reconstrucción sería una figura distinta con el mismo volumen. Y el caso de las dos esferas muestra un problema más profundo: ver dos piezas en el plano no dice si son dos objetos o uno solo conectado por arriba. Esa ambigüedad es la que en topología se estudia como el problema de reconstruir la conectividad de un objeto a partir de sus secciones, y es la que la teoría de Morse formaliza: los momentos en que el número de piezas cambia (aparece una, se separan dos, se juntan) delatan la forma global del objeto. Marston Morse desarrolló esa teoría en los años veinte y treinta, y John Milnor la expuso con claridad en *Morse Theory* (1963).

#### 10.3 Radon y la tomografía

Si el ser plano pudiera además ver el objeto desde varios ángulos, por ejemplo midiendo cuánto bloquea la luz a lo largo de cada línea, podría reconstruir la forma completa y no solo el perfil. Johann Radon demostró en 1917 (*Über die Bestimmung von Funktionen durch ihre Integralwerte längs gewisser Mannigfaltigkeiten*) que una función en el plano queda determinada por sus integrales a lo largo de todas las rectas. Medio siglo después, Allan Cormack y Godfrey Hounsfield construyeron sobre esa idea la tomografía computada, por la que recibieron el Premio Nobel de Medicina en 1979.

La tomografía es la pista 1 hecha tecnología: reconstruir un objeto de tres dimensiones a partir de cortes que se miden desde afuera. La pecera invierte el punto de vista: los cortes se miden desde adentro.

#### 10.4 Una dimensión más: la hiperesfera que nos atraviesa

Si una hiperesfera de cuatro dimensiones atravesara nuestro espacio, veríamos una esfera que aparece en un punto, crece, se achica y desaparece. Su "volumen de cuatro dimensiones" (el hipervolumen) es π²R⁴/2, y podríamos calcularlo sumando los volúmenes de las esferas que vimos por el espesor del corte en la cuarta dimensión. La herramienta muestra el caso 3D → 2D porque se puede dibujar; el razonamiento es idéntico un escalón más arriba.

¿Hay algo así en la naturaleza? No que se sepa. Pero el ejercicio enseña qué buscar: aparición sin causa, conservación de algo (el volumen total inferido) que no se explica con lo visible, y piezas separadas que actúan coordinadas.

#### 10.5 Cuando los cortes cambian de forma

En los cuatro objetos de la herramienta, los cortes solo cambian de **tamaño** (o de número, en las dos esferas). Pero si un objeto cruza el plano inclinado, sus cortes cambian de **forma**, y eso le da al habitante del plano mucha más información.

El ejemplo clásico es un cubo que cruza con su diagonal principal perpendicular al plano, apoyado primero sobre un vértice. El ser plano ve:

1. Un punto, cuando el vértice toca el plano.
2. Un triángulo equilátero que crece, mientras el plano corta las tres aristas que salen de ese vértice.
3. Un hexágono irregular, cuando el plano pasa a cortar seis aristas.
4. Exactamente a mitad de camino, un **hexágono regular**.
5. El proceso inverso: hexágono, triángulo (ahora rotado 60°) y punto.

Un habitante del plano que vea esa secuencia tiene una pista fuerte de simetría: el triángulo que aparece al final está girado respecto del primero, algo que ningún objeto plano en rotación produciría de esa manera. Lo mismo pasa un escalón más arriba: un teseracto que atraviesa nuestro espacio apoyado en un vértice se vería como un tetraedro que crece, se trunca, pasa por un octaedro en el medio y vuelve a ser un tetraedro, invertido. Banchoff y sus colaboradores animaron estas secuencias en los años setenta. Agregar objetos que rotan o cruzan inclinados está entre los próximos pasos de la herramienta.

### 11. Deducir la forma del mundo desde adentro: Gauss y Riemann

#### 11.1 El teorema egregio

La pista más profunda de que un mundo tiene una forma, aunque no se pueda salir de él, la dio Carl Friedrich Gauss. En *Disquisitiones generales circa superficies curvas* (1827) demostró el *Theorema Egregium* ("teorema notable"): la curvatura de una superficie se puede calcular midiendo solo distancias y ángulos **sobre** la superficie, sin referencia al espacio en el que está inmersa. Un ser plano que viviera en la superficie de una esfera podría descubrir que su mundo es curvo dibujando triángulos grandes y notando que sus ángulos suman más de 180°, o midiendo que la circunferencia de un círculo grande es menor que 2π veces su radio. Es el argumento de *Sphereland*.

Se cuenta que Gauss midió, como parte de su trabajo geodésico en Hannover, el triángulo formado por los montes Brocken, Hohenhagen e Inselsberg para ver si sus ángulos sumaban 180°. Los historiadores discuten si lo hizo con esa intención; lo seguro es que la idea de **geometría intrínseca** salió de su trabajo práctico de medir la Tierra.

#### 11.2 Riemann, 1854

Bernhard Riemann generalizó la idea en su conferencia de habilitación en Gotinga, *Über die Hypothesen, welche der Geometrie zu Grunde liegen* ("Sobre las hipótesis en que se funda la geometría", 1854, publicada en 1868). Riemann propuso que el espacio físico podría tener una curvatura que varía de punto a punto, y que cuál es la geometría del espacio es una pregunta empírica, no una verdad a priori. Fue el lenguaje que Einstein usaría sesenta años después para la relatividad general.

La lección para la pecera es esta: **no hace falta un afuera para tener forma**. Una variedad puede ser curva, finita o tener dimensiones enrolladas sin estar sumergida en nada. La pregunta "¿qué hay afuera de la pecera?" puede no tener respuesta, mientras que "¿qué forma tiene la pecera?" sí la tiene, y se responde midiendo desde adentro.

### 12. Pista 2: por qué la gravedad cae como 1/r²

#### 12.1 Líneas de campo y el teorema de Gauss

La pista 2 se apoya en una observación que se remonta a Michael Faraday y se formaliza con el teorema de Gauss: si una fuerza se transmite por "líneas de campo" que salen de una masa y no se crean ni se destruyen en el camino, la intensidad a distancia r es inversamente proporcional al área de una esfera de radio r. En tres dimensiones esa área es 4πr², así que la fuerza cae como 1/r². En un espacio de d dimensiones, la "esfera" de radio r tiene "área" proporcional a r^(d−1), así que

$$ F(r) ∝ 1 / r^(d−1) $$

En Planilandia (d = 2), F ∝ 1/r. En nuestro mundo (d = 3), 1/r². En un mundo de cuatro dimensiones espaciales, 1/r³.

#### 12.2 Kant y la pregunta al revés

Immanuel Kant, en su primer escrito publicado, *Gedanken von der wahren Schätzung der lebendigen Kräfte* ("Pensamientos sobre la verdadera estimación de las fuerzas vivas", 1747), sugirió el argumento al revés: quizás el espacio tiene tres dimensiones **porque** las sustancias interactúan con una ley de fuerza inversa al cuadrado. Si Dios hubiera elegido otra ley, el espacio tendría otra dimensión. Es una idea especulativa, pero muestra que la conexión entre el exponente de la fuerza y el número de dimensiones se intuyó muy temprano.

#### 12.3 Ehrenfest, 1917: por qué tres

Paul Ehrenfest, físico austríaco, publicó en 1917 un artículo con un título que es casi la pregunta de la pecera: *In what way does it become manifest in the fundamental laws of physics that space has three dimensions?* (*Proceedings of the Amsterdam Academy*, 20, 200–209). Mostró que, con una fuerza de tipo 1/r^(d−1), las órbitas planetarias cerradas y estables solo existen para d = 3. Con d = 4, la fuerza 1/r³ hace que cualquier órbita circular sea inestable: los planetas caerían en espiral o escaparían. También discutió que en d ≥ 4 los átomos no tendrían estados ligados estables. Un mundo con planetas y química estable "sabe" que tiene tres dimensiones grandes.

Esto marca un límite a la pecera: si hay dimensiones extra, tienen que ser lo bastante chicas como para que a escala atómica y planetaria la ley siga siendo 1/r². La herramienta modela exactamente ese escenario.

### 13. Dimensiones enrolladas: Kaluza, Klein y la pajita

#### 13.1 Kaluza, 1921

En 1919, Theodor Kaluza, un matemático poco conocido de Königsberg, le envió a Einstein un artículo con una idea notable: si se escribe la relatividad general en **cinco** dimensiones (cuatro de espacio, una de tiempo) en vez de cuatro, las ecuaciones contienen, además de la gravedad, las ecuaciones de Maxwell del electromagnetismo. La quinta dimensión "fabrica" la luz. Einstein tardó dos años en recomendarlo para publicación; apareció en 1921 como *Zum Unitätsproblem der Physik* en las actas de la Academia Prusiana de Ciencias. Gunnar Nordström había tenido una idea parecida en 1914 con una teoría de la gravedad anterior.

El problema era obvio: ¿dónde está la quinta dimensión?

#### 13.2 Klein, 1926

Oskar Klein, físico sueco, dio la respuesta en 1926 (*Quantentheorie und fünfdimensionale Relativitätstheorie*, *Zeitschrift für Physik*, 37, 895–906): la dimensión extra está **enrollada** en un círculo diminuto, de un tamaño del orden de la longitud de Planck (10⁻³⁵ m). La imagen clásica es una manguera de jardín vista de lejos: parece una línea (una dimensión), pero una hormiga sobre ella puede caminar también alrededor (la segunda dimensión, enrollada). Desde lejos, la dimensión circular es invisible.

Klein agregó un efecto cuántico: si la dimensión extra es un círculo de circunferencia L, el momento en esa dirección solo puede tomar valores discretos, múltiplos de h/L. Desde nuestro punto de vista, cada valor aparece como una partícula de masa distinta: una "torre de Kaluza-Klein" de partículas cada vez más pesadas. Buscar esas partículas en un acelerador es otra forma de detectar la dimensión escondida.

#### 13.3 Lo que modela la herramienta

La pista 2 usa exactamente la geometría de Klein: n dimensiones visibles grandes y una dimensión circular de circunferencia L. La herramienta no hace mecánica cuántica; calcula cómo se reparte una fuerza clásica en ese espacio.

### 14. El método de las imágenes: la matemática de la pista 2

#### 14.1 Una masa, infinitas copias

En un espacio con una dimensión circular, recorrer una distancia L en esa dirección te devuelve al punto de partida. Para calcular la fuerza, hay un truco elegante: "desenrollar" el círculo en una recta infinita y reemplazar la masa por una fila infinita de **copias** separadas por L. La fuerza en el espacio enrollado es la misma que la fuerza total de todas las copias en el espacio desenrollado. Es una variante del **método de las imágenes** que William Thomson (lord Kelvin) introdujo en 1848 para resolver problemas de electrostática con conductores, y que es estándar en los libros de texto como el de John David Jackson, *Classical Electrodynamics*.

En el espacio desenrollado hay n + 1 dimensiones, así que cada copia ejerce una fuerza que cae como 1/(distancia)ⁿ. Una partícula de prueba a distancia r en el mundo visible está a distancia √(r² + (kL)²) de la copia número k. Solo cuenta la componente de la fuerza en la dirección visible, que trae un factor r/√(r² + (kL)²). Sumando:

$$ F(r) = Σₖ r / (r² + (k·L)²)^((n+1)/2),   k = …, −2, −1, 0, 1, 2, … $$

Esa es la fórmula que implementa la función `fuerza` en `src/pecera.js`.

#### 14.2 Cerca: domina la copia más próxima

Si r ≪ L, la copia k = 0 está mucho más cerca que todas las demás. Su término es r/r^(n+1) = 1/rⁿ, y el resto es una corrección chica. La fuerza es la de un mundo de n + 1 dimensiones: **pendiente −n** en el gráfico logarítmico. Para nuestro mundo, −3.

#### 14.3 Lejos: las copias se funden

Si r ≫ L, las copias están tan juntas comparadas con r que se ven como una línea continua de masa con densidad 1/L. La suma se convierte en una integral:

$$ F(r) ≈ (1/L) ∫ r / (r² + z²)^((n+1)/2) dz $$

Para n = 3, la integral vale π/(2r²), así que F ≈ π/(2L r²): **la ley de Newton**, pendiente −2, con una intensidad diluida por el factor 1/L. Para n = 2, la integral vale 2/r y F ≈ 2/(L r): la ley de Planilandia.

#### 14.4 Dónde está la transición

Igualando las dos aproximaciones se obtiene dónde cambia el comportamiento. Para n = 3: 1/r³ = π/(2L r²) da r = 2L/π ≈ 0,64 L. Para n = 2: 1/r² = 2/(L r) da r = L/2. La herramienta confirma que con L = 1 y n = 3 la pendiente vale −2,95 a r = 0,3, −2,14 a r = 1 y −2,00 a r = 20.

#### 14.5 La corrección tipo Yukawa

Lejos de la transición, la desviación respecto de la ley 1/r² no es una potencia sino una **exponencial**. Usando la fórmula de sumación de Poisson, la suma sobre copias se reescribe como una suma sobre modos de Fourier en la dimensión compacta, y el primer modo da una corrección proporcional a e^(−2πr/L). Alexandros Kehagias y Konstantinos Sfetsos calcularon esto en 2000 (*Physics Letters B*, 472, 39–44): una dimensión extra compacta se manifiesta, a distancias grandes, como un potencial de Newton más un término de Yukawa,

$$ V(r) = −(G m₁ m₂ / r) · (1 + α e^(−r/λ)) $$

con λ del orden del tamaño de la dimensión extra. Por eso los experimentos reportan sus resultados como límites en el plano (α, λ): cuán fuerte puede ser una corrección de ese tipo y a qué distancia.

#### 14.6 Cómo lo calcula el código

Sumar infinitos términos en una computadora no es posible, así que `fuerza` suma desde k = −K hasta K, con K elegido según r/L (entre 50 y 20 000 términos), y aproxima el resto con la integral analítica de la cola (función `cola`). La pendiente se calcula con una derivada numérica en escala logarítmica:

$$ pendiente ≈ [ln F(r(1+h)) − ln F(r(1−h))] / [ln(1+h) − ln(1−h)],   h = 10⁻³ $$

Los tests verifican que cerca la fuerza tenga la pendiente de una dimensión más, que lejos coincida con la ley de n dimensiones diluida en L, y que la reconstrucción de la pista 1 dé los volúmenes correctos.

#### 14.7 La pendiente, número por número

Para ver la transición con los números del código (n = 3, L = 1):

| r | Pendiente | Lectura |
|---|---|---|
| 0,01 | −3,00 | Mundo de cuatro dimensiones espaciales |
| 0,05 | −3,00 | Todavía domina la copia más cercana |
| 0,3 | −2,95 | Empieza a notarse la segunda copia |
| 1 | −2,14 | Casi en la ley de Newton |
| 20 | −2,00 | Ley de Newton, diluida por 1/L |

Con n = 2 la tabla es análoga pero desplazada un escalón: −2,00 a r = 0,05, −1,85 a r = 0,3, −1,07 a r = 1 y −1,00 a r = 20. La transición es rápida: en menos de un orden de magnitud de distancia el exponente pasa de un valor entero al otro. Por eso un experimento necesita medir a varias distancias alrededor de L; medir a una sola distancia no alcanza para ver un cambio de pendiente.

### 15. Dimensiones extra en la física de hoy

#### 15.1 La teoría de cuerdas

En los años setenta y ochenta, la teoría de cuerdas revivió las dimensiones extra por necesidad: la teoría de supercuerdas solo es consistente en diez dimensiones de espacio-tiempo. Las seis sobrantes tendrían que estar enrolladas en formas complicadas llamadas variedades de Calabi-Yau, como propusieron Philip Candelas, Gary Horowitz, Andrew Strominger y Edward Witten en 1985 (*Nuclear Physics B*, 258, 46–74). En esas versiones, las dimensiones extra son del tamaño de Planck, inaccesibles a cualquier experimento imaginable. Barton Zwiebach escribió una introducción accesible en *A First Course in String Theory* (2.ª ed., 2009).

#### 15.2 Dimensiones grandes: ADD, 1998

En 1998, Nima Arkani-Hamed, Savas Dimopoulos y Gia Dvali propusieron algo audaz (*Physics Letters B*, 429, 263–272): ¿y si las dimensiones extra no fueran diminutas sino de hasta un milímetro? Para que eso no contradiga la experiencia, las partículas del Modelo Estándar (electrones, quarks, fotones) tendrían que estar confinadas a nuestra "membrana" de tres dimensiones, y solo la gravedad se propagaría en las dimensiones extra. Eso explicaría por qué la gravedad es tan débil comparada con las otras fuerzas: se "diluye" en un volumen más grande. Es exactamente el factor 1/L que aparece en la fórmula de la sección 14.3.

Este es el modelo que la pecera ilustra mejor: nosotros somos el pez confinado a la pecera, la luz no puede salir, pero la gravedad sí "se escapa" un poco. Y se escapa lo suficiente como para que a distancias menores que L la ley de fuerza cambie.

Con dos dimensiones extra, el modelo ADD predecía desviaciones de la ley de Newton por debajo del milímetro. Eso lo volvió falsable con experimentos de mesa.

#### 15.3 Randall y Sundrum, 1999

Lisa Randall y Raman Sundrum propusieron en 1999 dos modelos con una sola dimensión extra **curvada** (*Physical Review Letters*, 83, 3370 y 4690). En el segundo, la dimensión extra puede ser incluso infinita, y aun así la gravedad se ve de cuatro dimensiones porque la curvatura la "localiza" cerca de nuestra membrana. Es una pecera sin vidrio del otro lado. Randall lo cuenta para el público general en *Warped Passages* (2005).

### 16. Midiendo la pendiente: balanzas de torsión y aceleradores

#### 16.1 La balanza de Cavendish, reinventada

La pista 2 de la herramienta es, en el fondo, un experimento: medir la fuerza entre dos masas a distintas distancias y ver si la pendiente cambia. El grupo Eöt-Wash de la Universidad de Washington, dirigido por Eric Adelberger, Blayne Heckel y colaboradores, construyó balanzas de torsión que miden la gravedad entre masas separadas por décimas de milímetro. En 2001, Hoyle y colaboradores publicaron que la ley 1/r² se cumple hasta 218 µm (*Physical Review Letters*, 86, 1418). En 2007, Kapner y colaboradores bajaron el límite a 56 µm (*PRL*, 98, 021101). En 2020, Lee y colaboradores lo llevaron a 52 µm (*PRL*, 124, 101101).

Traducido al lenguaje de la herramienta: si hay una dimensión extra a la que la gravedad acceda, su tamaño L tiene que ser menor que unas decenas de micrómetros. A esas distancias, la gravedad es tan débil que cualquier otra fuerza (electrostática, efecto Casimir, el aire) la tapa, y los experimentos tienen que blindar todo con una precisión extraordinaria. Adelberger, Heckel y Nelson resumieron el estado del área en una revisión de 2003 (*Annual Review of Nuclear and Particle Science*, 53, 77–121).

#### 16.2 Aceleradores

Si la gravedad se escapa a dimensiones extra, en una colisión de alta energía podrían crearse gravitones que se van de la pecera llevándose energía. El detector vería un "agujero" en el balance de energía: un chorro de partículas de un lado y nada del otro. Los experimentos ATLAS y CMS del LHC buscaron esa señal y la de mini agujeros negros sin encontrarlas, lo que pone límites a los modelos ADD y Randall-Sundrum en la escala de varios TeV. El Particle Data Group mantiene una revisión actualizada de estos límites (Workman et al., 2022).

#### 16.3 Ondas gravitacionales que se escapan

En agosto de 2017, los detectores LIGO y Virgo registraron la onda gravitacional de dos estrellas de neutrones que se fusionaron a unos 40 megapársecs (el evento GW170817), y telescopios de todo el mundo vieron la luz de la misma explosión. Eso permitió una prueba nueva de la pecera: si la gravedad se escapara a dimensiones extra grandes, la onda gravitacional se debilitaría con la distancia más rápido que la luz, que queda confinada a nuestra membrana. Comparando la distancia estimada con las dos señales, Kris Pardo, Maya Fishbach, Daniel Holz y David Spergel concluyeron en 2018 que, a escalas de decenas de megapársecs, el número de dimensiones por las que se propaga la gravedad es compatible con cuatro (*Journal of Cosmology and Astroparticle Physics*, 2018(07), 048). Es la pista 2 de la herramienta aplicada a escala cosmológica: medir cómo se "diluye" una señal para contar dimensiones.

#### 16.4 Lo que esto dice de la pecera

Hoy sabemos que, si la pecera existe, su "vidrio" está a menos de unas decenas de micrómetros en la dirección escondida, o que solo la gravedad lo atraviesa de un modo muy sutil. Eso no descarta la idea; la acota. Y esa es exactamente la diferencia entre una especulación y una hipótesis científica.

### 17. Platón, el pez y los límites del conocimiento

La imagen de alguien que solo ve sombras de una realidad más amplia es antigua. En el libro VII de la *República*, Platón describe prisioneros encadenados en una caverna que solo ven las sombras que proyectan en la pared objetos que pasan detrás de ellos. Para los prisioneros, las sombras son la realidad. La pista 1 de la herramienta es una caverna con una diferencia crucial: el habitante del plano no se resigna, **mide**. Registra el área, apila los cortes, calcula un volumen. No sale de la caverna, pero razona sobre lo que hay afuera a partir de regularidades en las sombras.

Esa es también la postura de Ernst Mach y de buena parte de la física del siglo XX: una entidad que no tiene ninguna consecuencia observable no forma parte de la teoría. Las dimensiones extra entraron a la física cuando dejaron de ser metáforas y empezaron a predecir números medibles, como la pendiente de una fuerza a 50 micrómetros.

### 18. Confusiones comunes sobre la "cuarta dimensión"

Cuando se habla de dimensiones extra aparecen siempre las mismas confusiones. Vale la pena desarmarlas antes de usar la herramienta para escribir o enseñar.

**"La cuarta dimensión es el tiempo."** En la relatividad especial, Hermann Minkowski mostró en 1908 (conferencia *Raum und Zeit*, publicada en 1909) que espacio y tiempo forman un continuo de cuatro dimensiones, el espacio-tiempo. Pero el tiempo no es una cuarta dimensión **espacial**: entra en la geometría con un signo distinto, y por eso no se puede "girar" un objeto hacia el pasado como se lo gira hacia la izquierda. La pecera de la herramienta habla de una dimensión espacial adicional, además del tiempo. En el modelo ADD, por ejemplo, el espacio-tiempo tendría 4 + n dimensiones: tres espaciales grandes, n espaciales chicas y el tiempo.

**"Una dimensión extra sería un lugar al que se puede viajar."** No necesariamente. Si la dimensión es un círculo de 10 µm, "viajar" en esa dirección es dar una vuelta de 10 µm y volver al mismo punto. No hay un "otro lado" donde vivan otras cosas, salvo en modelos específicos con varias membranas, como el primero de Randall y Sundrum.

**"Si hubiera más dimensiones, lo veríamos."** Solo si la luz puede propagarse en ellas. En los modelos de membrana, todo lo que usamos para ver y tocar (fotones, electrones, la química) está pegado a nuestras tres dimensiones. Solo la gravedad, la fuerza más débil y la más difícil de medir a corta distancia, sentiría el afuera. Eso explica por qué las pruebas más directas son balanzas de torsión y no microscopios.

**"Más dimensiones significa más fuerza."** Al revés: si la gravedad se reparte en más dimensiones, a distancias grandes se ve **más débil**, diluida por el factor 1/L. Solo a distancias menores que L se ve más intensa que lo que predice Newton, porque crece con un exponente mayor.

**"Planilandia es solo una metáfora."** Es una metáfora, pero también un laboratorio real. Hay sistemas físicos que se comportan como mundos de dos dimensiones: los electrones en el grafeno o en las interfaces de semiconductores (donde se observó el efecto Hall cuántico), las películas de jabón, los gases de átomos fríos atrapados en planos. En ellos se miden leyes de fuerza y comportamientos propios de dos dimensiones, y a veces la "tercera dimensión" se delata exactamente como en la pista 2: cuando el espesor de la película deja de ser despreciable frente a las distancias medidas.

### 19. Cómo usar la herramienta para escribir

La idea original contemplaba un ensayo o un cuento. La herramienta sirve de andamio, porque cada pista sugiere una estructura narrativa distinta.

**Con la pista 1: el misterio.** Un personaje plano registra apariciones inexplicables. Primero las anota como anomalías (el registro de área). Después nota regularidades: siempre crecen y se achican, el total sumado es constante. Por último formula la hipótesis de un objeto más grande que pasa a través de su mundo (la deducción). Es la estructura de *Flatland* y también la del método científico según Charles Sanders Peirce: abducción (proponer una explicación), deducción (sacar consecuencias) e inducción (ponerlas a prueba).

**Con la pista 2: la medición.** Un personaje construye un instrumento cada vez más fino para medir una fuerza a distancias cada vez más cortas y, a partir de cierto punto, la pendiente cambia. Es menos espectacular que una esfera que aparece de la nada, pero es más verosímil y más cercano a cómo trabajan de verdad los grupos de investigación. La tensión dramática está en la duda: ¿la desviación es una dimensión escondida o un error de calibración, una carga electrostática, una vibración?

**Con las dos: el ensayo.** Un ensayo puede contrastar las dos pistas como dos formas de conocer: la del testigo de un evento extraordinario y la del metrólogo que acumula datos. La primera convence de inmediato pero es difícil de repetir; la segunda tarda décadas pero es acumulativa. La historia de las dimensiones extra, de Kaluza a los experimentos del grupo Eöt-Wash, es un ejemplo de que la ciencia avanza sobre todo por la segunda.

En cualquiera de los casos, conviene respetar los números: decir "a menos de 50 micrómetros" en vez de "en un lugar inalcanzable" hace más creíble y más interesante el texto.

### 20. ¿Tiene bordes nuestra pecera? La forma del universo

La pecera de la idea tiene una dimensión escondida. Hay una pregunta vecina que la cosmología sí investiga con datos: si nuestro espacio de tres dimensiones, sin ninguna dimensión extra, podría estar "cerrado sobre sí mismo", como la pantalla de un videojuego antiguo en el que salir por la derecha te devuelve por la izquierda. Sería una pecera sin vidrio, pero con forma.

#### 20.1 Curvatura y topología

La relatividad general dice cómo se curva el espacio localmente, pero no dice cuál es su forma global, su **topología**. Un espacio plano puede ser infinito o puede ser un **toro** de tres dimensiones: finito, sin bordes, y tal que viajando en línea recta se vuelve al punto de partida. Para un habitante, un universo así se vería como una sala de espejos: las mismas galaxias aparecerían repetidas en distintas direcciones, a distancias que son múltiplos del tamaño del universo. Es la tercera dimensión enrollada de la pista 2, pero sin ninguna dimensión extra: son las tres que conocemos las que se cierran.

#### 20.2 Círculos en el cielo

¿Cómo se detectaría? Neil Cornish, David Spergel y Glenn Starkman propusieron en 1998 (*Classical and Quantum Gravity*, 15(9), 2657–2670) un método elegante. El fondo cósmico de microondas que vemos proviene de una esfera, la superficie de la última dispersión. Si el universo es más chico que esa esfera y se cierra sobre sí mismo, la esfera se corta consigo misma en sus copias, y la intersección de dos esferas es un círculo. Habría entonces pares de **círculos en el cielo** con el mismo patrón de temperaturas, vistos desde dos direcciones distintas. Es, otra vez, la idea de deducir la forma desde adentro, con los cortes de la pista 1 aplicados a una esfera de luz.

#### 20.3 El universo dodecaédrico

En 2003, Jean-Pierre Luminet, Jeffrey Weeks y colaboradores propusieron en *Nature* (425, 593–595) que algunas anomalías del fondo cósmico medido por el satélite WMAP (en particular, que las fluctuaciones de mayor escala angular eran más débiles de lo esperado) podían explicarse si el universo tuviera la forma del **espacio dodecaédrico de Poincaré**: un dodecaedro cuyas caras opuestas están identificadas, de modo que salir por una cara devuelve por la opuesta, girado. Un universo así sería finito y relativamente chico, y su tamaño limitaría las ondas más largas posibles, como el tamaño de un instrumento limita sus notas más graves.

La propuesta era falsable: predecía círculos en el cielo con un patrón determinado. Las búsquedas posteriores no los encontraron.

#### 20.4 Lo que dicen los datos

La colaboración Planck buscó sistemáticamente señales de topología no trivial en sus mapas del fondo cósmico (*Astronomy & Astrophysics*, 594, A18, 2016) y no encontró ninguna. Su conclusión es que, si el universo se cierra sobre sí mismo, su tamaño tiene que ser comparable o mayor que la distancia a la superficie de la última dispersión, unos 14 000 megapársecs en distancia comóvil: lo bastante grande como para que, en la práctica, ninguna repetición sea visible.

Es la misma estructura de resultado que el de las balanzas de torsión de la sección 16: no se encontró el efecto, y la búsqueda pone una cota. Si la pecera existe, ya sea en una dimensión extra o en la forma de las tres conocidas, su "vidrio" está o muy cerca (por debajo de decenas de micrómetros en la dimensión escondida) o muy lejos (más allá del horizonte observable). La región intermedia, la de una pecera que se notaría a simple vista, está descartada.

#### 20.5 Para el cuento

La forma del universo da un recurso narrativo distinto del de la dimensión extra: un personaje que mira con un telescopio cada vez más potente y, en el límite, ve en una dirección la misma galaxia que ve en la opuesta. No necesita salir de la pecera para descubrir que es una pecera: le alcanza con mirar lo bastante lejos. Es el razonamiento de Gauss y Riemann (sección 11) llevado al cosmos, y es la versión de la idea que hoy más se parece a un experimento posible.

### 21. Del modelo al código

| Concepto | Función en `src/pecera.js` | Qué produce en la página |
|---|---|---|
| Corte de un objeto con el plano | `corte(objeto, z)` | Las figuras del panel "Desde adentro" |
| Área total de las figuras | `area(figuras)` | La curva del registro |
| Registro temporal | `registro(objeto, n)` | El gráfico de área en el tiempo y el conteo de piezas |
| Principio de Cavalieri | `volumenInferido(objeto)` | El volumen estimado (4,19 para la esfera) |
| Método de las imágenes | `fuerza(r, n, L)` | La curva del gráfico de la pista 2 |
| Cola de la suma como integral | `cola(r, Z, n)` | Precisión de la suma con pocos términos |
| Exponente efectivo | `pendiente(r, n, L)` | "Pendiente cerca" y "Pendiente lejos" |

Para usarlo desde Node:

```js
const P = require("./src/pecera.js");
P.volumenInferido("esfera");    // ≈ 4,1888
P.pendiente(0.01, 3, 1);        // ≈ −3,00
P.pendiente(100, 3, 1);         // ≈ −2,00
```

### 22. Ejercicios

1. Calculá a mano qué ve el habitante del plano cuando un cono con la punta **abajo** lo atraviesa. ¿Cambia el volumen inferido?
2. Un cubo cruza el plano apoyado sobre un vértice, con la diagonal principal vertical. Dibujá los cortes. ¿En qué momento aparece un hexágono regular?
3. Demostrá que el hipervolumen de una bola de cuatro dimensiones de radio R es π²R⁴/2 sumando volúmenes de esferas tridimensionales.
4. En la pista 2, con n = 3, ¿para qué L la pendiente a r = 0,1 vale −2,5? Probalo con el deslizador.
5. Si la gravedad tuviera dos dimensiones extra de tamaño 50 µm, ¿con qué exponente caería a 10 µm?
6. Leé el argumento de Ehrenfest sobre órbitas en cuatro dimensiones. Con la fuerza 1/r³ y un potencial efectivo que incluya el término centrífugo L²/(2mr²), mostrá que no hay mínimo y que las órbitas circulares son inestables.
7. Escribí una escena de un cuento en la que un personaje deduce la dimensión extra con la pista 2. ¿Qué instrumento usaría, y qué tendría que blindar?

### 23. Glosario

- **Corte (sección):** intersección de un objeto con un plano.
- **Principio de Cavalieri:** dos sólidos con secciones de igual área a cada altura tienen igual volumen.
- **Geometría intrínseca:** propiedades de un espacio que se pueden medir sin salir de él (distancias, ángulos, curvatura).
- **Dimensión compacta (enrollada):** una dirección del espacio que se cierra sobre sí misma con un tamaño finito L.
- **Método de las imágenes:** reemplazar una condición de borde o una geometría periódica por copias ficticias de las fuentes.
- **Exponente efectivo (pendiente):** d(log F)/d(log r); vale −(d−1) en un espacio de d dimensiones grandes.
- **Torre de Kaluza-Klein:** la serie de partículas de masa creciente que aparecen al cuantizar el movimiento en una dimensión compacta.
- **Potencial de Yukawa:** corrección exponencial e^(−r/λ) a una ley de potencias.

### 24. Conclusión

La pecera dimensional parece una fantasía, pero la pregunta "¿cómo se deduce un afuera desde adentro?" tiene respuestas concretas. Por los cortes: objetos que aparecen, cambian y desaparecen sin causa visible, y cuyos registros, sumados, revelan magnitudes que no se ven, como sabían Arquímedes y Cavalieri y como hace hoy un tomógrafo. Por las fuerzas: una ley de gravedad que cambia de exponente a distancias cortas, como predicen los modelos de Kaluza-Klein, ADD y Randall-Sundrum y como buscan las balanzas de torsión del grupo Eöt-Wash. La primera pista sirve para un cuento; la segunda es un programa de investigación con resultados: si la pecera existe, su dimensión escondida mide menos de unas decenas de micrómetros.

La herramienta deja abiertas dos líneas: agregar la luz que se dobla al cruzar el borde de la pecera (lo que Gauss y Riemann llamarían curvatura) y objetos que rotan al atravesar el plano. Y una tercera, literaria: usar las dos pistas como estructura de un relato en el que alguien, sin salir nunca, descubre la forma de su mundo.

## Referencias

- Abbott, E. A. (1884). *Flatland: A Romance of Many Dimensions*. Londres: Seeley & Co.
- Adelberger, E. G., Heckel, B. R., & Nelson, A. E. (2003). Tests of the gravitational inverse-square law. *Annual Review of Nuclear and Particle Science*, 53, 77–121. https://doi.org/10.1146/annurev.nucl.53.041002.110503
- Arkani-Hamed, N., Dimopoulos, S., & Dvali, G. (1998). The hierarchy problem and new dimensions at a millimeter. *Physics Letters B*, 429(3–4), 263–272. https://doi.org/10.1016/S0370-2693(98)00466-3
- Banchoff, T. F. (1990). *Beyond the Third Dimension: Geometry, Computer Graphics, and Higher Dimensions*. Scientific American Library. ISBN 978-0-7167-5025-3.
- Burger, D. (1965). *Sphereland: A Fantasy About Curved Spaces and an Expanding Universe* (trad. C. J. Rheinboldt). Thomas Y. Crowell.
- Candelas, P., Horowitz, G. T., Strominger, A., & Witten, E. (1985). Vacuum configurations for superstrings. *Nuclear Physics B*, 258, 46–74. https://doi.org/10.1016/0550-3213(85)90602-9
- Cavalieri, B. (1635). *Geometria indivisibilibus continuorum nova quadam ratione promota*. Bolonia: Clemente Ferroni.
- Cornish, N. J., Spergel, D. N., & Starkman, G. D. (1998). Circles in the sky: Finding topology with the microwave background radiation. *Classical and Quantum Gravity*, 15(9), 2657–2670. https://doi.org/10.1088/0264-9381/15/9/013
- Dewdney, A. K. (1984). *The Planiverse: Computer Contact with a Two-Dimensional World*. Poseidon Press.
- Ehrenfest, P. (1917). In what way does it become manifest in the fundamental laws of physics that space has three dimensions? *Proceedings of the Royal Netherlands Academy of Arts and Sciences*, 20, 200–209.
- Gauss, C. F. (1827). *Disquisitiones generales circa superficies curvas*. Gotinga: Dieterich.
- Heath, T. L. (Ed.). (1912). *The Method of Archimedes, Recently Discovered by Heiberg*. Cambridge University Press.
- Hinton, C. H. (1904). *The Fourth Dimension*. Londres: Swan Sonnenschein.
- Hoyle, C. D., Schmidt, U., Heckel, B. R., Adelberger, E. G., Gundlach, J. H., Kapner, D. J., & Swanson, H. E. (2001). Submillimeter test of the gravitational inverse-square law: A search for "large" extra dimensions. *Physical Review Letters*, 86(8), 1418–1421. https://doi.org/10.1103/PhysRevLett.86.1418
- Jackson, J. D. (1999). *Classical Electrodynamics* (3.ª ed.). Wiley. ISBN 978-0-471-30932-1.
- Kaluza, T. (1921). Zum Unitätsproblem der Physik. *Sitzungsberichte der Preussischen Akademie der Wissenschaften*, 966–972.
- Kant, I. (1747). *Gedanken von der wahren Schätzung der lebendigen Kräfte*. Königsberg: Dorn.
- Kapner, D. J., Cook, T. S., Adelberger, E. G., Gundlach, J. H., Heckel, B. R., Hoyle, C. D., & Swanson, H. E. (2007). Tests of the gravitational inverse-square law below the dark-energy length scale. *Physical Review Letters*, 98(2), 021101. https://doi.org/10.1103/PhysRevLett.98.021101
- Kehagias, A., & Sfetsos, K. (2000). Deviations from the 1/r² Newton law due to extra dimensions. *Physics Letters B*, 472(1–2), 39–44. https://doi.org/10.1016/S0370-2693(99)01421-5
- Klein, O. (1926). Quantentheorie und fünfdimensionale Relativitätstheorie. *Zeitschrift für Physik*, 37(12), 895–906. https://doi.org/10.1007/BF01397481
- Lee, J. G., Adelberger, E. G., Cook, T. S., Fleischer, S. M., & Heckel, B. R. (2020). New test of the gravitational 1/r² law at separations down to 52 μm. *Physical Review Letters*, 124(10), 101101. https://doi.org/10.1103/PhysRevLett.124.101101
- Luminet, J.-P., Weeks, J. R., Riazuelo, A., Lehoucq, R., & Uzan, J.-P. (2003). Dodecahedral space topology as an explanation for weak wide-angle temperature correlations in the cosmic microwave background. *Nature*, 425, 593–595. https://doi.org/10.1038/nature01944
- Milnor, J. (1963). *Morse Theory*. Princeton University Press. ISBN 978-0-691-08008-6.
- Minkowski, H. (1909). Raum und Zeit. *Physikalische Zeitschrift*, 10, 104–111.
- Pardo, K., Fishbach, M., Holz, D. E., & Spergel, D. N. (2018). Limits on the number of spacetime dimensions from GW170817. *Journal of Cosmology and Astroparticle Physics*, 2018(07), 048. https://doi.org/10.1088/1475-7516/2018/07/048
- Peirce, C. S. (1903). *Harvard Lectures on Pragmatism*. En *The Essential Peirce*, vol. 2 (1998). Indiana University Press.
- Planck Collaboration. (2016). Planck 2015 results. XVIII. Background geometry and topology of the Universe. *Astronomy & Astrophysics*, 594, A18. https://doi.org/10.1051/0004-6361/201525829
- Platón. (ca. 375 a. C.). *República*, libro VII.
- Radon, J. (1917). Über die Bestimmung von Funktionen durch ihre Integralwerte längs gewisser Mannigfaltigkeiten. *Berichte der Sächsischen Akademie der Wissenschaften zu Leipzig, Math.-Phys. Klasse*, 69, 262–277.
- Randall, L. (2005). *Warped Passages: Unraveling the Mysteries of the Universe's Hidden Dimensions*. Ecco. ISBN 978-0-06-053108-9.
- Randall, L., & Sundrum, R. (1999). An alternative to compactification. *Physical Review Letters*, 83(23), 4690–4693. https://doi.org/10.1103/PhysRevLett.83.4690
- Randall, L., & Sundrum, R. (1999). Large mass hierarchy from a small extra dimension. *Physical Review Letters*, 83(17), 3370–3373. https://doi.org/10.1103/PhysRevLett.83.3370
- Riemann, B. (1868). Über die Hypothesen, welche der Geometrie zu Grunde liegen. *Abhandlungen der Königlichen Gesellschaft der Wissenschaften zu Göttingen*, 13, 133–150.
- Rucker, R. (1984). *The Fourth Dimension: A Guided Tour of the Higher Universes*. Houghton Mifflin. ISBN 978-0-395-34424-1.
- Workman, R. L., et al. (Particle Data Group). (2022). Review of particle physics. *Progress of Theoretical and Experimental Physics*, 2022(8), 083C01. https://doi.org/10.1093/ptep/ptac097
- Zwiebach, B. (2009). *A First Course in String Theory* (2.ª ed.). Cambridge University Press. ISBN 978-0-521-88032-9.
