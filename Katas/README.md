# Correcciones de Katas
## OLIVERA, CRISTIAN NICOLAS
K2052 olivera.cristian93@gmail.com	elcri93

### [Kata00](https://github.com/pdep-utn/kata-0-primera-funcion-elcri93) 

El badge a CircleCI no fue generado correctamente. Actualmente se ve así:

[![CircleCI](https://circleci.com/gh/pdep-utn/kata-0-primera-funcion-elcri93.svg?style=svg)](https://circleci.com/gh/pdep-utn/kata-0-primera-funcion-elcri93)

Esto se debe a que no creaste el Token.
El procedimiento para generarlo es el siguiente:

![](Videos/circleCIstatusBadge.gif)

En cuanto a la función, 
``` Haskell
f x | x < 0 = 2* x + 3
    | (x >= 0 && x <= 5) = x - 1
    | otherwise =  x
```
está perfecta.



### [Kata01](https://github.com/pdep-utn/kata-1-guardas-elcri93) **NOTA: 1**

Mismo problema con el Badge de CircleCI. Ver correción de Kata 00.
Pero acá hay un problema más: los test fallán al ejecutarlo. Poder verificarlo en [el log de CircleCI](https://circleci.com/gh/pdep-utn/kata-1-guardas-elcri93/2).

La parte buena es que no se debió a como codeaste la función, sino por un problema en el archivo de test por nuestra parte.
Varios de tus compañeros nos informaron del error al grupo de la clase, y les indicamos como corregirlo.
Sabemos que fue una semana complicada donde se enviaron muchisimos mails, pero es importante que intentes verlos porque seguramente habrá información que te va a ser de utilidad.

En cuanto a la solución, hay un par de aclaraciones a realizar:
Estrictamente en cuanto a lo que la solución compete, cumple con su objetivo.
```Haskell
calcuLoco :: Integer -> Integer -> Integer
calcuLoco primerNumero segundoNumero | primerNumero > segundoNumero = primerNumero * segundoNumero
                                     | mod primerNumero 2 == 0 = segundoNumero * 3
                                     | otherwise = primerNumero - segundoNumero
```
Sin embargo, te queremos mencionar dos puntos:
- Función Even: 
  La función Even, ya proporcionada por Haskell, recibe un número y retorna True si es par, False si es impar.
  Dentro de la siguiente [Guía](https://docs.google.com/document/d/1oJ-tyQJoBtJh0kFcsV9wSUpgpopjGtoyhJdPUdjFIJQ/edit) podrás encontrar más funciones que te van a facilitar las resoluciones

```Haskell
calcuLoco :: Integer -> Integer -> Integer
calcuLoco primerNumero segundoNumero | primerNumero > segundoNumero = primerNumero * segundoNumero
                                     | even primerNumero = segundoNumero * 3
                                     | otherwise = primerNumero - segundoNumero
```

- Expresividad:
  Supongamos que la función Even no existiera. La manera en que resolviste la segunda condicion es correcta. Ahora bien, me queda claro cual es esa condición al leer el código? Con un poquito de razonamiento, seguro que si, pero en el paradigma funcional (y a lo largo de toda la meteria) te vamos a estar pidiendo que delegues estas partes "locas" con el objetivo de que el código quede más claro. ¿Y cómo sería esto?

```Haskell
calcuLoco :: Integer -> Integer -> Integer
calcuLoco primerNumero segundoNumero | primerNumero > segundoNumero = primerNumero * segundoNumero
                                     | esPar primerNumero = segundoNumero * 3
                                     | otherwise = primerNumero - segundoNumero

esPar :: Integer -> Bool
esPar unNumero = mod unNumero 2 == 0
```

## CAPURRO, ROMÁN FEDERICO
K2052 romi_fede_07@hotmail.com	roma1417

### [Kata00](https://github.com/pdep-utn/kata-0-primera-funcion-Roma1417)
Función Ok,
Circle CI Ok.

```Haskell
f :: Integer -> Integer
f x | x > 5 = x
 | x < 0 = 2 * x + 3
 | otherwise = x - 1
 ```

Bienvenido a la materia :)

### [Kata01](https://github.com/pdep-utn/kata-1-guardas-Roma1417) **NOTA:2** 

La función cumple con el requerimiento
```Haskell
calcuLoco :: Integer -> Integer -> Integer
calcuLoco x y | x > y = x * y
 |rem x 2 == 0 = y * 3
 |otherwise = x - y
 ```
Sin embargo, te queremos mencionar dos puntos:
- Función Even: 
  La función Even, ya proporcionada por Haskell, recibe un número y retorna True si es par, False si es impar.
  Dentro de la siguiente [Guía](https://docs.google.com/document/d/1oJ-tyQJoBtJh0kFcsV9wSUpgpopjGtoyhJdPUdjFIJQ/edit) podrás encontrar más funciones que te van a facilitar las resoluciones

```Haskell
calcuLoco :: Integer -> Integer -> Integer
calcuLoco x y | x > y = x * y
              | even x = y * 3
              | otherwise = x - y
```

- Expresividad:
  Supongamos que la función Even no existiera. La manera en que resolviste la segunda condicion es correcta. Ahora bien, me queda claro cual es esa condición al leer el código? Con un poquito de razonamiento, seguro que si, pero en el paradigma funcional (y a lo largo de toda la meteria) te vamos a estar pidiendo que delegues estas partes "locas" con el objetivo de que el código quede más claro. ¿Y cómo sería esto?

```Haskell
calcuLoco :: Integer -> Integer -> Integer
calcuLoco x y | x > y = x * y
              | esPar x = y * 3
              | otherwise = x - y
```

Y por ultimo una pequeña aclaración más, que entendemos que lo tuviste en cuenta pero no está de más mencionarlo:
Llamar a las variables X e Y aplican correctamente para este estilo de problemas matemáticos, dado que estamos representando funciones. Pero es importante que esto este claro y cuando pasemos a otro estilos de problemas, continuemos buscando nombres que nos expresen lo que está modelando y representando.

## CASTRO, EMILIANO MATIAS
K2152 emilianocast98@gmail.com	ecastro98


### [Kata00](https://github.com/pdep-utn/kata-0-primera-funcion-ecastro98)

Función Ok,
Circle CI Ok.

```Haskell
f :: Integer -> Integer
f x | x > 5     = x
    | x < 0     = 2 * x + 3
    | otherwise = x - 1
 ```

Bienvenido a la materia :)

### [Kata01](https://github.com/pdep-utn/kata-1-guardas-ecastro98) **NOTA:2** 

La función cumple con el requerimiento. Muy bien utilizada la delegación sobre esPar.

```Haskell
esPar :: Integer -> Bool
esPar numero = numero `mod` 2 == 0

calcuLoco :: Integer -> Integer -> Integer
calcuLoco x y | x > y = x * y
              | esPar x = y * 3
              | otherwise = x - y
```

Sin embargo, te queremos mencionar la existencia de la función Even: ya proporcionada por Haskell, recibe un número y retorna True si es par, False si es impar.
Dentro de la siguiente [Guía](https://docs.google.com/document/d/1oJ-tyQJoBtJh0kFcsV9wSUpgpopjGtoyhJdPUdjFIJQ/edit) podrás encontrar más funciones que te van a facilitar las resoluciones

Y por ultimo una pequeña aclaración más, que entendemos que lo tuviste en cuenta pero no está de más mencionarlo:
Llamar a las variables X e Y aplican correctamente para este estilo de problemas matemáticos, dado que estamos representando funciones. Pero es importante que esto este claro y cuando pasemos a otro estilos de problemas, continuemos buscando nombres que nos expresen lo que está modelando y representando.


## GUGINO, AGUSTIN EZEQUIEL & LUNA, LUCAS MARTIN
### [Kata00](https://github.com/pdep-utn/kata-0-primera-funcion-agustingugino)

Función Ok,
Circle CI Ok.

```Haskell
f :: Integer -> Integer
f x | x > 5     = x 
    | x < 0     = 2 * x + 3
    | otherwise = x - 1
 ```

Bienvenidos a la materia :)

[Kata00Bis](https://github.com/pdep-utn/kata-0-primera-funcion-lucasluna068)
Repositorio duplicado. Ver https://github.com/pdep-utn/kata-0-primera-funcion-agustingugino.

### [Kata01](https://github.com/pdep-utn/kata-1-guardas-agustingugino) **NOTA: 2**
La función cumple con el requerimiento. Muy bien utilizada la delegación sobre even.
La unica aclaración es que los parentesis rodeando a even no son necesarios.
```Haskell
calcuLoco :: Integer -> Integer -> Integer
calcuLoco primero segundo   | primero > segundo = primero * segundo
                            | (even) primero   = segundo * 3
                            | otherwise         = primero - segundo 
```
Los parentesis son necesarios cuando necesitas especificarle a haskell el orden de evaluación, dado que su prescedencia estandar no es la que queres utilizar. Por ejemplo:

La siguiente función no va a compilar:
```Haskell
cantLetrasImpar :: String -> Bool
cantLetrasImpar palabra = not.even.length palabra
```
Esto debido a que Haskell tomará el siguiente orden de evaluación, que confundirá totalmente al compilador:
Primero resuelve a length palabra y lo intenta componer
```Haskell
not.even.(length palabra)
```
Entonces ahora si, necesitamos ingresar los partentesis que engloben a la composición
```Haskell
cantLetrasImpar palabra = (not.even.length) palabra
```

## LOPEZ, YAMIL ALEJANDRO
### [Kata00](https://github.com/pdep-utn/kata-0-primera-funcion-Yamil2017)

Función OK.
CircleCI OK.

```Haskell
f :: Integer -> Integer
f x |x>5=x
    |0<=x && x<=5 = x-1
    |x<0 = 2*x + 3 
```
Solo una aclaracion: para este caso donde podes cubrir todo el dominio que puede recibir un Integer, no hay problema si no utilizas el otherwise. Pero tene en cuenta que en otros casos este puede ser fundamental, ya que si la función no encuentra una guarda que la acepte, tendrás un error en tiempo de ejecución.

### [Kata01](https://github.com/pdep-utn/kata-1-guardas-Yamil2017) **NOTA: 2**
La función cumple con el requerimiento:
```Haskell
calcuLoco :: Integer -> Integer -> Integer
calcuLoco numero1 numero2  |numero1 > numero2 = numero1*numero2
                           |(mod numero1 2)==0 = numero2*3
                           |otherwise = (numero1-numero2)
```
Sin embargo, te queremos mencionar dos puntos:
- Función Even: 
  La función Even, ya proporcionada por Haskell, recibe un número y retorna True si es par, False si es impar.
  Dentro de la siguiente [Guía](https://docs.google.com/document/d/1oJ-tyQJoBtJh0kFcsV9wSUpgpopjGtoyhJdPUdjFIJQ/edit) podrás encontrar más funciones que te van a facilitar las resoluciones

```Haskell
calcuLoco :: Integer -> Integer -> Integer
calcuLoco numero1 numero2 | numero1 > numero2 = numero1 * numero2
              | even numero1 = numero2 * 3
              | otherwise = numero1 - numero2
```

- Expresividad:
  Supongamos que la función Even no existiera. La manera en que resolviste la segunda condicion es correcta. Ahora bien, me queda claro cual es esa condición al leer el código? Con un poquito de razonamiento, seguro que si, pero en el paradigma funcional (y a lo largo de toda la meteria) te vamos a estar pidiendo que delegues estas partes "locas" con el objetivo de que el código quede más claro. ¿Y cómo sería esto?

```Haskell
calcuLoco :: Integer -> Integer -> Integer
calcuLoco numero1 numero2 | numero1 > numero2 = numero1 * numero2
              | esPar numero1 = numero2 * 3
              | otherwise = numero1 - numero2
```
