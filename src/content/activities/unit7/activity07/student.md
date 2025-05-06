# ACTIVIDAD 7:

1. El viaje de un vértice

El vértice va desde la CPU al VBO, luego al VAO, pasa por el Vertex Shader, se rasteriza, el Fragment Shader define su color y finalmente se muestra en pantalla.

2. La orquesta gráfica

GLFW y GLAD preparan el entorno, C++ dirige todo, los shaders son los especialistas visuales, y los buffers conectan y transfieren datos entre CPU y GPU.

3. Shaders

Los shaders permiten personalizar el procesamiento gráfico. El Vertex Shader transforma geometría y el Fragment Shader define el color de los píxeles.

4. De la CPU a la GPU

Los VBOs envían datos por vértice (atributos), y los uniforms envían datos constantes (como color o tiempo). Ambos son esenciales para comunicar con la GPU.

5. Concepto clave

El uso de shaders programables es clave porque permite personalizar el comportamiento gráfico en tiempo real, a diferencia del pipeline fijo.

6. Mayor desafío

Entender cómo enviar datos desde C++ al shader usando glUniform fue lo más difícil, y lo superé explorando ejemplos y practicando.
