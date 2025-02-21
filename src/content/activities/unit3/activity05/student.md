# Experimento

## Experimento 3

¿Que ocurre? y ¿Por que? 
* global_inicializada = 42;  Se almacena en el segmento de datos (.data) porque tiene un valor asignado.
* global_no_inicializada;  Se almacena en el segmento de variables (.data) y se inicializa en cero automáticamente por el sistema.
* global_inicializada imprimirá 42 (porque ya tenía un valor asignado).
* global_no_inicializada imprimirá 0 (porque el segmento de variables inicializa a cero las variables no inicializadas).
* global_inicializada se reecribe a 69 (porque ya tenía un valor asignado y se permite ya que están en memoria de lectura y no son protegidas).
* global_no_inicializada se modifica a 666 (porque no tenía un valor asignado y se permite ya que están en memoria de lectura y no son protegidas).
* global_inicializada ahora imprime 69.
* global_no_inicializada ahora imprime 666.

## Experimento 4

¿Que ocurre?, ¿Por que?, ¿Qué pasa con las variables cada que entras y sales de la función? y ¿Qué pasa con las variables locales estáticas?
* El código original genera un error de compilación porque var_estatica solo existe dentro de funcionConStatic().
* Las variables locales normales se destruyen al salir de la función.
* Las variables locales estáticas mantienen su valor entre llamadas.
