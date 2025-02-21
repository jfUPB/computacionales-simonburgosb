# Experimentos

## Experimento 5
¿Qué ocurre?, ¿Por qué?, Ves alguna diferencia entre las variables locales estáticas y no estáticas? y ¿Qué pasa con las variables cada que entras y sales de la función?
*funcionSinStatic() siempre imprime 100 porque su variable local se destruye y se vuelve a crear en cada iteración.
* funcionConStatic() imprime valores crecientes, ya que var_estatica se mantiene entre llamadas.
* Las variables normales (var_no_estatica) se crean y destruyen en cada llamada, por lo que se reinician siempre.
* Las variables estáticas (var_estatica) se inicializan una vez y persisten, manteniendo su valor entre llamadas.
* Normales: Se destruyen al salir de la función.
* Estáticas: Permanecen en memoria y conservan su último valor.

## Experimento 6

* Este código asigna memoria dinámicamente en el Heap y luego intenta acceder a ella después de liberarla.
* Gestión: Heap la hace	manual (new/delete); stack	automática
* Tiempo de vida: Heap es hasta que se libere con delete; stack lo destruye automáticamente al salir de la función
* Si no usamos delete[], ocurre una fuga de memoria (memory leak) lo que lleva a: 
  * La memoria reservada queda inutilizable hasta que el programa termine.
  * Si se repite muchas veces, el programa puede agotar la memoria RAM y volverse más lento o fallar.
* delete[] se usa para liberar memoria asignada con new[].
  * Si usamos delete en lugar de delete[], solo se liberaría la primera posición del arreglo, dejando la fuga de memoria.

