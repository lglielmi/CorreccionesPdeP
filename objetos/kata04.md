# [Agustín Tamborini (TamboriniAgustin) y Nicolás Lannert (nicolasLannert) - Te lo codeo como bokita](https://github.com/pdep-utn/kata-04-hogar-te-lo-codeo-como-bokita-papa-2)
Solo hay un commit con todo hecho por Agustin. Se hacia en casa o en la facu esta kata? Onda me da la sensación de que lo hizo todo Agustin pero bueno, detalle.
## 1. Nivel de confort de las Habitaciones
### En general
Ok con que hayan usado herencia dado que no debería cambiar el tipo de habitación.

Lo que si podría estar mejor es usar template method para separar el valor base del particular según la clase de habitación. Creo que vieron el patron en octubre.
### Integrante 1: 
**Habitación uso general y cocina**
- Al no usar template method, uso general es una clase vacia si o si. 
- Cocina está ok, sin embargo como hacen el stub para el test no. Lo ideal sería que en lugar de mandar "return 5.randomUpTo(15)" de una, llamen a un metodo auxiliar que haga eso y que el stub herede de cocina (no de habitación) y reimplemente a este metodo auxiliar.

### Integrante 2:
**Habitación Baño y Dormitorio**
- Baño todo ok.
- Con dormitorio malinterpretaron el enunciado. Entendieron que *En caso de un dormitorio en el que duermen dos personas, sumaría 5 a cada una* era enunciado y no un ejemplo.
Estaba escrito medio ambiguo pero creo que se entendía. No se. Suponiendo que la consigna era así, lo delegaron bastante bien así que se los marcaría pero no les reduciría todo el puntaje.
Obviamente los test quedaron raros porque clavaron muchos más casos de los esperados.

## 2. Consultas sobre la familia y la casa
- 2.1 (Integrante 1) Saber las habitaciones que están ocupadas de una casa (tienen al menos un ocupante). **Ok** Sin embargo, el test que se le hizo no esta bueno. Si casaLoca().habitacionesOcupadas() hubiera devuelto a cocina (que está desocupada), habria dado todo ok igual.
- 2.2 (Integrante 1) Saber los responsables de la casa, el cual es el conjunto formado por el ocupante más viejo de cada habitación ocupada. **Ok**
- 2.3 (Integrante 2) Saber si una familia está a gusto, para lo cual tiene que suceder que todos los integrantes de la familia se sienta a gusto en la casa donde vive la familia. **No está implementado**

Además a Casa le agregan una validación que no está pedida en ningún lado.

Implementación de Persona: No cumple con *Queremos que una persona pueda cambiar de forma de ser a lo largo del tiempo.*

- Obsesives: si todas las habitaciones están ocupadas (tienen al menos un ocupante). **Ok** 
- Goloses: si al menos un miembro de la familia tiene habilidades de cocina. **Ok** Falta su test para cuando no está a gusto.
- Sencilles: si la casa tiene al menos 1 habitación más que la cantidad de miembros de la familia. **Ok**
