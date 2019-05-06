# ALUMNOS
- DI SANTO, FACUNDO SEBASTIAN	fadisanto@gmail.com @fadisanto
- LOPEZ, YAMIL ALEJANDRO	pechyar@hotmail.com @Yamil2017

https://github.com/pdep-utn/fun-kata-04-destinos-fadisanto

**NOTA: 2**

**Función esBarato: Todo OK**

**Función tieneAlMenosTresPuntos: Todo OK**

**Función bienDefinido**

Cuidado que dentro de la subfunción que crearon `estaOrdenado`, no contemplaron el caso donde la lista de puntos de interés estuviera vacía. No había un caso asi en el spec y por lo tanto los tests no fallan, así que quizás no fuese una necesidad de negocio pero de existir, lanzaría un error de Pattern Matching incompleto

```Haskell
estaOrdenado :: [PuntoDeInteres] -> Bool
--Faltaría además acá un
--estaOrdenado [] = True
estaOrdenado [primerPunto] = True
estaOrdenado (primerPunto:siguientePunto:puntosRestantes) =   diferenciaDeUno (primerPunto) (siguientePunto) && estaOrdenado (siguientePunto:puntosRestantes)   
```
Además, en la función `diferenciaDeUno` usar snd no está mal en una tupla, pero se pierde un poco de expresividad que estaría bueno mantener creando una función para el negocio actual
```Haskell
diferenciaDeUno primerPunto siguientePunto = snd(siguientePunto) - snd (primerPunto) == 1

--Podría crearse una función más descriptiva
estrellas :: PuntoDeInteres -> Estrellas
estrellas = snd

--Y quedaría así que es un poco más fácil de entender a simple vista
estrellas siguientePunto - estrellas primerPunto == 1
```

Más allá de estos detalles, la recursividad esta usada diez puntos así que está aprobada la kata.

---

# ALUMNOS
- BANDEO, MARCOS LUIS	mlbandeo@gmail.com @DevInABottle
- OLIVERA, CRISTIAN NICOLAS	olivera.cristian93@gmail.com @elcri93

https://github.com/pdep-utn/fun-kata-04-destinos-DevInABottle

**NOTA: 2**

Antes que nada, no me quedó claro por qué definieron un `sanFrancisco` suelto, imagino que para guiarse pero ojo con eso porque no está bueno committear código extra que no sirve algún propósito, puede traer problemas sin querer.


**Función esBarato: Todo OK**

Queda un poco confuso tener una función `barato` y otra `esBarato`, pero es muy buena la idea de separar la noción del número 22000 a un lugar propio, porque esas cosas son las mas propensas a cambiar en sistemas reales - aunque me hubiera gustado más separar el número nada más en lugar de la función. De todos modos, muy copada la idea.
```Haskell
precioLímiteParaDestinosBaratos = 22000
esBarato =(< precioLímiteParaDestinosBaratos) . valor
```

**Función tieneAlMenosTresPuntos: Todo OK**

**Función bienDefinido**

Al hacer pattern matching de listas con 2+ elementos, no son necesarios los paréntesis internos.

```Haskell
destinosOrdenados (primerPunto:(segundoPunto:otrosPuntos)) = ...

-- Queda mejor así
destinosOrdenados (primerPunto:segundoPunto:otrosPuntos) = ...
```

Luego, metieron una redundancia que complicó un montón el código al querer meter guardas. Así como regla a ojo, en cualquier lenguaje, si están trabajando con operaciones booleanas, eviten meter además `True` o `False` porque suelen ser redundantes.

Además el checkeo de si un punto tiene 1 sola estrella más que otro era una responsabilidad puntual que podría extraerse a otra función para dejar el código aún más limpio. 

Ya en estos ejercicios puede notarse como descuidarse con estos detalles termina en que idea simple como "que estén ordenados y vayan de a uno" se estire en una línea de más de 200 caracteres (es una banda!). Siempre es mejor tratar de seguir la ley del menor esfuerzo y apuntar a que sea fácil leer una línea en complejidad y longitud, y particularmente en longitud horizontal, porque es más natural scrollear verticalmente.

```Haskell
destinosOrdenados (primerPunto:segundoPunto:otrosPuntos) | ((+1).cantidadEstrellas) primerPunto == cantidadEstrellas segundoPunto = True && destinosOrdenados (segundoPunto:otrosPuntos)
| otherwise = False

--Simplificando los booleanos redundantes queda
destinosOrdenados (primerPunto:segundoPunto:otrosPuntos) = ((+1).cantidadEstrellas) primerPunto == cantidadEstrellas segundoPunto && destinosOrdenados (segundoPunto:otrosPuntos)

--Simplificando la comparación además queda
esMayorPorUno primerPunto segundoPunto = ((+1).cantidadEstrellas) primerPunto == cantidadEstrellas segundoPunto

destinosOrdenados (primerPunto:segundoPunto:otrosPuntos) = esMayorPorUno primerPunto segundoPunto && destinosOrdenados (segundoPunto:otrosPuntos)
```

