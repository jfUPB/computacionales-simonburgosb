# ACTIVIDAD 6:

## Patrón Observer en mi proyecto:
### ¿En qué parte específica de tu código implementaste el rol de Sujeto (Subject)?

El rol de Sujeto es implementado en la clase Garden. El método notify se encarga de enviar los eventos a todos los observadores registrados.
void Garden::reactToKey(char key) {
    if (key == 'a') notify("agitate");
    else if (key == 's') notify("sleep");
    else if (key == 'h') notify("happy");
}

### ¿Qué clase(s) implementaron el rol de Observador (Observer)?
Las criaturas, que son instancias de LightCreature, implementan el rol de Observador. La clase LightCreature tiene el método onNotify para reaccionar a los eventos que le envía el Sujeto.

void LightCreature::onNotify(const std::string& event) {
    if (event == "agitate") {
        setState(new AgitatedState());
    } else if (event == "sleep") {
        setState(new SleepState());
    } else if (event == "happy") {
        setState(new HappyState());
    }
}

### ¿Qué eventos concretos notificaba tu Sujeto?
Los eventos notificados por el Sujeto (Garden) son "agitate", "sleep", y "happy". Estos eventos cambian el estado de las criaturas.

### ¿En qué parte de tu código se utiliza el patrón (es decir, dónde se llama a notify y dónde reaccionan los observadores)?
El patrón se usa en el método reactToKey de Garden, que notifica a los observadores al llamar a notify. Las criaturas reaccionan a estos eventos mediante el método onNotify.

void Garden::reactToKey(char key) {
    if (key == 'a') notify("agitate");
    else if (key == 's') notify("sleep");
    else if (key == 'h') notify("happy");
}

## Patrón Factory Method en mi proyecto:

### ¿Dónde está definido tu método factory?
El método createCreature está definido en la clase CreatureFactory. Este método crea nuevas instancias de LightCreature.

LightCreature* CreatureFactory::createCreature(const std::string& type, float x, float y) {
    LightCreature* creature = new LightCreature(x, y);
    if (type == "agitated") {
        creature->setState(new AgitatedState());
    } else if (type == "sleep") {
        creature->setState(new SleepState());
    } else {
        creature->setState(new HappyState());
    }
    return creature;
}

### ¿Qué tipos específicos de objetos creaba tu factory?
La fábrica crea objetos de la clase LightCreature con diferentes estados iniciales como "agitated", "sleep", o "happy".

### ¿Por qué fue beneficioso usar una factory en esa parte de tu código?
Usar una factory permite centralizar la creación de LightCreature, lo que ayuda a evitar la duplicación de lógica de creación de criaturas en diferentes partes del código. Esto desacopla la creación de objetos del código que los utiliza, facilitando la modificación y extensión del comportamiento de las criaturas sin tener que modificar el código cliente.

### Muestra un ejemplo de cómo usaste una factory en tu código cliente (ej. en setup o en respuesta a un evento).
En el método setup de ofApp, se utiliza la fábrica para crear criaturas con el estado inicial "happy":

void ofApp::setup() {
    for (int i = 0; i < 20; ++i) {
        LightCreature* creature = CreatureFactory::createCreature("happy", ofRandomWidth(), ofRandomHeight());
        garden.addObserver(creature);
        creatures.push_back(creature);
    }
}

## Patrón State en mi proyecto:
### ¿Qué clase actuó como Contexto (la que tiene un estado)?
La clase LightCreature actúa como el contexto. Mantiene una referencia al estado actual mediante un puntero a la clase State.

void LightCreature::setState(State* newState) {
    if (state) state->onExit(*this);
    delete state;
    state = newState;
    if (state) state->onEnter(*this);
}

### ¿Cuáles fueron los ConcreteStates que implementaste?
Implementé tres estados concretos: HappyState, AgitatedState y SleepState. Cada uno de estos estados tiene un comportamiento diferente para la criatura.

void HappyState::update(LightCreature& creature) {
    creature.color = ofColor::fromHsb(ofRandom(255), 180, 255);
    creature.radius = 15 + 3 * sin(ofGetElapsedTimef() * 2);
}

void AgitatedState::update(LightCreature& creature) {
    creature.pos.x += ofRandom(-5, 5);
    creature.pos.y += ofRandom(-5, 5);
    creature.color = ofColor::red;
}

### ¿Qué desencadenaba las transiciones entre estados en tu aplicación?
Las transiciones entre estados se desencadenan por los eventos notificados por el Garden. Cuando el Garden recibe una tecla ('a', 's', 'h'), notifica a las criaturas para que cambien de estado.

void LightCreature::onNotify(const std::string& event) {
    if (event == "agitate") {
        setState(new AgitatedState());
    } else if (event == "sleep") {
        setState(new SleepState());
    } else if (event == "happy") {
        setState(new HappyState());
    }
}

### ¿Por qué decidiste que el patrón State era apropiado para gestionar el comportamiento de esa clase en particular?
El patrón State es apropiado para gestionar el comportamiento de LightCreature porque su comportamiento cambia dependiendo de su estado (feliz, agitado, dormido). Este patrón permite encapsular estos comportamientos y facilita la adición de nuevos estados en el futuro sin tener que modificar el código existente. Alternativamente, se podría haber usado un enfoque basado en una máquina de estados, pero el patrón State proporciona una solución más modular y flexible.

## Definiciones Post-Experiencia:
* ¿Qué es una clase? Una clase es una plantilla o definición que establece cómo se deben crear los objetos. Define los atributos y comportamientos comunes para los objetos de ese tipo.
* ¿Qué es un objeto? Un objeto es una instancia concreta de una clase. Es una entidad con atributos específicos y puede ejecutar los métodos definidos en su clase.

## Beneficios Estructurales:
Los tres patrones (Observer, Factory y State) han mejorado la estructura de mi proyecto al hacerlo más modular, flexible y fácil de mantener. La separación de responsabilidades (como la notificación de eventos, la creación de objetos y la gestión de estados) facilita la extensión y el entendimiento del código.
