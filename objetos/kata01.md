# Te lo codeo como bokita papá (odio este nombre)

TAMBORINI AGUSTÍN	TamboriniAgustin Te lo codeo como bokita papá (2052)
LANNERT, NICOLÁS	nicolasLannert	Te lo codeo como bokita papá(2152)

**NOTA: 1**

- **No compila la solución.** 

Actualmente en travis se puede chequear que no se están ejecutando los test (y de hecho, el badge está en failing)
No compila debido a que definieron al method comerseUnBigMac(), sin embargo en la aplicación que correspondía dentro de diaDeTrabajo(), tipearon a comerBigMac().
Corregido esto, al ejecutar los test hay algunos que dan mal

- **"Olivia recibe masajes muchas veces y su grado de concentracion aumenta bastante más al estar relajada"**

El enunciado indica "a partir del tercer masaje, al estar más relajada su grado de concentración aumenta 5 puntos", utilizaron > 3 cuando correspondía >= 3.
Además, para sumar un valor, recuerden que pueden utilizar la notación concentracion = + 5 (para no tener que escribir la variable 2 veces).

- **"Si discute una sola vez, el estado inicial Olivia queda su concentración inicial"**

El enunciado indica "cuando discute, su grado de concentración baja a 5, salvo que tenga menos de 5 puntos de concentración, en cuyo caso no pasa nada".
Lo que se está realizando en el method discutir() no refleja esto: coloquialmente, lo realizado es "si la concentración es < 5, asignarle al estado "Concentración" un 5. Sino, restarle 5.

Por un lado, si la concentracion es < 5 no debería hacer nada, pero en la implementación se hace algo:
cuando la concentración es 0, 1, 2, 4 debería quedarse así, pero en todos esos casos lo están reemplazando por 5.

Por otro lado, no dice que se deba bajar 5 grados, sino que BAJA A 5, lo cual no es lo mismo.

Una manera de resolver este punto sería la siguiente:
```
method discutir() {
  concentracion = 5.min(concentracion) //Retorna al más bajo entre 5 y gradoDeConcentración)
}
```
o 
```
method discutir() {
  if (concentracion > 5) concentracion = 5
}
```

- **"cuando discute, su grado de concentración baja a 5, salvo que tenga menos de 5 puntos de concentración, en cuyo caso no pasa nada."**

Este test no pasa debido a lo mismo que en el punto anterior: en el test olivia discute 4 veces. 
Originalmente su concentración es 4, entonces en ningún momento debería verse afectada.
Sin embargo por su implementación, esto ocurre.

- **"Si Olivia se da un masaje y luego discute, su estado inicial queda con el máximo grado de concentración posible"**

Originalmente el grado de concentración es 4. Luego del masaje pasa a 5. Al discutir, su implementación resta 5 (dejandolo en 0), pero debería dejarlo en 5.

- **Posibles mejoras:**

Pueden evitar el uso de tantos IFs en recibirMasajes utilizando el metodo max que conocen los nros:
```
	method recibirMasajes(){
		contractura = 0.max(contractura - 2) //Retorna al más alto entre 0 y nivelDeContractura-2
	}
```
Dentro de codear(), tal vez sería más feliz separar la condición cantidadDeVecesQueCodeo == 1 en un metodo yaCodeo() = cantidadDeVecesQueCodeo == 1.

Esto puede hacer al código más declarativo, además de que le sacamos a codear() la responsabilidad de definir si adriano codeó o no.

- **Punto Teorico** Nota: la primera no me gusta mucho pero creo que sela podemos dar como bien y la 3ra está mal. Se lo marcamos?

  ¿Dónde aparece el concepto polimorfismo? Justifique.
  
 	Aparece en los métodos darBanioDeVapor, recibirMasaje, y todos aquellos que sean
 	 compartidos por mas de un objeto, ya que si los llamo sabran actuar diferente
 	 en cada uno de estos.
 	
	¿Quién es el objeto que se beneficia de ese concepto? Justifique.
  
	Aquel que envia el mensaje. 
	
	¿De qué tipo es el parámetro persona de spa?
  
	Es de tipo objeto.

---------------------------------------------------------------------------------------------------------------
# BTF 
BUCCI, PABLO 		PabloBucci	BTF (2152)
CONTESTABILE, ALEJO 	AlejoCont  BTF (2152)

**NOTA: 2**

La solución no pasa por todos los tests.

- **""Olivia recibe masajes muchas veces y su grado de concentracion aumenta bastante más al estar relajada"**

Debido a que en su implementación primero modifican el grado de concentración y suman 1 a la cantidad de masajes termina sucediendo que:
  
  La primera ejecución: cant masajes = 0, sumo 2. Luego cant masajes = 1. OK
  
  La segunda ejecución: cant masajes = 1, sumo 2. Luego cant masajes = 2. OK
  
  la tercera ejecución: cant masajes = 2, sumo 2 Luego cant masajes = 3. Pero este es el tercer masaje!! debería haber sumado 5!!

La manera más simple de solucionarlo sería sumarle 1 a cantidad de masajes antes de la modificación del grado de concentración.

- **"Adriano codea más de una vez y se contractura lo mismo que si codeara una sola vez"**

Debería aumentar su contractura solo la primera vez que codea. A partir de la segunda, esto no debería sucederle.
Podrías guardar un estado que sea un booleano, el cual inicialmente esté en false y pase a true la primera vez que se ejecuté codear (y en base a eso, saber si le tenes que sumar o no)

- **"Adriano tiene un día de trabajo y se contractura un poco"**

Error acarreado por lo anterior en relación a codear().

- **Posibles mejoras**

Para discutir() podrían salvarse de usar el if utilizando el metodo min que conocen los nros
```
method discutir(){
		gradoDeConcentracion = 5.min(gradoDeConcentracion) //Retorna al más bajo entre 5 y gradoDeConcentración)
	}
```
De manera similar para recibirMasajes() de adriano, pero utilizando max
```
method recibirMasajes(){
		nivelDeContractura = 0.max(nivelDeContractura - 2)  //Retorna al más alto entre 0 y nivelDeContractura-2
	}
```

Ojo que comerseUnBigMac() y darseUnBanioDeVapor() no son mensajes sino acciones. No debería estar definido con "= ()" sino entre "{}"

- **Punto Teorico** Nota: Este me gusta más que el primero. Lo marcaría como ok de una.

¿Dónde aparece el concepto polimorfismo? Justifique. 

Aparece cuando los objetos entienden un mensaje con el mismo nombre y tienen comportamientos diferentes. Ej: recibirMasaje() que actúa distinto en Olivia y Adriano.

¿Quién es el objeto que se beneficia de ese concepto? Justifique. 

El objeto que utiliza a los objetos polimórficos. En este caso spa atiende a Olivia y a Adriano de igual manera, pero cada uno obtuvo efectos diferentes.

¿De qué tipo es el parámetro persona de spa? 

Tipo personas

- **Test de Spa**

Falta responder las preguntas teoricas y no se testea el nivel de contractura de Adriano


