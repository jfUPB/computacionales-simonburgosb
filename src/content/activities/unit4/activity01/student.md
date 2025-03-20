# Actividad 1



## ¿Cómo se crea la lista enlazada?
La lista enlazada se declara en ofApp.h como una variable miembro de la clase ofApp:

glm::vec2 target = glm::vec2(ofGetMouseX(), ofGetMouseY());
    float interpolationFactor = 0.2;  // controla la velocidad de movimiento (0-1)

    for (auto& pos : snake) {
        pos = glm::mix(glm::vec3(pos, 0.0f), glm::vec3(target, 0.0f), 0.2); // Se mueve gradualmente
        target = pos;  // Cada nodo sigue al anterior
    }

Esto crea una lista doblemente enlazada de posiciones (glm::vec2), donde cada nodo representa una posición en el plano.

## ¿Cómo se añaden los primeros nodos a la lista?
En el método setup() de ofApp.cpp, se agregan los primeros 20 nodos. 

## ¿Cómo se añaden nodos adicionales a la lista?
Se pueden agregar nodos presionando la tecla 'a', lo cual está definido en keyPressed(int key):

## ¿Cómo se eliminan nodos de la lista?
Presionando la tecla 'r', se elimina el último nodo

## ¿Cómo se limpia la lista?
Presionando la tecla 'c', se borra completamente la lista

## ¿Cómo se verifica si la lista está vacía?
Antes de eliminar un nodo, se usa la condición:

if (!snake.empty()) {
Esto comprueba si la lista contiene nodos antes de intentar eliminar uno. }
