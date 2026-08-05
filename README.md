# Fin de Mes

Un juego narrativo de decisiones. Tenés veintidós años, tu primer trabajo en blanco, y
diez años por delante en un país donde los precios llegan antes que los sueldos.

No es una app de finanzas. No hay planillas, no hay presupuestos, no hay consejos. Hay
escenas, decisiones y consecuencias que aparecen meses después, cuando ya te olvidaste
de qué habías elegido.

## La idea

La gente no maneja mal la plata por falta de información. La maneja mal porque las
consecuencias de una decisión financiera llegan años más tarde, cuando ya no se pueden
asociar con la causa.

Un juego es la única forma de arreglar eso: comprime diez años en veinte minutos y te
hace *sentir* el resultado de algo que elegiste al minuto tres.

## Reglas de diseño

Tres decisiones de diseño sostienen todo lo demás. Si alguna se rompe, el juego enseña
cosas falsas y es peor que no existir.

**1. Ninguna opción es la correcta.** Ahorrar todo también sale caro: si nunca viajás,
nunca salís y nunca te comprás nada, el ánimo se te va al piso y el epílogo te lo cobra.
La plata es un medio. Un juego que premia solo acumular enseña a ser miserable, no a ser
prudente.

**2. No se puede ganar prediciendo.** El régimen económico se sortea al empezar, está
oculto, y cambia solo cada uno o dos años. El dólar empata con la inflación en el largo
plazo: se atrasa durante meses —y ahí el que está dolarizado pierde contra los precios— y
después corrige de golpe. El plazo fijo a veces le gana a la inflación y a veces no. Si
existiera una jugada que gana siempre, no habría nada que aprender.

**3. El puntaje no es el patrimonio.** La métrica principal es el **aire**: cuántos meses
podrías vivir si mañana se corta el ingreso. Si el puntaje fuera la plata final, el juego
enseñaría a apostar y ganaría el que arriesgó todo y tuvo suerte.

## Lo que enseña sin explicar

- Los gastos se ajustan por inflación **todos los meses**. El sueldo se ajusta cada cinco
  o seis, y casi siempre por debajo. Nadie te explica la licuación: la ves en el resumen
  de fin de mes y te da bronca.
- Las cuotas fijas sin interés, con inflación alta, **juegan a tu favor**. El problema
  nunca es una cuota: son seis al mismo tiempo.
- La deuda de tarjeta es lo único que crece más rápido que la inflación.
- El colchón no sirve para ganar plata. Sirve para no tener que aceptar la primera cosa
  que aparezca cuando te echan.
- Nadie te presta infinito. Cuando se corta el crédito, no queda otra que achicarse.

Al final, el juego compara **tu mismo flujo de plata** contra cinco estrategias mecánicas
—todo en pesos, todo a plazo fijo, todo a dólares, todo al índice global, todo al bono—
sobre el escenario exacto que te tocó. Ahí está el aprendizaje, más que en la partida.

## Cómo jugarlo

Es un solo archivo HTML sin dependencias. Alcanza con abrirlo:

```bash
python3 -m http.server 8000
# y entrar a http://localhost:8000
```

O directamente `open index.html`. Funciona sin internet y guarda la partida en curso en
el navegador.

## Estructura

```
index.html    Todo: motor económico, contenido narrativo e interfaz
```

El contenido vive en dos listas al final del archivo:

- `HITOS` — escenas fijas que se disparan en un mes determinado y en orden. Son la
  columna vertebral: primer sueldo, la tarjeta, el primer aumento que no alcanza, el
  despido, la pareja.
- `EVENTOS` — bolsa aleatoria de la vida diaria. Las marcadas `repetible: true` pueden
  volver a aparecer después de veinte meses. Algunas están condicionadas al estado del
  país: `dolar-barato` solo aparece cuando el tipo de cambio está atrasado, y
  `pre-eleccion` cuando faltan menos de cuatro meses para votar.

Hay además una lista de `urgentes` en `escenaDisponible()`: escenas que tapan cualquier
otra cosa que esté pasando (quedarte sin trabajo, el bajón anímico, la elección).

