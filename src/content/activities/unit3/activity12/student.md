# Act 12

## ¿Compila? 
No, el primer código no compila debido a que pBloque2 fue declarado dentro de un bloque {} y 
deja de existir una vez que se sale del bloque. Al intentar acceder a pBloque2 después del bloque, 
el compilador genera un error porque pBloque2 ya no existe.

## ¿Por qué pBloque se destruye al salir del bloque y pBloque2 no?
* pBloque es un objeto automático, es decir, se almacena en el stack y se destruye automáticamente al salir del bloque.
* pBloque2 es un puntero que se almacena en el stack, pero apunta a un objeto en el heap.
* El objeto al que apunta pBloque2 no se destruye automáticamente porque fue creado con new.
•	Es necesario llamar a delete pBloque2; manualmente para liberar la memoria. 
