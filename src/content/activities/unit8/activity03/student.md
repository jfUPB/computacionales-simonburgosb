## Experimento 1: Cambiar el número de hilos
### Hipótesis:
Si modificamos el número de hilos (con el parámetro numThreads), el rendimiento del algoritmo cambiará. Con más hilos, el cálculo se distribuye entre más núcleos, lo que debería reducir el tiempo total de cálculo. Sin embargo, es posible que haya un punto en el que el overhead de manejar muchos hilos (como la creación y sincronización) haga que más hilos no resulten en una mejora significativa o incluso en un empeoramiento.
### Cambio:
Modifica el número de hilos en el código, cambiando el valor de numThreads. Puedes probar con un valor superior a los núcleos de tu CPU para observar si el rendimiento empeora, ya que en muchos casos, tener más hilos de los que se pueden ejecutar realmente puede ser ineficiente.
### ¿Qué esperar?
* Pocos hilos: Es probable que el rendimiento sea más bajo, ya que no se aprovechan completamente los núcleos del procesador.
* Muchos hilos: El rendimiento puede mejorar, pero si la cantidad de hilos supera los núcleos de la CPU, podría haber un impacto negativo debido al costo de gestión de hilos adicionales.
### ¿Por qué pasa esto?
Cada hilo tiene un costo de creación, sincronización y terminación. A partir de cierto número de hilos, el coste adicional de gestionar estos hilos puede superar la mejora en el rendimiento que ofrecen. Además, el hardware tiene un número limitado de núcleos, por lo que tener más hilos de los que se pueden ejecutar simultáneamente puede llevar a un contexto de cambio excesivo (context switching), lo que ralentiza el proceso.

## Experimento 2: Cambiar el tamaño de la imagen (resolución)
### Hipótesis:
Si aumentas la resolución de la imagen, el tiempo de cálculo aumentará, ya que el algoritmo deberá calcular más píxeles. Además, el paralelismo debería ser más efectivo a medida que la cantidad de trabajo por hilo (el número de filas asignadas) se incrementa.
### Cambio:
Modifica la resolución de la imagen cambiando imgWidth y imgHeight a valores más grandes. Por ejemplo, usa 1920x1080 en lugar de la resolución predeterminada.
### ¿Qué esperar?
Mayor resolución: El tiempo de cálculo aumentará, pero como cada píxel se puede calcular en paralelo, la mejora en el rendimiento debería ser más notable cuando se usan múltiples hilos.
### ¿Por qué pasa esto?
A medida que aumentas la resolución, el número total de píxeles a calcular aumenta exponencialmente. Esto hace que el paralelismo sea más efectivo, ya que hay más trabajo para distribuir entre los hilos.
