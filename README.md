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

Al final, el juego compara **tu mismo flujo de plata** contra cuatro estrategias mecánicas
—todo en pesos, todo a plazo fijo, todo a dólares, todo al índice global— sobre el
escenario exacto que te tocó. Ahí está el aprendizaje, más que en la partida.

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

Mover plata paga comisión (0,8% por operación, más el spread del dólar), así que
rebalancear por rebalancear cuesta — y eso también es parte de la lección.

## Conceptos y logros

No hay tutorial ni glosario para leer al principio. Cada uno de los **22 conceptos** se
desbloquea el mes exacto en que te pasa, y recién ahí se te nombra lo que acabás de vivir:
la licuación aparece cuando cerrás una paritaria por debajo de la inflación, la tasa real
el mes que tu plazo fijo rinde menos que los precios, el riesgo de contraparte cuando le
prestás a un amigo.

Al final ves cuáles te faltan. No están escondidos: aparecen si tomás otras decisiones.
Ahí está el motivo para jugar de nuevo.

Los **10 logros** están puestos en lo difícil de sostener diez años: no deber nunca, pasar
una crisis sin endeudarte, no vender los dólares en el pico, terminar con el ánimo alto.

## La gente que vuelve

Antes cada escena traía "un amigo" distinto y las repeticiones se sentían repeticiones.
Ahora vuelven cuatro personas con nombre y arco propio a lo largo de la década:

- **Nacho**, el que siempre tiene el dato. Eufórico con la pantalla en verde, después deja
  el laburo para operar, después se funde — o la pega, una de cada cinco veces. Su historia
  avanza sola, la acompañes o no: la lección es que el que te muestra la captura nunca te
  muestra la de seis meses después. Cuatro capítulos.
- **Vale**, compañera de trabajo que sabe de plata. Te explica la tasa real con una planilla
  de Excel, después se va a otra empresa por el doble, después te ofrece entrar donde está.
  Tres capítulos.
- **Fede**, el que arranca cosas. Te pide prestado, después aparece con facturas y la
  conversación incómoda pendiente, después te ofrece entrar en su negocio. Tres capítulos.
- **Susana**, tu vieja. El primer sueldo, el mes que no le cierra, y cuando internan a tu
  viejo.

Las continuaciones esperan al menos año y medio, para que se sientan años y no escenas
seguidas. Medido sobre 600 partidas: se ven en promedio 3,13 de los 4 capítulos de Nacho,
2,4 de los 3 de Vale y 2,5 de los 3 de Fede.

## La colección

Los conceptos y logros **no se reinician** al empezar otra vida: se acumulan en el
navegador. Al final de cada partida ves cuántos llevás de todos, cuáles fueron novedad
esta vez, y cuál fue tu mejor aire histórico.

Ahí está la razón concreta para volver a jugar. Una partida típica desbloquea entre 14 y
18 de los 22 conceptos; llegar a los 22 lleva tres o cuatro vidas, porque los que faltan
solo aparecen si tomás decisiones que todavía no tomaste.

## El gráfico

La pantalla final abre con tu patrimonio mes a mes **en pesos constantes**, descontada la
inflación. Es deliberado: en pesos corrientes cualquier curva sube y el gráfico mentiría.
Ésta muestra si de verdad avanzaste. Se puede recorrer con el dedo para ver qué tenías en
cualquier mes de la década.

## Formas de perder

La década puede cortarse antes de los diez años, y no como castigo por jugar mal:

- **Quiebre.** Si el ánimo queda en el piso medio año seguido. Siempre avisa antes con
  escenas de bajón que ofrecen una salida — cara, pero salida.
- **Tocar fondo.** Sin trabajo, sin crédito y sin colchón para bancar la espera.
- **Insolvencia.** Cuando lo que debés, contando cuotas, supera lo que podés pagar.

Sobre 700 partidas jugadas al azar, el 71% llega a los diez años, 19% termina en quiebre y
9% tocando fondo. Jugando con la cabeza esos números bajan bastante.

## Estado

Prototipo, 49 escenas. La pregunta que tiene que contestar es una sola: **¿dan ganas de
jugar otra partida?** Si la respuesta es no, nada del resto importa.

Falta: la revisión anual todavía no te muestra qué hizo cada instrumento en los últimos
doce meses —que es justo el dato que necesitás para decidir bien—, las escenas de pareja e
hijos son más flacas que las de plata, y no hay sonido.

---

Los precios, sueldos e inflación son inventados pero verosímiles. No es un pronóstico y
nada de acá es asesoramiento financiero.
