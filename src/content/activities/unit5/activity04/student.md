# ACTIVIDAD 4:
## Encapsulamiento
Resumen: Agrupo los atributos y comportamientos de cada partícula dentro de su clase, y evito el acceso directo desde fuera. Dónde se aplica:

class RisingParticle : public Particle { protected: glm::vec2 position; ... };

## Herencia
Resumen: Creo nuevas clases a partir de una clase base para reutilizar código y especializar comportamiento. Dónde se aplica:

class RisingParticle : public Particle { ... };
class CircularExplosion : public ExplosionParticle { ... };

## Polimorfismo
Resumen: Uso punteros a la clase base Particle para tratar diferentes tipos de partículas y llamar a sus métodos apropiados automáticamente. Dónde se aplica:

particles[i]->update(dt); particles[i]->draw(); // llamados polimórficos

## Objeto y Clase
Resumen: Una clase es una plantilla de código, y un objeto es una instancia real de esa plantilla en memoria con datos concretos. Dónde se aplica:

particles.push_back(new RisingParticle(...)); // creación de un objeto

## Objeto en memoria con herencia
Resumen: Un objeto que hereda contiene primero los atributos de la clase base, luego los de la derivada, y un puntero a la vtable si hay métodos virtuales. Dónde se aplica:

class CircularExplosion : public ExplosionParticle { ... }; // hereda estructura en memoria
