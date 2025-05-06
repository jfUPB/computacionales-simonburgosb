# Actividad 1

## ¿Qué es lo que ves?
*	Al presionar el mouse, la ventana se congela por un tiempo prolongado.
*	Durante ese tiempo, el círculo deja de moverse.
*	Después de varios segundos, el círculo cambia de tamaño y continúa su movimiento.
## ¿Qué esperabas ver?
*	Que el círculo siguiera moviéndose de forma continua mientras se realizaba la "computación pesada" (heavyComputation()), como si fueran tareas separadas.
## ¿Por qué crees que sucede esto?
Esto ocurre porque la función heavyComputation() bloquea el hilo principal (el mismo que se encarga de actualizar y dibujar la ventana). Como todo el código está corriendo en un solo hilo, cuando se ejecuta una tarea que toma mucho tiempo, como hacer mil millones de raíces cuadradas, la interfaz gráfica se detiene hasta que termina esa tarea.
## Qué es lo que ves?
* El programa sigue respondiendo, el círculo no se congela.
* El cambio de tamaño del círculo ocurre con retraso, no justo al hacer clic.
## ¿Qué esperabas ver?
* Esperaba que el círculo siguiera animándose (lo cual ocurre).
* Esperaba también que cambiara de tamaño inmediatamente al hacer clic (esto no ocurre de inmediato).
## ¿Por qué crees que sucede esto?
El retraso en el cambio de tamaño del círculo se debe a que:
* La función heavyComputation() sigue siendo una tarea muy pesada que toma varios segundos en ejecutarse.
* Ahora esta función se está ejecutando en un hilo separado, por lo tanto ya no bloquea la animación, lo cual es correcto.
* Sin embargo, el cambio de tamaño del círculo está programado para ocurrir después de que termine la tarea pesada, no antes.

## Concurrencia vs. Paralelismo – En mis propias palabras:
Concurrencia es cuando un programa hace varias cosas "a la vez", pero no necesariamente al mismo tiempo real. Más bien, intercala tareas rápidamente en un solo núcleo, de modo que parece que están ocurriendo simultáneamente. Es como si una persona estuviera haciendo varias tareas, cambiando rápidamente entre ellas: contesta un correo, luego revisa un mensaje, luego vuelve al correo.
Paralelismo, en cambio, es cuando varias tareas se ejecutan exactamente al mismo tiempo, pero en núcleos diferentes del procesador. Es como si varias personas estuvieran trabajando en tareas distintas al mismo tiempo, cada una en su propio escritorio.
## ¿Por qué es importante entender esta diferencia al trabajar con hilos?
*	Ayuda a diseñar mejor tus programas. Si sabes que tu programa correrá en una máquina con un solo núcleo, entonces tus hilos serán concurrentes, no paralelos. Así que tener demasiados hilos no traerá beneficios reales de rendimiento y puede incluso empeorar las cosas.
*	Te prepara para manejar problemas como las condiciones de carrera. En memoria compartida, si múltiples hilos acceden o modifican la misma variable a la vez, podrías tener errores difíciles de detectar. Este riesgo es mayor cuando hay paralelismo real.
*	Entender la diferencia permite optimizar el uso de recursos. Puedes decidir cuándo vale la pena usar hilos, y cómo balancear la carga entre ellos si tienes múltiples núcleos.
