# Descifrando el hack

## ¿En qué direcciones de memoria se implementan las variables i y sum?

En Hack, las variables no predefinidas se almacenan en la RAM en direcciones que empiezan desde la dirección 16 en adelante.

i se almacena en la primera dirección de memoria disponible, por lo que está en RAM[16].

sum es la siguiente variable, así que está en RAM[17].

Por lo tanto:
* i → RAM[16]
* sum → RAM[17]

## Diferencia entre la dirección de una variable y su contenido

La dirección de una variable es el lugar en la memoria donde se almacena su valor. El contenido es el valor almacenado en esa dirección.

##  Cómo se implementa la condición i <= 100

* D;JGT Evalua si el numero guardado en D es mayor a O
*  Si i > 100, entonces D = i - 100 será mayor que 0, lo que activa el salto a END.
*  Si i <= 100, el programa sigue sumando valores.
