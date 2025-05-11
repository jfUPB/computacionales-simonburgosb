# ACTIVIDAD 2: 
## ¿Qué ocurre si cambias el valor de la variable useLock?
* Cuando useLock está en true (lock habilitado): Los hilos se sincronizan correctamente usando el locker (el objeto ofThread). Esto asegura que solo un hilo pueda modificar el contador a la vez, lo que elimina la condición de carrera y produce el valor correcto.
* Cuando useLock está en false (lock deshabilitado): Los hilos pueden modificar el contador sin ninguna sincronización. Esto lleva a condiciones de carrera, donde los hilos compiten por acceder al contador y los valores finales son incorrectos (y generalmente menores al esperado), ya que se produce una interferencia entre los hilos.

## ¿Por qué crees que ocurre esto?
* Con lock(), la sincronización garantiza que solo un hilo acceda al contador a la vez, evitando que se sobrescriban los valores del contador simultáneamente.
* Sin lock(), varios hilos pueden acceder y modificar el contador simultáneamente, lo que causa que algunos incrementos se "pierdan" o que varias escrituras se realicen de manera incorrecta, creando un desfase en el valor final.

La condición de carrera ocurre cuando varios hilos acceden y modifican una variable compartida sin sincronización, lo que provoca resultados incorrectos. En este caso, cuando useLock está en false, múltiples hilos intentan incrementar la misma variable counter simultáneamente, pero la operación de incremento (++(*counter)) no es atómica, lo que significa que varios hilos pueden leer y escribir el valor al mismo tiempo, perdiendo actualizaciones.
Por ejemplo, si dos hilos leen el mismo valor de counter (0), lo incrementan a 1 por separado y lo escriben de nuevo, el resultado final es 1, cuando debería ser 2.
Usar lock() resuelve el problema, ya que asegura que solo un hilo pueda modificar counter a la vez, evitando las interferencias y garantizando un resultado correcto.
Este problema es un ejemplo de condición de carrera, y puede evitarse mediante sincronización adecuada entre los hilos.
