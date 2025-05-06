# ACTIVIDAD 3: 
##  Sobre glViewport
### Cuando haces:
glViewport(0, 0, bufferWidth, bufferHeight);
Estás diciendo: "Usa todo el framebuffer para dibujar".
### Cuando haces:
glViewport(0, bufferHeight/2, bufferWidth/2, bufferHeight/2);
Estás diciendo: "Dibuja sólo en un cuarto superior izquierdo del framebuffer".
•	Dividir los valores por 2, 4, etc., hace que el área donde OpenGL dibuja se vuelva más pequeña.
•	Multiplicar los valores por 2, 4, etc., puede hacer que el área se salga del framebuffer (lo que genera resultados extraños, como que parte del dibujo no se vea o se deforme).
## ¿Qué crees que pasa?
Al cambiar el viewport, cambias la región donde OpenGL mapea sus coordenadas normalizadas (de -1 a 1) en la ventana. Así que el dibujo se adapta a esa nueva región.
Hasta ahora he aprendido que OpenGL necesita un contexto para funcionar. Ese contexto se crea con la ayuda de GLFW, que además facilita la creación de la ventana y la gestión de eventos como el teclado y el mouse.
Cuando OpenGL dibuja, lo hace en un framebuffer, que es como una hoja invisible donde va pintando todo antes de mostrarlo en pantalla.
El viewport es la zona específica dentro del framebuffer donde el dibujo realmente aparece, y si cambiamos su tamaño o posición, cambiamos la forma en que los gráficos se ven.
He entendido también que OpenGL no dibuja directamente: simplemente da instrucciones a la GPU, que es la que hace el trabajo real.
## ¿Qué es el contexto OpenGL?
El contexto OpenGL es como el "taller de arte" donde se guardan todas las herramientas y materiales: pinceles, colores, reglas, etc. Es un espacio de trabajo donde OpenGL mantiene toda la información: buffers, estados, texturas, shaders, etc.
Sin un contexto, OpenGL no puede trabajar, igual que un artista no puede pintar sin su taller preparado.
## ¿Cuál es el rol de la biblioteca GLFW y qué ventaja tiene usarla?
GLFW es una biblioteca que nos facilita crear ventanas, manejar eventos de teclado y ratón, y gestionar el contexto de OpenGL en diferentes sistemas operativos (Windows, Mac, Linux).
La gran ventaja es que no tenemos que escribir código específico para cada sistema. GLFW lo hace por nosotros, permitiéndonos enfocarnos en la lógica gráfica.
## ¿Por qué crees que OpenGL necesita un contexto?
Como la analogía del taller de arte, OpenGL necesita un "espacio" donde organizar todos sus recursos.
Sin contexto, no sabría dónde dibujar, qué herramientas usar ni qué configuraciones aplicar.
Contexto = espacio de trabajo en la memoria de la GPU.
## ¿Qué será el framebuffer y a qué te recuerda de las primeras unidades?
El framebuffer es como un lienzo donde OpenGL dibuja cada imagen antes de mostrarla en pantalla.
Me recuerda a conceptos de buffers en programación o a imágenes en memoria que vimos al principio del curso: es un área donde se almacenan temporalmente datos visuales antes de mostrarlos.
## ¿Qué relación hay entre el viewport y el framebuffer?
El viewport es como una ventana a través de la cual miramos una parte del framebuffer.
* El framebuffer puede ser grande, pero el viewport define qué parte se muestra y en qué tamaño.
* Si cambias el tamaño del viewport, cambiará cómo se dibujan los objetos.
## ¿Qué rol juegan los drivers de la GPU y la GPU misma?
* GPU: Es el "artista" real que ejecuta las instrucciones para dibujar imágenes. Hace cálculos rápidos para renderizar gráficos.
* Drivers: Son los "traductores" que permiten que el sistema operativo y OpenGL hablen con la GPU.
Sin drivers actualizados, OpenGL no puede usar todo el poder de la GPU.
## ¿Por qué es necesario activar el VSync? ¿Qué pasa si no lo activas?
VSync sincroniza el refresco de OpenGL con el refresco del monitor:
* Si no activas VSync y la imagen es estática, puede no notarse mucho.
* Si la imagen es dinámica (moviéndose), puede aparecer tearing: franjas donde partes de diferentes frames se ven mezcladas.
Activar VSync hace que la animación sea más fluida y limpia.
## ¿Qué es OpenGL Legacy y qué diferencias hay con OpenGL moderno?
* OpenGL Legacy: Era el estilo antiguo, donde OpenGL traía por defecto shaders, iluminación y cámara. Usabas funciones como glBegin(), glVertex3f(), etc. Todo era más sencillo pero menos flexible.
* OpenGL Moderno: Nos obliga a usar shaders personalizados y gestionar toda la memoria y pipeline manualmente. Es más complejo, pero más poderoso.
## ¿Qué es el shader program y por qué es importante en OpenGL moderno?
Un shader program es un programa pequeño que corre en la GPU.
Se compone de al menos un vertex shader (maneja vértices) y un fragment shader (maneja colores y píxeles).
Es fundamental porque define cómo se procesa y se dibuja todo en la pantalla.
Sin shaders, OpenGL moderno no puede dibujar nada.
## ¿Qué intuyes que hace setupTriangle()? ¿Qué es el VAO y el VBO?
### setupTriangle():
* Crea y llena el VBO (Vertex Buffer Object) con los datos de los vértices del triángulo.
* Configura el VAO (Vertex Array Object) que guarda cómo leer esos vértices.
VBO → Guarda datos de vértices.
VAO → Guarda la configuración de cómo interpretar esos datos (qué atributo es posición, etc.).
## En el ciclo principal, ¿es necesario volver a indicar shader program y VAO en cada frame?
No estrictamente, si no cambias de shader ni de VAO.
Pero es buena práctica:
Permite cambiar de shader o VAO en mitad del programa (por ejemplo, para dibujar diferentes objetos con diferentes shaders).
Facilita el manejo cuando la escena es más compleja.
## ¿Por qué es importante glfwSwapBuffers(mainWindow)? ¿Qué pasa si no lo llamas?
Importante porque intercambia el buffer donde se dibujó con el que se muestra.
Sin glfwSwapBuffers(), el usuario no vería los dibujos nuevos.
La pantalla quedaría congelada o se vería vacía.
