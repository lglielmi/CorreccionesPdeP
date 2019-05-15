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

**Nota: 1.5**

palabrasReservadas OK

esPalabraReservada & esCaracterValido: acá hubo una pequeña mezcla que hizo que en su conjunto funcione bien para lo que era el ejercicio
pero ninguna de las dos realiza lo que dice realizar. Vamos de a una:
```Haskell
esCaracterValido:: Caracter -> Bool
esCaracterValido caracter = elem caracter especiales
```
Al hacer esto, nos devolverá true cuando el caracter pertenezca a la lista especiales, y false cuando no. Es decir que para este caso nos va a estar devolviendo true para #$%&/()!_*, que son justamente los caracteres invalidos.
Entonces la función implementada es más bien un esCaracterEspecial.

Una manera correcta de implementarla habría sido
```Haskell
esCaracterValido:: Caracter -> Bool
esCaracterValido caracter = (not.elem caracter) especiales
```
O si quiero usar point free
```Haskell
esCaracterValido:: Caracter -> Bool
esCaracterValido = not.flip elem especiales
```
Luego, una palabra es reservada cuando todos sus caracteres son válidos.
```Haskell
esPalabraReservada:: Palabra -> Bool
esPalabraReservada  = not.(any esCaracterValido)
```
Sin embargo lo que acá hicieron es equivalente a "una palabra es reservada si no tiene algún caracter valido". Y como justo su implementación de esCaracterValido era más bien un esCaracterEspecial, nos termino quedando algo equivalente a "una palabra es reservada si no tiene algún caracter especial", lo cual es cierto, pero no es lo que expresa la función en cuanto a su declaratividad.
Tomando en cuenta la implementación de esCaracterValido que nosotros les indicamos, una implementación posible será:
```Haskell
esPalabraReservada:: Palabra -> Bool
esPalabraReservada  = all esCaracterValido
```



