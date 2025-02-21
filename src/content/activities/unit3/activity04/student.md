# Experimentacion 1

## Codigo 1

¿Que ocurre? y ¿Por que? 
* &main obtiene la dirección de memoria donde está almacenada la función main(), que se encuentra en el segmento de código (también llamado text segment).
* reinterpret_cast<void*> se usa para convertir la dirección a un puntero genérico (void*), lo cual evita advertencias del compilador.
* Se convierte ptr a un puntero int*, lo que permite tratar esa dirección como si almacenara un entero.
* Luego, *reinterpret_cast<int*>(ptr) = 0; intenta escribir un 0 en esa dirección de memoria.
* Esto genera un error ya que las direcciones son datos protejidos, por lo tanto no se puede modificar la direccion por un entero

## Codigo 2
* La dirección almacenada en mensaje_ro no puede cambiar.
* El contenido al que apunta ("Hola, memoria de solo lectura") está en memoria de solo lectura (segmento de texto o .rodata).
* &mensaje_ro obtiene la dirección del puntero mensaje_ro, no del contenido del string.
* Se castea a char*, permitiendo modificarlo sin advertencias del compilador.
* Luego, *ptr = 0; intenta escribir un 0 en esa dirección.
* Esto genera un error ya que las direcciones son datos protejidos, por lo tanto no se puede modificar la direccion por un entero