Dicho esto, renombrar `snd` para que sea más expresiva con el enunciado fue una muy buena idea.

Más allá de estos detalles, la recursividad esta usada diez puntos así que está aprobada la kata.

---

# ALUMNOS
- ESPADA, SOFÍA	sofiaespada20@gmail.com @zaphry20100
- MALPICA TAMASHIRO, OSCAR ANDRÉ FERNANDO	andrefer2505@gmail.com @andrefer25

https://github.com/pdep-utn/fun-kata-04-destinos-Andrefer25

**NOTA:1.5

Antes que nada, quería comentar sobre decisión de mezclar idiomas en la misma base de código. Es algo super menor en este caso, pero en los trabajos de programación una buena idea en general es mantener las prácticas de estilo del código existente (en este caso, el código hecho en Paradigmas lo escribimos en castellano). Además, si pueden tomar la decisión ustedes y el código no va a ser usado por personas que hablen otros idiomas, siempre les recomiendo escribir su propio código o al menos su código de negocio en su lengua nativa por lo que les comento más abajo.

**Función esBarato: Todo OK**

**Función tieneAlMenosTresPuntos: Todo OK**

**Función bienDefinido**

Lo primero a notar acá es la función `sortByStars`. Al decidir codear en inglés es un compromiso que le agrega carga al pensar nombres (algo que es muy muy difícil de por sí aunque no parezca), y en este caso le quedó un nombre incorrecto que significa "ordenar por estrellas" y recibe una lista, lo cual al leer da a entender que retornará una nueva lista ordenada cuando en realidad su propósito es totalmente distinto. Un nombre correcto para casos booleanos en general debería empezar con `is`, en este caso `isSortedByStars`, y además aclarar que es de a uno - `isSortedByStarsIncrementallyByOne`. 

Luego, en este caso los tests no lo contemplaban, pero el pattern matching fallaría de existir un destino sin puntos de interés, así que cuidado con eso a futuro.

```Haskell
--Faltaría este caso
sortByStars [] = True
```

También quería hacerles notar que aunque se hubieran asegurado de que en `sortByStars(punto:puntos)`, la lista de cola `puntos` tendría siempre un elemento por tener pattern matching en `sortByStars [punto]` previamente, es peligroso porque la notación `(punto:puntos)` matchea con listas de un sólo elemento, con lo cual hacer `head puntos` lanzaría un error. 
Como está escrito en los apuntes, para asegurarse de que solo matchee con listas de 2 elementos, hay que utilizar la siguiente sintaxis: 
```Haskell
sortByStars (primerPunto:segundoPunto:otrosPuntos) = ((+1).stars) punto == stars segundoPunto && sortByStars (puntos)
```

Y como último para destacar, la responsabilidad de chequear que dos puntos de interes esten ordenados y su diferencia sea de uno, es una responsabilidad lo suficientemente puntual como para extraer a su propia función, quedando así:

```Haskell
esMayorPorUno primerPunto segundoPunto = ((+1).stars) primerPunto == stars segundoPunto

sortByStars (primerPunto:segundoPunto:otrosPuntos) = esMayorPorUno primerPunto segundoPunto && sortByStars (segundoPunto:otrosPuntos)
```
---
# ALUMNOS
- CRESPO, HERNÁN	h.crespo06@gmail.com	hcrespo06
- CASTRO, EMILIANO MATIAS	emilianocast98@gmail.com	ecastro98

https://github.com/pdep-utn/fun-kata-04-destinos-ecastro98

**Nota: 2**

**Función esBarato: Todo OK**

**Función tieneAlMenosTresPuntos: Todo OK**

**Función esOrdenado:**

La recursividad está perfecta. 
```Haskell
esOrdenado :: [PuntoDeInteres] -> Bool
esOrdenado [] = True 
esOrdenado (_:[]) = True
esOrdenado (x:y:xs) = ((estrellas x)+1 == estrellas y) && esOrdenado (y:xs)
```
Solo dos comentarios (calando muy ondo dado que toda la kata está muy bien resuelta)
- El pattern matching (x:y:ys) no resulta muy expresivo. Se puede utilizar (punto1 : punto2 : otrosPuntos), es decir, le pueden dar el nombre que les parezca más adecuado.
- La responsabilidad de chequear que dos puntos de interes esten ordenados y su diferencia sea de uno, es una responsabilidad lo suficientemente puntual como para extraer a su propia función
Se podría haber implementado la siguiente función:
```Haskell
esMayorPorUno punto1 punto2 = ((+1).estrellas) punto1 == estrellas punto2
esOrdenado (punto1:punto2:otrosPuntos) = esMayorPorUno punto1 punto2 && sortByStars (segundoPunto:otrosPuntos)
```
**Función bienDefinido: Todo OK**