Agregar una escena nueva es agregar un objeto a una de las dos listas. Cada opción tiene
un `hacer()` que modifica el estado y devuelve el texto de la consecuencia.

## Veinte maneras de arrancar

El comienzo se elige en dos ejes: **dónde vivís** y **de qué laburás**. Cinco por cuatro dan
veinte arranques distintos sin que el juego dure un minuto más — son dos toques en vez de
uno. Cada opción muestra su dificultad en tres puntos, así nadie firma la partida más brava
sin enterarse.

Y enseña algo que el juego no decía: **la forma de tu ingreso importa tanto como el monto**.

| Trabajo | Cobra | Qué le falta |
|---|---|---|
| Empleado en blanco | $900.000 | — |
| Monotributista | $1.120.000 | Sin aguinaldo, sin indemnización, y lo que entra varía cada mes |
| Negocio familiar | $960.000 | Lo que entra sigue a la economía: en crisis vende menos |
| Changas y facultad | $560.000 | Poco ahora, con la promesa de un salto |

El monotributista cobra 24% más que el empleado y termina peor en casi todos los casos: el
aguinaldo es un mes de sueldo por año, la indemnización es el colchón que no tuviste que
juntar, y un mes flojo no lo cubre nadie. Medido sobre las veinte combinaciones, llegar a
los diez años va del 23% al 75% según cómo arranques.

Antes de todo eso hay una pantalla que pregunta tu nombre, y aparece después en boca de los
personajes y en el epílogo.

## Lo que elegís al principio te lleva por otro lado

Elegir el arranque no cambiaba solamente los números iniciales: ahora **abre escenas que
las otras partidas no ven**. Cada camino tiene entre dos y tres situaciones propias, y son
las que le enseñan a ese camino lo que ese camino tiene para enseñar.

| Arranque | Lo que te pasa a vos y a nadie más | Qué te deja |
|---|---|---|
| Monotributista | Facturaste el mejor mes del año y cobrás a 90 días | Facturar no es cobrar: el que trabaja solo se funde por el tiempo entre las dos cosas |
| Negocio familiar | Vendiste bien y reponer esa mercadería salió más caro | Costo de reposición: la ganancia se mide contra lo que va a costar volver a tenerlo |
| Empleado en blanco | Te ofrecen 42% más en mano, todo en negro | Lo que no ves del sueldo: obra social, aguinaldo, indemnización, historial crediticio |
| Changas y facultad | Te recibís y el sueldo salta entre 1,75× y 2,3× | El capital humano es lo único que la inflación no licúa |
| Vivís solo | El costo fijo que no se divide, y un problema chico un viernes a la noche | Bajar un gasto fijo rinde más que cualquier inversión; y hay urgencias que solo se pagan con plata líquida |
| Compartido | Se va un compañero y el alquiler sigue igual | Compartir baja el costo y suma un riesgo que no estaba en la cuenta |
| Del interior | Un casamiento allá, y la oferta de volverte | La distancia se paga todos los años; lo que define cuánto guardás no es el sueldo, es la resta |
| En pareja | Los suegros, y la charla de plata que nunca tuvieron | Dos economías que no se hablan son dos problemas, no uno |

Medido sobre 40 partidas por combinación, las veinte reciben sus escenas propias entre el
80% y el 100% de las veces.

### Y las escenas compartidas cambian de piel

Tener escenas propias no alcanzaba. El problema más visible era el otro: las escenas que sí
comparten todos **contaban una vida que no era la tuya**. A un monotributista le llegaba una
paritaria. Al del negocio familiar lo echaban por reestructuración. A los dos les ofrecían
manejar un equipo de cuatro personas.

Ahora `texto` puede ser un objeto indexado por cómo te ganás la vida, con sus propias
variantes adentro. Y las opciones se filtran igual, así que **no cambian los sustantivos:
cambia la decisión**.

