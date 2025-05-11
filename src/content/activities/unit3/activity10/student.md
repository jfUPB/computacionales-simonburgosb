# Funciones y objetos en C++

## ¿Qué ocurre después de llamar a la función cambiarNombre? ¿Por qué aparece el mensaje Destructor: Punto cambiado(70, 80) destruido.? ¿Por qué original sigue existiendo luego de llamar cambiarNombre?
Original no cambia su nombre, sigue llamándose "original". Esto ocurre porque la función cambiarNombre recibe su parámetro por valor. 
Esto significa que dentro de la función se crea una copia temporal de original, llamada p. Se modifica el atributo name en esa copia, pero no afecta al objeto original en main. Cuando la función termina, la copia p es destruida, y por eso se imprime
El mensaje indica que el objeto copia (p) ha sido destruido, no original.

## ¿En qué parte del mapa de memoria se encuentra original y en qué parte se encuentra p? ¿Son el mismo objeto?
### original
* original se encuentra en el stack de main(), ya que es una variable local de main().
* Como es una instancia de la clase Punto, sus atributos (name, x, y) también están en el stack.
### p en cambiarNombre
* p es una copia de original
* Sus atributos (name, x, y) son independientes de los de original.
* Cuando cambiarNombre termina, p se elimina del stack y se ejecuta su destructor.
  
Por lo tanto, original y p no son el mismo objeto. Son objetos distintos con valores idénticos al principio, pero completamente independientes en memoria.

## Cambio de la funcion: cambiarNombre

Al cambiar la funcion para usar usar referencia en lo que es p, ya este si permite modificar el original. 

## Cambio del main y nuevante de la funcion: cambiarNombre

Esto significa que p almacena la dirección de memoria del objeto original, en lugar de crear una copia.
Cuando modificamos p->name, estamos modificando directamente el objeto en main(), ya que p apunta a original.
