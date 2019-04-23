# Alumnos
- RAMÍREZ MOREALE, NICOLÁS PAUL	nicolaspaulmoreale@outlook.com	@nramrezmoreale
- ENRIQUEZ, SYLVINA	sylvina64@gmail.com	@sylvina64

**NOTA: 2**

Lamentablemente vemos que la solución no corrió bien por Travis.
[![Build Status](https://travis-ci.com/pdep-utn/kata-3-funcional-2019-modelado-hobbies-sylvina64.svg?token=r9NmZKuvxPp5obinxbZw&branch=master)](https://travis-ci.com/pdep-utn/kata-3-funcional-2019-modelado-hobbies-sylvina64)

Al compilar da el siguiente error, correspondiente a la función 2. 
```Haskell
/home/travis/build/pdep-utn/kata-3-funcional-2019-modelado-hobbies-sylvina64/src/Library.hs:46:57: error:
    • Estás usando una función como un número o un número como una función.
    • In the first argument of ‘(.)’, namely
        ‘(+ (videoJuegosAux nivel))’
      In the expression: (+ (videoJuegosAux nivel)) . gradoDeDiversion
      In the ‘gradoDeDiversion’ field of a record
   |
46 |                                   gradoDeDiversion =  ((+ (videoJuegosAux nivel)).gradoDeDiversion) persona,
   |                
```
Vamos por partes:
**Funcion 01: Todo OK**

**Función 02: No compila :(**
Bueno, para empezar tenemos el problema de que no compila por el error mencionado antes:
```Haskell
videoJuegos :: Int -> PasaTiempo
videoJuegosAux nivel persona = ((+ (calcularGrado nivel)).gradoDeDiversion) persona

calcularGrado nivel = min 8 (nivel `div` 2)

videoJuegos nivel persona = Persona{
                                  nombre = nombre persona,
                                  fechaDeNacimiento = fechaDeNacimiento persona,
                                  gradoDeDiversion =  ((+ (videoJuegosAux nivel)).gradoDeDiversion) persona,
                                  hobbies = hobbies persona
                                  }
```
Por un lado no se llega a comprender fácilmente cuál fue la intención de videoJuegosAux - esto es por falta de **expresividad**. 
Entiendo que intentaron calcular cuanto tiene que subir el Grado de Diversión, y despues sumarlo. 
De hecho, con calcularGrado lo lograban sin problemas (nota: vimos que Nicolas lo continuó por su cuenta y también se percato de ello, así que podemos mostrar directamente su solución, aunque esto no va a valer para la kata porque salió despues de hora):

```Haskell
videoJuegos :: Int -> PasaTiempo
videoJuegos nivel persona = persona { 
    gradoDeDiversion = ((+ (calcularGrado nivel)).gradoDeDiversion) persona
}
```
Además, en lugar de pasar cada uno de los componentes de persona nuevamente, solo pasó al que quiere modificar (utilizando el pattern matching del record syntax).

**Función 3: Todo OK**
```Haskell
jardineria :: String -> PasaTiempo

jardineriaAux tipo | tipo == "ornamental" = 10
                                 | tipo == "bonsai" = 20
                                 | otherwise = length tipo

jardineria tipo persona = Persona{
                                  nombre = nombre persona,
                                  fechaDeNacimiento = fechaDeNacimiento persona,
                                  gradoDeDiversion =  ((+ (jardineriaAux tipo)).gradoDeDiversion) persona,
                                  hobbies = hobbies persona
                                  }
```
Pero como aclaración va lo siguiente:
- Expresividad: jardineriaAux no me dice mucho que es lo que va a hacer. Podría llamarse diversionDeJardineria, gradoDeJardineria o seguramente de varias formas más que me expresan mucho mejor que es lo que me retorna
- Record Syntax: aclaramos nuevamente que podrían haber redefinido unicamente el gradoDeDiversion manteniendo el resto.
```Haskell
jardineria tipo persona = Persona{
                                  gradoDeDiversion =  ((+ (jardineriaAux tipo)).gradoDeDiversion) persona,
                                  }

```
- Sobre este punto se pedía "no repetir código". Si se fijan, videoJuegos y jardineria poseen practicamente la misma lógica: ambos a partir de un criterio aumentan en N los grados de diversión.
```Haskell
-- Podríamos separar esa parte de la logica en una función
divertirse :: Int -> PasaTiempo 
divertirse grado persona = persona{
    gradoDeDiversion = grado + gradoDeDiversion persona
}
-- Y que las dos funciones que teníamos que implementar la utilicen.
videoJuegos :: Int -> PasaTiempo
videoJuegos nivel persona = divertirse calcularGradoVideoJuego(nivel) persona

jardineria :: String -> PasaTiempo
jardineria tipo persona = divertirse calcularGradoJardineria(tipo) persona
```

**Funcion 4: Todo OK**
```Haskell
esCentennial :: Persona -> Bool
esCentennial persona = (esMayorA1995.anioNacimiento.fechaDeNacimiento) persona

anioNacimiento (_,_,anio) = anio

esMayorA1995 = (>1995)
```
Solo una aclaración: en este caso, se podría haber implementado la función con Point-Free sin ingresar a persona:
```Haskell
esCentennial :: Persona -> Bool
esCentennial = esMayorA1995.anioNacimiento.fechaDeNacimiento
```
Pero no es más que un detalle.

**Funció 5: Todo OK**
```Haskell
golf :: PasaTiempo
golf persona = agregarSir persona

agregarSir persona | empiezaConSir persona = persona
                   | otherwise = sumarSir persona

sumarSir persona = Persona{
nombre = (("Sir " ++).nombre) persona,
fechaDeNacimiento = fechaDeNacimiento persona,
gradoDeDiversion = gradoDeDiversion persona,
hobbies = hobbies persona
}

empiezaConSir persona = ((=="Sir ").(take 4).nombre) persona
```
En este caso, a diferencia de los anteriores, el agregarSir es bien expresivo, al igual que el empiezaConSir. Así, el código queda totalmente claro. Sin embargo, acá devuelta tenemos que recordarle lo del record syntax.

 - Aclaraciones finales:
 Esten más atentos a indicar el tipo de las funciones auxiliares que implementen. En ninguno de los casos se agregó.
 Por otro lado, se olvidaron de ingresar el badge. Para la proxima recuerden agregarlo al README, porque es condición necesaria para tomar la kata como aprobada.
# ALUMNOS
- AGUILA VISITACION, JESSICA MILAGROS	jessica.3091@gmail.com	jessica3091
- ARZA, CHRISTIAN MARIANO	marianoarza@gmail.com	marianoarza 

**NOTA: 3**
**Función 01: Todo OK**

**Función 02: Todo OK**
Muy bien delegando a la función obtenerGradoDiversionJuego.
```Haskell
obtenerGradoDiversionJuego :: Int -> Int
obtenerGradoDiversionJuego nivel | ((>=8) . (div nivel)) 2 = 8
                            | otherwise = div nivel 2

-- ============================================================================================

videoJuegos :: Int -> PasaTiempo
videoJuegos nivel persona  = persona {
                             gradoDeDiversion = gradoDeDiversion persona + obtenerGradoDiversionJuego nivel
}
```
Solo una aclaración: se podrían haber ahorrado la función con guardas utilizando la función min, que recibe dos números y devuelve el más bajo.
```Haskell
obtenerGradoDiversionJuego :: Int -> Int
obtenerGradoDiversionJuego nivel = min 8 (div nivel 2)
```

**Funcion 03: Todo OK** 
Nuevamente, muy bien separando las responsabilidades.
```Haskell
obtenerGradoDiversionJardineria :: String -> Int
obtenerGradoDiversionJardineria tipoJardineria | tipoJardineria == "ornamental" = 10
                                               | tipoJardineria == "bonsai" = 20
                                               | otherwise = length tipoJardineria

jardineria :: String -> PasaTiempo
jardineria tipo persona = persona {
                          gradoDeDiversion = gradoDeDiversion persona + obtenerGradoDiversionJardineria tipo
}
```
Sobre este punto se pedía "no repetir código". Si se fijan, videoJuegos y jardineria poseen practicamente la misma lógica: ambos a partir de un criterio aumentan en N los grados de diversión.
```Haskell
-- Podríamos separar esa parte de la logica en una función
divertirse :: Int -> PasaTiempo 
divertirse grado persona = persona{
    gradoDeDiversion = grado + gradoDeDiversion persona
}
-- Y que las dos funciones que teníamos que implementar la utilicen.
videoJuegos :: Int -> PasaTiempo
videoJuegos nivel persona = divertirse calcularGradoVideoJuego(nivel) persona

jardineria :: String -> PasaTiempo
jardineria tipo persona = divertirse calcularGradoJardineria(tipo) persona
```
**Función 04: Todo OK**
Nada que agregar, está perfecto. Bien delegando, componiendo y notando que no hacia falta poner a persona en la implementación.
```Haskell
obtenerAnioNacimiento (_,_,anio) = anio

esCentennial :: Persona -> Bool
esCentennial = (>=1995) . obtenerAnioNacimiento . fechaDeNacimiento
```
**Función 05: Todo OK**
Todo perfecto. 
```Haskell
controlarSir nombre | take 3 nombre == "Sir" = nombre
                    | otherwise  = "Sir" ++ " " ++ nombre

golf :: PasaTiempo
golf persona = persona {
               nombre = controlarSir (nombre persona)               
}
```
Como aclaraciones muy chiquitas:
 - Habría estado bueno separar el take 3 nombre == "Sir" en una función aparte "yaEsSir" o "empiezaConSir". 
 - en el otherwise, podrían haber puesto "Sir " en lugar del "Sir" ++ " ".

Felicitaciones chicos, buen trabajo!