| La misma escena | Empleado | Por tu cuenta | Negocio familiar | Estudiando |
|---|---|---|---|---|
| El aumento anual | Te dan menos que la inflación: ¿pedís más? | Nadie te actualiza: ¿te subís el precio vos? | ¿Remarcás con la lista nueva o aguantás la clientela? | ¿Cobrás más la hora o priorizás rendir? |
| Perder el ingreso | Reestructuración | Se te cae el cliente que era la mitad | El local no cubre los costos hace cuatro meses | Se terminó la changa en mitad de la cursada |
| La oferta del año 2 | Te busca otra empresa | Te ofrecen entrar en relación de dependencia | Te ofrecen un puesto y tu viejo se queda solo | Un full time que no te deja cursar |
| Manejar gente | Te ofrecen un equipo | ¿Tomás a alguien y le pagás cobres o no? | ¿Ponés un encargado en el local? | — |
| La plata que cae de golpe | Bono por objetivos | Un cliente te paga tres facturas juntas | Diciembre, el local no para en tres semanas | Sale la beca |

La del año 2 es la que más se ramifica: dejar la facultad cierra el hito de recibirse para
siempre, y entrar en relación de dependencia te apaga las escenas de facturar y te enciende
las de estar en blanco. Lo que elegís en el mes 22 decide qué situaciones existen en el 60.

Hay un chequeo dedicado a esto (`coherencia.js`): renderiza el texto de las 69 escenas en
las cuatro vidas y busca palabras que no correspondan —"tu jefe", "aguinaldo", "paritaria",
"indemnización"— con una lista de excepciones para los casos donde la palabra aparece
justamente porque *eso* es lo que no tenés.

## La escalera

Los instrumentos no están todos disponibles desde el minuto uno: se habilitan según cuánto
**aire líquido** tengas — plata que podés usar mañana, no patrimonio.

| Escalón | Se abre con | Qué enseña |
|---|---|---|
| Plazo fijo | medio mes | Tasa real: el número solo no dice nada, la resta contra la inflación sí |
| Dólares | 1,5 meses | Cambiar de riesgo no es sacárselo de encima |
| Bono del país | 4 meses | El cupón alto es el precio del miedo, no un regalo |
| Índice global | 6 meses | Sube a diez años y en el medio se cae un 30% |

No se pueden saltear escalones. Es la regla que más plata le ahorra a la gente y que casi
nadie respeta: **primero el colchón, después invertir**. Querer comprar bonos sin tener
para el mes que viene no es ser audaz, es no haber entendido el orden.

## Elecciones

Cada cuatro años hay elección, y es el único momento del juego con fecha conocida. Lo que
no se sabe es el resultado ni cómo va a reaccionar el mercado. Los meses previos el bono
se hunde porque nadie quiere quedarse con papeles.

**El precio no se mueve según quién ganó, sino según cuánto se apartó de lo que ya estaba
descontado.** Si el bono subiera siempre con un signo político, el juego enseñaría a
apostarle a ese signo — que es falso y convertiría esto en un panfleto. Los partidos son
abstractos a propósito: "el sector del ajuste" y "el del gasto", sin nombres ni colores.

El bono puede entrar en default, con quita de entre el 55% y el 78%. Pasa en el 3% de las
partidas, y solo en crisis — que es exactamente cuando el bono se ve barato.

## Revisión anual de cartera

Una vez por año de juego ves toda tu plata junta y podés reacomodar cómo está repartida.
Diez momentos en toda la partida, a propósito: si pudieras tocar la cartera todos los
meses, esto sería un simulador de trading, que es lo contrario de lo que queremos enseñar.

Cada activo tiene su propia perilla y se mueve sola. Lo que bajás queda como **saldo sin
asignar** y lo ponés donde quieras — que es como se reparte plata de verdad. Ninguna perilla
puede pasarse de lo que haya libre: si arrastrás de más, vuelve sola. Debajo de cada una se
ve en pesos cuánto queda ahí, y el botón de aplicar espera a que no quede saldo suelto.

Mover plata paga comisión (0,8% por operación, más el spread del dólar), así que
rebalancear por rebalancear cuesta — y eso también es parte de la lección.

