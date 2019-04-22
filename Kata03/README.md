#Alumnos
- RAMÍREZ MOREALE, NICOLÁS PAUL	nicolaspaulmoreale@outlook.com	nramrezmoreale
- ENRIQUEZ, SYLVINA	sylvina64@gmail.com	sylvina64

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
- Funcion 01: Todo OK
- Función 01: Bueno, para empezar tenemos el problema de que no compila por el error mencionado antes:
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
Por un lado no se llega a comprender cual fue la intención de videoJuegosAux (expresividad cof cof). 
Entiendo que intentaron calcular cuanto tiene que subir el Grado de Diversión, y despues sumarlo. 
De hecho, con calcularGrado lo lograban sin problemas (sidenote: vimos que Nicolas lo continuó por su cuenta y también se percato de ello, así que podemos mostrar directamente su solución, aunque esto no va a valer para la kata porque salió despues de hora):

```Haskell
videoJuegos :: Int -> PasaTiempo
videoJuegos nivel persona = persona { 
    gradoDeDiversion = ((+ (calcularGrado nivel)).gradoDeDiversion) persona
}
```
Además, en lugar de pasar cada uno de los componentes de persona nuevamente, solo pasó al que quiere modificar (utilizando el pattern matching del record syntax **Javi: Validame si se llama así**)

- Función 3: Todo OK
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
- Repetición de código: No se si lo habrán notado pero lo que hicimos en la función de videoJuegos y Jardineria hace practicamente lo mismo: le suma un Algo a gradoDeDiversion
```Haskell
divertirse :: Int -> PasaTiempo 
divertirse grado persona = persona{
    gradoDeDiversion = grado + gradoDeDiversion persona
}

videoJuegos :: Int -> PasaTiempo
videoJuegos nivel persona = divertirse calcularGradoVideoJuego(nivel) persona

jardineria :: String -> PasaTiempo
jardineria tipo persona = divertirse calcularGradoJardineria(tipo) persona
```

