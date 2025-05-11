# ACTIVIDAD 2: 

## ¿Para qué sirve el patrón Observer?
Sirve para notificar a varios objetos cuando algo ocurre, sin que el que envía el evento tenga que saber qué hacen esos objetos.
Problema que resuelve: evita el acoplamiento fuerte y facilita la extensión del programa.

## ¿Quién es quién?
* Observer → es la interfaz que define onNotify()
* Particle → es un ConcreteObserver porque implementa onNotify() y reacciona
* Subject → tiene la lista de observers y el método notify()
* ofApp → es el ConcreteSubject porque llama a notify()

## Diagrama
           +-------------+
           |   Subject   |  <--- Clase base
           +-------------+
           | notify()    |
           | addObserver |
           +------^------+
                  |
          Inheritance
                  |
              +--------+
              | ofApp  |  <--- Emite eventos
              +--------+

                  |
             notify("r")
                  ↓
          +----------------+
          |   Observer     |  <--- Interfaz
          +----------------+
          | onNotify() = 0 |
                  ↑
          Inheritance
                  |
            +------------+
            | Particle   |  <--- Reacciona al evento
            +------------+
            | setState() |


## ¿Qué pasa cuando presiono ‘r’?
* Presiono 'r' → ofApp::keyPressed() llama notify("repel")
* notify() llama a onNotify("repel") en cada partícula
* Cada partícula cambia su estado a RepelState
* En cada update(), la partícula huye del mouse usando RepelState::update()

## Ventajas del patrón Observer en este proyecto
* Código más limpio y organizado
* Flexibilidad para agregar o quitar partículas fácilmente
