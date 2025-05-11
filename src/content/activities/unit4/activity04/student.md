# Actividad 4

## Explicación Sencilla de una Cola (FIFO) y su Implementación
Imagina que estás en una fila para comprar boletos en el cine. El primer cliente en llegar es el primero en ser atendido, y cuando alguien nuevo llega, se pone al final de la fila. Esto es exactamente cómo funciona una cola en programación: sigue el principio FIFO, es decir, el primero en entrar es el primero en salir.

## ¿Cómo Implementar una Cola Manualmente?
En una cola manual, cada elemento se representa como un nodo que almacena información y un puntero al siguiente nodo en la fila.
### Agregar un elemento al final
Cuando agregamos un nuevo elemento:
* Creamos un nuevo nodo.
* Si la cola está vacía, ese nodo se convierte en el primero y el ultimo. 
* Si la cola ya tiene elementos, el nuevo nodo se coloca después del último.

### Eliminar el primer elemento
Cuando eliminamos un elemento:
* El nodo el más antiguo es eliminado.
* Si la cola queda vacía, debe ser nullptr.

## Error Común: Pérdida de Referencia (Memory Leak)
Un error frecuente es olvidar actualizar front después de eliminar un nodo o no liberar la memoria correctamente.
### Cómo Evitarlo:
Antes de eliminar un nodo, guarda su referencia en una variable temporal, actualiza front, y luego libera la memoria.

