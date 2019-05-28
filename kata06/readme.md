YSLAS, GONZALO EZEQUIEL	gonzaloyslas@gmail.com	gyslas	
TAMBORINI CRISCUELI, AGUSTÍN ARIEL	atamborinicriscueli@est.frba.utn.edu.ar	TamboriniAgustin	x

**Nota 2**

**Función 1:** Todo ok
```Haskell
realizarHobbies :: Persona -> Persona
realizarHobbies persona = foldl (\hobbie persona -> persona hobbie) persona (hobbies persona)
```

**Funcion 2:** se llega a aplicar las funciones lamdas y de hecho diaDeDiversion llega a su cometido.

Sin embargo, notarán que se realizan dos recorridos de listas: 1ro con el filter, 2do con el foldl
```Haskell
aumentaMasDe5 :: Persona->PasaTiempo->Bool
aumentaMasDe5 persona hobbie = ((gradoDeDiversion . hobbie) persona - gradoDeDiversion persona) >= 5

diaDeDiversion :: Persona -> Persona
diaDeDiversion persona = (foldl (\hobbie persona -> persona hobbie) persona . filter (\hobbie -> aumentaMasDe5 persona hobbie)) (hobbies persona)
```
Esto se podría haber evitado si filtrabamos en la función lamda, por ej de la siguiente manera
```Haskell
diaDeDiversion :: Persona -> Persona
diaDeDiversion persona = foldl (\persona1 hobby-> if aumentaMasDe5 persona hobby then hobby persona1 else persona1) persona (hobbies persona)
```
Si, sabemos que es raro ver un if en funcional. Pero este es un caso donde aplica. 
Dentro del modulo de funciones lamdas pueden encontrar otro ejemplo

**Funcion 3:** de manera parecida a la función dos, se llega a aplicar las funciones lamdas pero tenemos dos recorridos a una lista cuando se podría haber realizado en uno solo
```Haskell
maximaDiversion :: Persona -> Int
maximaDiversion persona = (foldl1 max . map (\hobbie -> gradoDeDiversion $ hobbie persona)) (hobbies persona) 
```
Por ejemplo de la siguiente manera:
```Haskell
maximaDiversion persona = foldr (\hobby maximo -> max ((gradoDeDiversion . hobby) persona) maximo) 0 (hobbies persona)
```
---

DI SANTO, FACUNDO SEBASTIAN	fadisanto@gmail.com	fadisanto	x
GARBINI, SANTIAGO	santiago.garbini1@gmail.com	Elgarbo
**Nota: 1,5**

**Función 1:** Todo ok
```Haskell
realizarHobbies :: Persona -> Persona
realizarHobbies persona = foldl (\hobbie persona -> persona hobbie) persona (hobbies persona)
```

**Funcion 2:** se llega a aplicar las funciones lamdas y de hecho diaDeDiversion llega a su cometido.

Sin embargo, notarán que se realizan dos recorridos de listas: 1ro con el filter de gradoDeDiversion, 2do con el foldl
```Haskell
diaDeDiversion :: Persona -> Persona
diaDeDiversion persona = foldl (\persona hobby -> hobby persona) persona (gradoDeDiversionMayorA5 persona)

gradoDeDiversionMayorA5 :: Persona -> [PasaTiempo]
gradoDeDiversionMayorA5 persona = filter (tieneMasDe5Diversion persona) (hobbies persona)

tieneMasDe5Diversion :: Persona -> PasaTiempo -> Bool 
tieneMasDe5Diversion persona hobby = gradoDeDiversion (hobby persona) - gradoDeDiversion persona > 5
```
Esto se podría haber evitado si filtrabamos en la función lamda, por ej de la siguiente manera
```Haskell
diaDeDiversion :: Persona -> Persona
diaDeDiversion persona = foldl (\persona1 hobby-> if tieneMasDe5Diversion persona hobby then hobby persona1 else persona1) persona (hobbies persona)
```
Si, sabemos que es raro ver un if en funcional. Pero este es un caso donde aplica. 
Dentro del modulo de funciones lamdas pueden encontrar otro ejemplo

**Funcion 3:** No se si por falta de tiempo o porque se les complicó, no llegaron a dar este punto. Esta es una posible solución
```Haskell
maximaDiversion persona = foldr (\hobby maximo -> max ((gradoDeDiversion . hobby) persona) maximo) 0 (hobbies persona)
```

---

CUESTA, MARTIN NICOLAS	cuesta.martin.n@hotmail.com	maartincm	x
WILLIMAN, NICOLÁS	williman.nicolas@gmail.com	nicolaswilliman
**Nota: 2**

**Función 1:** Todo ok
```Haskell
realizarHobbies :: Persona -> Persona
realizarHobbies persona = foldr (\hobbie persona' -> hobbie persona') persona (hobbies persona)
```

**Funcion 2:** muy bien utilizada la función lamda. Capaz quedó un poco confuso el significado de "diversionAplicadaPorEsMayorA".
Un "generaDiversionMayorA" resultaría más entendible.
```Haskell
diaDeDiversion :: Persona -> Persona
diaDeDiversion persona = foldr (\hobbie persona' -> if diversionAplicadaPorEsMayorA 5 hobbie persona' then hobbie persona' else persona') persona (hobbies persona)

diversionAplicadaPor :: PasaTiempo -> Persona -> Int
diversionAplicadaPor hobbie persona = (gradoDeDiversion.hobbie) persona - gradoDeDiversion persona

diversionAplicadaPorEsMayorA :: Int -> PasaTiempo -> Persona -> Bool
diversionAplicadaPorEsMayorA numero hobbie = (>= numero).diversionAplicadaPor hobbie
```

**Funcion 3:** Acá no llegaron a evitar recorrer dos listas. Piensen que el map recorre una lista generando una nueva, que se la pasa a maximum quien la recorre y se queda el más alto.
```Haskell
maximaDiversion :: Persona -> Int
maximaDiversion persona = (foldl1 max . map (\hobbie -> gradoDeDiversion $ hobbie persona)) (hobbies persona) 
```
Una manera de hacer todo esto de una podría ser la siguiente:
```Haskell
maximaDiversion persona = foldr (\hobby maximo -> max ((gradoDeDiversion . hobby) persona) maximo) 0 (hobbies persona)
```
---