## Conceptos y logros

No hay tutorial ni glosario para leer al principio. Cada uno de los **26 conceptos** se
desbloquea el mes exacto en que te pasa, y recién ahí se te nombra lo que acabás de vivir:
la licuación aparece cuando cerrás una paritaria por debajo de la inflación, la tasa real
el mes que tu plazo fijo rinde menos que los precios, el riesgo de contraparte cuando le
prestás a un amigo.

Al final ves cuáles te faltan. No están escondidos: aparecen si tomás otras decisiones.
Ahí está el motivo para jugar de nuevo.

Los **10 logros** están puestos en lo difícil de sostener diez años: no deber nunca, pasar
una crisis sin endeudarte, no vender los dólares en el pico, terminar con el ánimo alto.

## Cada vida tiene su guion

Al empezar una partida se sortean tres cosas: **en qué mes cae cada hito** dentro de su
ventana, **cuáles ocurren** y cuáles no, y **qué parte del catálogo de eventos existe** en
esa vida. Los personajes se sortean enteros: o Pedro está en tu vida o no está, porque si
apareciera solo el capítulo tres el arco se sentiría roto.

Antes los hitos disparaban en el mes exacto y sin excepción —primer sueldo mes 1, tarjeta
mes 3, el primer aumento corto mes 13— así que los primeros cuatro años eran idénticos
partida tras partida.

```
parecido entre dos partidas         69%  ->  48%
escenas que salen en más del 75%     37  ->   8
```

El problema de fondo no era que faltara contenido: con 59 escenas y unas 57 pantallas por
partida, veías el catálogo entero siempre. No había nada que quedara afuera.

## Variantes de texto

Que el súper, la heladera o un casamiento vuelvan dos o tres veces en diez años es
correcto — así es la vida. Lo que rompe la inmersión es leer **el mismo párrafo** otra vez.

