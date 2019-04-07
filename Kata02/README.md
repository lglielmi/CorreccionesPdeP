# SOSA CELMAN, IGNACIO HERNAN	& AMAYA, TAMARA LUJAN
- igsosa.92@gmail.com	igsosacelman
- lujan.amaya@hotmail.com	Poisondrops

## Solucion
nombreDificil :: Persona -> Bool
nombreDificil = (>15).length.nombre
edadDificil :: Persona -> Bool
edadDificil = (>=40).(+1).edad

# ORELLANA, AYLEN JORGELINA	& ANZORANDÍA, MATÍAS LEANDRO
- Ayluorellana@gmail.com	aylu2910
- Matias.l.anzorandia@gmail.com	matiasanz

## Solucion
```Haskell
nombreDificil :: Persona -> Bool
nombreDificil  = (>15).length.nombre
edadDificil :: Persona -> Bool
edadDificil  =(>=40).(1+).edad
```

#Corrección (para ambos dado que son iguales)
- **Nota: 2**
Bien utilizada la composición y aplicación parcial en ambos casos. La función cumple con todos los requerimientos planteados.

Solo a modo de comentario (porque la solución está perfecta), queriamos mencionarles que la composición les abre las puertas a poder separar la funcionalidad de tal manera que puede otorgarnos mayor claridad en el codigo (aunque en otros casos no, y en ese punto es donde entrará en juego su criterio como desarrolladores).

Por citar un ejemplo:
Se podría haber creado la siguiente función:
```Haskell
longitudNombre :: Persona -> Integer
longitudNombre  = length.nombre
```
y luego utilizarla en la función nombreDificil:
```Haskell
nombreDificil :: Persona -> Bool
nombreDificil  = (>15).longitudNombre
```
Para este caso, nos gusta más la solución de ustedes, pues length es suficientemente claro y vuelve redundante a longitudNombre. Pero no queriamos dejar de mencionarlo ya que se presentaran otros casos donde será conveniente la separación.
