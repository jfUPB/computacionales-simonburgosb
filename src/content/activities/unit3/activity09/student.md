# Copia en C++ Y C#

## C++

Crea un nuevo objeto copia, que tiene sus propios valores x, y y name. Como name es una cadena de std::string, se hace una copia automática del contenido. Luego, al modificar copia, los cambios no afectan a original, lo que confirma que es una copia independiente.
Puede usarse punteros para compartir objetos en memoria.

## C#

Ambas variables (copia y original) referencian el mismo objeto en memoria. Cualquier cambio en copia también afectará a original, ya que ambas variables son solo referencias al mismo espacio de memoria.
Se usan referencias implícitamente (sin punteros explícitos).