Por eso `texto` puede ser una lista en vez de una función: se elige la versión según cuántas
veces viste esa escena. Veinticuatro escenas tienen tres versiones cada una, y muchas
aprovechan para saber que es la segunda vez ("otra vez", "la tercera elección de tu vida
adulta"). Así la repetición deja de ser un bache y pasa a ser continuidad.

El bajón anímico además **escala**: la primera vez es cansancio, la segunda es la cuenta de
todos los meses que venís empujando, la tercera ya no es un bajón sino cómo estás. Tiene
cinco versiones porque es la escena que más vuelve — es la red que evita el final por
quiebre, así que no se puede espaciar sin romper el juego. Se probó: llevar su espera de 7
a 11 meses bajó el texto repetido pero subió el quiebre del 13% al 53% en manos de un
jugador que decide bien. Se volvió atrás y se resolvió escribiendo más variantes.

Medido sobre 400 partidas, pantallas que muestran texto ya leído:

```
antes de las variantes   26 de 66   (39%)
después                 3,3 de 52   ( 6%)
```

## La gente que vuelve

Antes cada escena traía "un amigo" distinto y las repeticiones se sentían repeticiones.
Ahora vuelven cuatro personas con nombre y arco propio a lo largo de la década:

- **Pedro**, el que siempre tiene el dato. Eufórico con la pantalla en verde, después deja
  el laburo para operar, después se funde — o la pega, una de cada cinco veces. Su historia
  avanza sola, la acompañes o no: la lección es que el que te muestra la captura nunca te
  muestra la de seis meses después. Cuatro capítulos.
- **Vale**, compañera de trabajo que sabe de plata. Te explica la tasa real con una planilla
  de Excel, después se va a otra empresa por el doble, después te ofrece entrar donde está.
  Tres capítulos.
- **Bautista**, el que arranca cosas. Te pide prestado, después aparece con facturas y la
  conversación incómoda pendiente, después te ofrece entrar en su negocio. Tres capítulos.
- **Susana**, tu vieja. El primer sueldo, el mes que no le cierra, y cuando internan a tu
  viejo.

Las continuaciones esperan al menos año y medio, para que se sientan años y no escenas
seguidas. Medido sobre 600 partidas: se ven en promedio 3,13 de los 4 capítulos de Pedro,
2,4 de los 3 de Vale y 2,5 de los 3 de Bautista.

## La revisión anual muestra qué rindió cada cosa

Al lado de cada instrumento se ve cuánto rindió en los últimos doce meses **descontada la
inflación**. Es el único número que importa y es el que casi nadie mira: un plazo fijo al
4% mensual con inflación del 5% te está haciendo perder, aunque el saldo de la cuenta suba.

Medido sobre 300 partidas, rendimiento real anual:

| | p10 | mediana | p90 | años que le ganan a la inflación |
|---|---|---|---|---|
| Pesos quietos | −36% | −26% | −11% | 0% |
| Plazo fijo | −3% | +1% | +3% | 68% |
| Dólares | −13% | −1% | +15% | 45% |
| Bono del país | −24% | +9% | +50% | 65% |
| Índice global | −16% | +10% | +32% | 73% |

## El pronóstico

Cada revisión anual cierra pidiéndote que arriesgues **qué va a rendir más el año que viene**.
No cambia nada de tu plata. Doce meses después, arriba de la revisión siguiente, aparece el
veredicto: a qué le apostaste, qué ganó en realidad, y cuántos llevás acertados.

Al final de la década ves el registro completo. Lo normal es terminar cerca de lo que daría
tirar una moneda, y descubrirlo con **tu propia lista de errores** enseña que no se puede
predecir de una forma que ningún cartel de texto va a lograr.

Es además la única interacción del juego con una forma distinta: el 92% de las pantallas son
una escena o su consecuencia, y esto rompe esa monotonía una vez por año.

## Con qué terminás

Además del epílogo, el final te da un **arquetipo**: el título con el que te quedás cuando
alguien te pregunta cómo te fue. Hay veinte y se evalúan del más específico al más genérico.

> **El millonario infeliz** — Juntó como nadie y no se acuerda de un solo domingo.
>
> **El que vivió** — No juntó casi nada y tiene las mejores anécdotas de la mesa.
>
> **El colchón abajo del colchón** — Terminó con todo en pesos en la caja de ahorro. Todo.
>
> **La tortuga** — Nada brillante, nada estúpido, diez años seguidos. Es más difícil de lo
> que parece.

Debajo hay un botón que copia la línea para mandarla: *"Mateo, 32 años · El millonario
infeliz — 21 meses de aire, 15 de 26 ideas, 3 de 9 pronósticos."* Eso es lo que hace que
alguien pase el juego a un amigo.

## La colección

Los conceptos y logros **no se reinician** al empezar otra vida: se acumulan en el
navegador. Al final de cada partida ves cuántos llevás de todos, cuáles fueron novedad
esta vez, y cuál fue tu mejor aire histórico.

Ahí está la razón concreta para volver a jugar. Una partida típica desbloquea entre 14 y
20 de los 26 conceptos; llegar a los 26 lleva tres o cuatro vidas, porque los que faltan
solo aparecen si tomás decisiones que todavía no tomaste.

## El gráfico

La pantalla final abre con tu patrimonio mes a mes **en pesos constantes**, descontada la
inflación. Es deliberado: en pesos corrientes cualquier curva sube y el gráfico mentiría.
Ésta muestra si de verdad avanzaste. Se puede recorrer con el dedo para ver qué tenías en
cualquier mes de la década.

## Por qué es difícil

El gasto persigue al sueldo **hacia arriba y no baja solo**. Cada aumento se convierte en más
nivel de vida en un par de años sin que lo decidas: cambiás el celular, salís más, dejás de
mirar algunos precios. Es la razón real por la que el que gana el triple que hace diez años
sigue llegando justo, y sin eso el juego era demasiado fácil.

Tiene una defensa, y es una decisión explícita: cuando llega un aumento grande podés elegir
mantener el nivel de vida que tenías. Es lo más difícil de la lista y lo que más plata deja.
Nadie te felicita por eso y no se puede contar en ningún asado — la única prueba de que
funcionó aparece cinco años después.

Y **tener plata no te hace feliz**. Durante un tiempo el ánimo subía solo cuando el aire
era alto, y eso rompía la regla principal del juego: acumular salía gratis y no gastar nunca
era la jugada óptima. Ahora el saldo de la cuenta solo evita que la falta de plata te
destruya; lo único que levanta el ánimo son las decisiones — viajar, la gente, la terapia,
moverse. Guardar todo diez años y no vivir nada termina en quiebre.

Probado con bots que prueban cada opción y se quedan con la mejor, con dos criterios
distintos, contra uno que elige al azar:

| | al azar | equilibrado | ahorrador |
|---|---|---|---|
| Meses de aire (mediana) | 5,1 | 9,7 | **26,0** |
| Llegaste con aire | 0% | 13% | 3% |
| Con plata y cansado | 1% | 11% | **53%** |
| Quiebre o tocar fondo | 52% | 8% | 13% |

Lo importante es la última columna: **el que optimiza solo la plata termina rico y roto casi
la mitad de las veces.** Ninguna estrategia miope llega al mejor final, y esa es exactamente
la lección.

Hay una salida, y ninguno de los dos bots la encuentra porque hace falta entender el
sistema: la terapia, la pareja y entrenar suman +0,90 de ánimo por mes contra una caída
base de −0,22. El que descubre eso puede ahorrar y llegar entero a la vez.

Además de la inflación de estilo de vida, tres cosas más lo hacen difícil:

- **Los márgenes son chicos.** Se ahorra entre el 13% y el 25% del sueldo según dónde vivas,
  y la suma de todos los golpes de la década se come buena parte de eso.
- **Una emergencia cuesta cuatro meses de gastos.** A tu viejo lo internan y hay que operar:
  con colchón es un año malo, sin colchón es el principio de una espiral. Es la escena que
  justifica todo lo demás.
- **Vivir en casa de los viejos no es gratis para siempre.** A los veinticinco hay que
  decidir, y ahí aparece el alquiler que nunca pagaste. Antes ese origen ahorraba el 28% y
  la escena del aumento de alquiler estaba bloqueada para él: llegaba al año diez sin haber
  pagado un peso de techo, acumulaba 4,7 meses de aire por año y al segundo año el juego ya
  estaba ganado.
- **Uno de cada cuatro despidos no trae indemnización.** En negro, monotributo, o la empresa
  que "va a arreglar" y no arregla.

## Formas de perder

La década puede cortarse antes de los diez años, y no como castigo por jugar mal:

- **Quiebre.** Si el ánimo queda en el piso medio año seguido. Siempre avisa antes con
  escenas de bajón que ofrecen una salida — cara, pero salida.
- **Tocar fondo.** Sin trabajo, sin crédito y sin colchón para bancar la espera.
- **Insolvencia.** Cuando lo que debés, contando cuotas, supera lo que podés pagar.

Sobre 300 partidas jugadas al azar, el 49% llega a los diez años, 46% termina en quiebre y
5% tocando fondo. Decidiendo con la cabeza el quiebre baja al 8-13%, que es lo que tiene
que pasar: el juego es duro con el que no mira, no con el que sí.

## Estado

Prototipo, 69 escenas. La pregunta que tiene que contestar es una sola: **¿dan ganas de
jugar otra partida?** Si la respuesta es no, nada del resto importa.

La consecuencia de lo que elegís aparece **debajo de la opción, en la misma pantalla**, en
vez de reemplazarla. Así quedan juntos el cierre del mes, la escena, tu decisión y lo que
pasó — que es como se lee una historia y no una sucesión de tarjetas sueltas. Eso bajó los
redibujados de pantalla de 128 por partida a 53 (los toques son los mismos: elegir y
seguir).

Falta: el juego te sigue pidiendo casi siempre lo mismo — leer y elegir una opción. El
pronóstico anual es la única interacción con otra forma. Y no hay sonido.

---

Los precios, sueldos e inflación son inventados pero verosímiles. No es un pronóstico y
nada de acá es asesoramiento financiero.
