# ACTIVIDAD 6:
## Responsividad
Usar un hilo ayuda cuando una tarea pesada (como cálculos) puede hacer que la interfaz se congele. Al moverla a otro hilo, la app sigue siendo fluida.
## Paralelismo
Si la tarea se puede dividir (como calcular píxeles independientes en fractales), varios hilos pueden trabajar al mismo tiempo, acelerando el proceso.
## Estado compartido
El problema es que varios hilos pueden modificar los mismos datos al mismo tiempo. La solución es usar lock para evitar errores.
## Comparación de casos
Mandelbrot/Julia no necesitan sincronización porque cada hilo trabaja por separado. En cambio, Flocking sí, porque todos los boids comparten datos.
## Conclusión personal
Usaría hilos para mantener la app fluida o acelerar cálculos. Siempre cuidaría la sincronización cuando los hilos compartan datos.
