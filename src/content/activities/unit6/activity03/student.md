# ACTIVIDAD 3: 

## Propósito del patrón Factory Method
El patrón Factory Method permite centralizar la creación de objetos y separar ese código del resto de la aplicación. Esto resuelve el problema de tener instancias new repetidas por todo el código. 

## Ventajas de usar ParticleFactory en ofApp::setup
Usar ParticleFactory mejora la organización del código porque ofApp se enfoca solo en usar las partículas, no en configurarlas. Esto respeta el principio de responsabilidad única (SRP), hace el código más legible y permite agregar nuevos tipos de partículas fácilmente sin modificar ofApp. También permite reutilizar la fábrica desde otras partes del programa si fuera necesario.

## Añadir el tipo de partícula black_hole
Para agregar una partícula llamada black_hole, solo debo editar ParticleFactory::createParticle y añadir una condición con sus características (color negro, tamaño grande, velocidad lenta). No es necesario modificar ofApp::setup, simplemente llamo a la fábrica con el nuevo tipo. Esto demuestra la flexibilidad del patrón, ya que permite extender funcionalidades sin tocar el código principal que usa las partículas.

## Implicaciones de que createParticle sea estático
El método estático createParticle es conveniente porque se puede usar sin crear una instancia de ParticleFactory, lo que simplifica su uso. Sin embargo, limita la flexibilidad futura, ya que no permite herencia ni mantener estado interno dentro de la fábrica. Si en el futuro se quisiera tener varias fábricas especializadas, sería mejor convertirlo en un método de instancia.

