DI SANTO, FACUNDO SEBASTIAN	fadisanto@gmail.com	fadisanto		X

LANNERT, NICOLÁS	nicolas.lannert@gmail.com	nicolasLannert

**Nota: 2** 

palabrasReservadas OK (Aunque podrían haber usado point free)

esPalabraReservada OK (Aunque podrían haber usado point free)

esCaracterValido OK. 

calcularImpuestoGanancias OK. Perfecta la resolución pero queremos mencionarles que lo ideal no será usar a sum y map juntos.

¿Porque? Piensen que están tomando una lista, para transformarla en otra lista y despues reducirla a un valor. 
Es decir, estamos recorriendo dos veces una lista, cuando podríamos haberlo hecho una sola. 

¿Cómo?
En la ultima clase vimos el fold, que nos viene perfecto para resolver este punto. Una manera sería:
```Haskell
calcularImpuestoGanancias:: [Float] -> Float
calcularImpuestoGanancias sueldos = foldl ((+).calculoImpuesto) 0 sueldos 
```
o bien, considerando que sueldos nunca sea una lista vacia:
```Haskell
calcularImpuestoGanancias:: [Float] -> Float
calcularImpuestoGanancias sueldos = foldl1 ((+).calculoImpuesto) sueldos 
```
---
BANDEO, MARCOS LUIS	mlbandeo@gmail.com	DevInABottle			X

OLIVERA, CRISTIAN NICOLAS	olivera.cristian93@gmail.com	elcri93

**Nota: 2**

palabrasReservadas OK 

esPalabraReservada OK 

esCaracterValido OK (y muy bien asimilando rapido el uso del flip!)

calcularImpuestoGanancias OK. El objetivo de la kata era usar lo más posible el orden superior y lo usaron muy bien.
Ahora bien, yendo a la practica, no va a ser muy lindo encontrarse con un sum, map y filter en la misma función.

¿Porque? Piensen que están tomando una lista, para transformarla en una otra lista (más chica), para transformarla en otra lista (de otro tipo) 
y despues reducirla a un valor. Es decir, estamos recorriendo tres veces una lista, cuando podríamos haberlo hecho recorriendola solo una vez.

¿Cómo?
Primero tendríamos que modificar la forma en que se calcula el impuesto
```Haskell
calculoImpuesto :: Float -> Float
calculoImpuesto sueldo | sueldo > 1000 = aplicarAlicuota sueldo
                       | otherwise = 0

aplicarAlicuota :: Float -> Float
aplicarAlicuota sueldo = (sueldo - valorLimiteParaImpuesto) * 0.3
```
Luego, la ultima clase vimos el fold, que nos viene perfecto para resolver este punto. Una manera sería:
```Haskell
calcularImpuestoGanancias:: [Float] -> Float
calcularImpuestoGanancias sueldos = foldl ((+).calculoImpuesto) 0 sueldos 
```
o bien, considerando que sueldos nunca sea una lista vacia:
```Haskell
calcularImpuestoGanancias:: [Float] -> Float
calcularImpuestoGanancias sueldos = foldl1 ((+).calculoImpuesto) sueldos 
```
---

ALBOR, LUCAS EMANUEL	lucas.007.albor.e@gmail.com	Emanuelalbor		X

CALVO ROMERO, CRISTOPHER JOHN	ccalvoromero@gmail.com	ccalvoromero

*Pendiente*
