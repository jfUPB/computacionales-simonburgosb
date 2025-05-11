# Actividad 5
## Cálculo del píxel en el conjunto de Julia:
``` cpp
int calculateJuliaPixel(float x, float y, glm::vec2 k, int maxIterations) {
    float zx = x;
    float zy = y;
    int iteration = 0;

    while (zx * zx + zy * zy < 4.0f && iteration < maxIterations) {
        float xtemp = zx * zx - zy * zy + k.x;
        zy = 2 * zx * zy + k.y;
        zx = xtemp;
        iteration++;
    }

    return iteration;
}
```
## Mapeo del mouse a la constante k:
``` cpp
ofApp::mouseMoved(int x, int y)
void ofApp::mouseMoved(int x, int y) {
    juliaK.x = ofMap(x, 0, ofGetWidth(), -1.5f, 1.5f);
    juliaK.y = ofMap(y, 0, ofGetHeight(), -1.5f, 1.5f);
    needsUpdate = true;  // Flag para recalcular
}
``` 
## Reutilización de la estructura de hilos:
Reutilicé el mismo sistema de múltiples hilos que dividen la imagen por filas. En lugar de llamar a calculateMandelbrotPixel, cada hilo ahora llama a calculateJuliaPixel, pasando la k actual. No fue necesario modificar la estructura de creación o unión de hilos. Solo cambié la función que cada hilo ejecuta y me aseguré de que juliaK esté accesible o pasada como argumento.
## Recalcular al mover el mouse:
Usé una variable needsUpdate que se activa cada vez que el mouse se mueve (mouseMoved). En update(), si needsUpdate es true, relanzo los hilos para que recalculen toda la imagen con la nueva k. Luego, pongo needsUpdate = false para evitar recálculos innecesarios.
## Desafíos encontrados:
* Estabilidad de la imagen: Al mover el mouse rápidamente, algunos valores de k producen fractales que se "vuelven negros" o desaparecen. Para solucionarlo, limité el rango de mapeo de k o aumenté las iteraciones máximas.
* Sincronización del recálculo: Tuve que asegurarme de que los hilos terminararan antes de que se volviera a dibujar el buffer de la imagen. Usé join() correctamente para evitar condiciones de carrera.
* Rendimiento: Al mover el mouse muy rápido, se lanzaban muchos recálculos. Como solución, establecí un pequeño retraso mínimo entre cada actualización o filtré actualizaciones redundantes (si k no cambia significativamente).
