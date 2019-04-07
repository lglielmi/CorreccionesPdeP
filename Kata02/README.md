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
