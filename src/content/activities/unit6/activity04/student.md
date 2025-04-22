# ACTIVIDAD 4: 

## Propósito del patrón State
El patrón State me permite cambiar el comportamiento de un objeto según su estado interno, sin tener que usar muchos if o switch. Es útil cuando un objeto tiene varios modos de funcionamiento y esas formas pueden cambiar dinámicamente. En mi caso, las partículas cambian su movimiento según si están en estado normal, de atracción, repulsión o detención.

## Diagrama explicado en palabras simples
Imagino a la clase Particle como una burbuja central que puede estar en uno de cuatro estados:
* Normal
* Attract
* Repel
* Stop

Cada estado es como un nodo, y las transiciones entre ellos ocurren cuando se presionan teclas:
* Presiono 'n' → cambia a Normal
* Presiono 'a' → cambia a Attract
* Presiono 'r' → cambia a Repel
* Presiono 's' → cambia a Stop

Cada transición es una flecha entre los nodos. Las teclas son como los disparadores que mueven la partícula de un estado a otro.

## Ventajas del patrón State vs. if/switch
Usar el patrón State me da un código más limpio y organizado. En vez de tener muchos if en update() preguntando por el estado actual, cada estado se encarga de su propio comportamiento. Eso mejora la cohesión, ya que cada clase hace solo lo que le corresponde. Además, si quiero agregar un nuevo estado (por ejemplo, "Explode"), solo creo una nueva clase sin tocar el código de Particle. Esto sigue el Principio Abierto/Cerrado: el código está abierto a extensión pero cerrado a modificación.

## Rol de onEnter y onExit
onEnter y onExit son métodos que se ejecutan al entrar o salir de un estado. Sirven para preparar o limpiar cosas. Por ejemplo, en AttractState::onEnter() podría mostrar una animación de atracción, o guardar la posición del mouse. En StopState::onExit() podría reiniciar la velocidad de la partícula para que vuelva a moverse. Aunque no se usan mucho en este ejemplo, son muy útiles para manejar cambios visuales o reiniciar variables cuando el estado cambia.
