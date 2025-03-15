# Miembros estaticos y variables de instancias

## Conclusiones sobre los miembros estáticos y de instancia en C++

### Diferencias entre miembros de instancia y estáticos:
* Los miembros de instancia pertenecen a cada objeto de la clase. 
* Los miembros estáticos pertenecen a la clase en sí y son compartidos por todas las instancias. 

### Gestión en memoria:
* Los miembros de instancia se almacenan en el stack o en el heap. 
* Los miembros estáticos se almacenan en la data segment del programa y existen una sola vez, independientemente del número de instancias.

### Ventajas y desventajas de los miembros estáticos:
#### Ventajas:
* Permiten compartir información entre todas las instancias sin duplicar datos.
* Son útiles para contar instancias de una clase 
#### Desventajas:
* No pueden acceder directamente a miembros no estáticos.

### Cuándo utilizarlos:
* Cuando se necesita una variable compartida por todas las instancias, como un contador de objetos.
* Para definir métodos que operan sobre la clase y no sobre instancias individuales 

### Ubicación en memoria de las variables en el programa:
* c1 y c2:
Son variables locales en main(), por lo que se almacenan en el stack.
* Contador::total:
Es un miembro estático, por lo que se almacena en el data segment
* c3:
c3 es un puntero, y como es una variable local la cual se almacena en el stack.
*c3, es decir, el objeto al que apunta c3, se creó con new, por lo que se almacena en el heap.
