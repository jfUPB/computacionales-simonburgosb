# ACTIVIDAD 4: 
1.	Estructura de datos principal: El vector boids de la clase Flock es la estructura de datos principal que contiene la información de todos los boids y es accedida por múltiples hilos (el hilo principal para dibujar y el hilo trabajador para actualizar).
2.	Operaciones sobre el vector de boids en threadedFunction(): El hilo trabajador recorre el vector boids y actualiza las posiciones de los boids mediante la función b.run(boids).
3.	Operación en ofApp::draw() sobre el vector compartido: El hilo principal recorre el vector boids y dibuja cada boid en la pantalla usando b.draw().
4.	Operación en Flock::addBoid() y mouseDragged(): Flock::addBoid() agrega un nuevo boid al vector boids y mouseDragged() es el evento que llama a esta función cuando el usuario mueve el ratón.
5.	Escenario problemático de sincronización: Si el hilo principal está recorriendo el vector boids (por ejemplo, en ofApp::draw()) y el hilo trabajador intenta agregar un boid al vector (Flock::addBoid()), puede ocurrir una condición de carrera. El iterador del hilo principal puede volverse inválido si el tamaño del vector cambia mientras se recorre.
6.	Llamadas a lock() y unlock(): Las llamadas a lock() y unlock() se encuentran en las funciones Flock::addBoid() y Flock::threadedFunction(), donde se protege el acceso al vector boids para evitar condiciones de carrera.
7.	Justificación del uso de lock() y unlock(): En el escenario mencionado, el uso de lock() en Flock::addBoid() y Flock::threadedFunction() asegura que el acceso al vector boids sea exclusivo para un solo hilo a la vez. Esto evita que el hilo principal y el hilo trabajador accedan al vector simultáneamente, lo que podría causar problemas de lectura y escritura en el vector.
8.	Contención y rendimiento: Tener muchos hilos esperando por un lock sobre el mismo vector podría limitar el rendimiento del paralelismo. Aunque los hilos pueden estar trabajando en diferentes tareas, la contención del lock significa que solo un hilo podrá acceder al vector a la vez, lo que genera cuellos de botella. Esto reduce la ventaja del paralelismo porque los hilos no pueden aprovechar completamente los recursos del sistema mientras esperan para acceder a la misma estructura de datos.
* Reflexión sobre hilos en flocking: Tener solo dos hilos (uno para el cálculo y otro para el dibujo) limita el potencial de paralelización. Si tuviéramos varios hilos calculando el movimiento de los boids, podríamos aprovechar mejor los recursos del sistema, distribuyendo el trabajo entre múltiples núcleos de CPU. Sin embargo, esto traería problemas como condiciones de carrera y carga desbalanceada, que se pueden solucionar con sincronización (mutex) y balance de carga.
## Análisis del código de Flocking con y sin hilos:
* Sin hilos, todo el trabajo se realiza secuencialmente en un solo hilo.
* Con hilos, el cálculo del movimiento se realiza en un hilo secundario, mientras que el hilo principal se encarga de dibujar los boids.
* La sincronización es esencial para evitar condiciones de carrera y errores en el acceso a memoria compartida.
* Añadir boids ralentiza la simulación debido al aumento de la carga computacional y posibles problemas de sincronización.
* El sleep(5) en el hilo trabajador se utiliza para evitar un uso excesivo de CPU y para equilibrar el trabajo entre los hilos. Si se elimina, el hilo trabajador podría ejecutar demasiadas veces sin esperar, afectando el rendimiento.

## Rendimiento y lock/unlock:
* Sin hilos: Limitado por la ejecución secuencial.
* Con hilos: Potencialmente más rápido, pero la sincronización incorrecta podría disminuir el rendimiento.
* Si no se usan lock/unlock, podrían ocurrir condiciones de carrera, resultando en un comportamiento impredecible, como posiciones incorrectas de los boids o caídas del programa.

## ¿Por qué ocurriría esto? 
El problema se da porque ambos hilos (principal y trabajador) están intentando acceder y modificar la misma lista de boids sin mecanismos de sincronización. Cuando el hilo trabajador está calculando el movimiento de los boids, cualquier cambio en la estructura de datos (como añadir un boid) puede generar conflictos. El hilo principal podría intentar agregar un boid en una ubicación que el hilo trabajador todavía no ha procesado, o el trabajador podría intentar acceder a un boid que el principal está eliminando o modificando.
## ¿Se congelará la aplicación? 
No necesariamente se congelará de inmediato, pero la aplicación podría comportarse de manera errática, y si el conflicto es grave, puede llevar a bloqueos o caídas del programa. La congelación podría ocurrir si los hilos entran en un estado de espera mutua, lo que se conoce como un deadlock.
