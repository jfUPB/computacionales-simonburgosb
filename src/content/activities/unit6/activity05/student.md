# ACTIVIDAD 5:

## OFAPP.CPP
``` c++
#include "ofApp.h"

// ---- LightCreature ----
LightCreature::LightCreature(float x, float y) {
    pos.set(x, y);
    radius = ofRandom(10, 20);
    color = ofColor::fromHsb(ofRandom(255), 200, 255);
    setState(new HappyState());
}

void LightCreature::update() {
    if (state) state->update(*this);
}

void LightCreature::draw() {
    ofSetColor(color);
    ofDrawCircle(pos, radius);
}

void LightCreature::onNotify(const std::string& event) {
    if (event == "agitate") {
        setState(new AgitatedState());
    }
    else if (event == "sleep") {
        setState(new SleepState());
    }
    else if (event == "happy") {
        setState(new HappyState());
    }
}

void LightCreature::setState(State* newState) {
    if (state) state->onExit(*this);
    delete state;
    state = newState;
    if (state) state->onEnter(*this);
}

// ---- States ----
void HappyState::update(LightCreature& creature) {
    creature.color = ofColor::fromHsb(ofRandom(255), 180, 255);
    creature.radius = 15 + 3 * sin(ofGetElapsedTimef() * 2);
}

void AgitatedState::update(LightCreature& creature) {
    creature.pos.x += ofRandom(-5, 5);
    creature.pos.y += ofRandom(-5, 5);
    creature.color = ofColor::red;
}

void SleepState::update(LightCreature& creature) {
    creature.radius = 10;
    creature.color = ofColor(100);
}

// ---- Factory ----
LightCreature* CreatureFactory::createCreature(const std::string& type, float x, float y) {
    LightCreature* creature = new LightCreature(x, y);
    if (type == "agitated") {
        creature->setState(new AgitatedState());
    }
    else if (type == "sleep") {
        creature->setState(new SleepState());
    }
    else {
        creature->setState(new HappyState());
    }
    return creature;
}

// ---- Garden ----
void Garden::reactToKey(char key) {
    if (key == 'a') notify("agitate");
    else if (key == 's') notify("sleep");
    else if (key == 'h') notify("happy");
}

// ---- ofApp ----
void ofApp::setup() {
    for (int i = 0; i < 20; ++i) {
        LightCreature* creature = CreatureFactory::createCreature("happy", ofRandomWidth(), ofRandomHeight());
        garden.addObserver(creature);
        creatures.push_back(creature);
    }
}

void ofApp::update() {
    for (auto& c : creatures) c->update();
}

void ofApp::draw() {
    for (auto& c : creatures) c->draw();
}

void ofApp::keyPressed(int key) {
    garden.reactToKey((char)key);
}
```

## OFAPP.H
``` c++
#pragma once
#include "ofMain.h"

// --- Observer Pattern Interfaces ---
class Observer {
public:
    virtual void onNotify(const std::string& event) = 0;
    virtual ~Observer() {}
};

class Subject {
public:
    void addObserver(Observer* obs) {
        observers.push_back(obs);
    }
    void notify(const std::string& event) {
        for (Observer* obs : observers) {
            obs->onNotify(event);
        }
    }
private:
    std::vector<Observer*> observers;
};

// --- State Pattern ---
class LightCreature;

class State {
public:
    virtual void update(LightCreature& creature) = 0;
    virtual void onEnter(LightCreature& creature) {}
    virtual void onExit(LightCreature& creature) {}
    virtual ~State() {}
};

class HappyState : public State {
public:
    void update(LightCreature& creature) override;
};

class AgitatedState : public State {
public:
    void update(LightCreature& creature) override;
};

class SleepState : public State {
public:
    void update(LightCreature& creature) override;
};

// --- LightCreature ---
class LightCreature : public Observer {
public:
    LightCreature(float x, float y);
    void update();
    void draw();
    void onNotify(const std::string& event) override;
    void setState(State* newState);

    ofVec2f pos;
    float radius;
    ofColor color;
private:
    State* state = nullptr;
};

// --- Factory ---
class CreatureFactory {
public:
    static LightCreature* createCreature(const std::string& type, float x, float y);
};

// --- Garden ---
class Garden : public Subject {
public:
    void reactToKey(char key);
};

// --- ofApp ---
class ofApp : public ofBaseApp {
public:
    void setup();
    void update();
    void draw();
    void keyPressed(int key);

    std::vector<LightCreature*> creatures;
    Garden garden;
};
```

## Descripción del proyecto:
El proyecto es una simulación interactiva de un jardín de criaturas de luz, donde cada criatura cambia su comportamiento y apariencia en función de su estado interno (feliz, agitada o dormida). El usuario puede interactuar con las criaturas presionando teclas para activar diferentes estados. El comportamiento de las criaturas varía visualmente, desde cambios en su tamaño y color hasta movimientos aleatorios, creando una atmósfera dinámica y emocional.

## Diseño con patrones:
* Observer: El Garden actúa como el sujeto que notifica a sus observadores (las criaturas). Las criaturas cambian de estado (agitada, dormida o feliz) según los eventos notificados (teclas presionadas). Se probó la notificación asegurando que las criaturas respondan a las teclas de manera esperada.
* Factory Method: La CreatureFactory crea diferentes tipos de criaturas con estados iniciales predefinidos (feliz, agitada, dormida). Se usó este patrón para desacoplar la creación de criaturas y facilitar la expansión futura. Se probó verificando que las criaturas se generaran con los estados correctos.
* State: La clase LightCreature utiliza el patrón State para cambiar su comportamiento según el estado (feliz, agitada o dormida). Los estados encapsulan comportamientos diferentes y gestionan las transiciones entre ellos. Se probó cambiando los estados con las teclas y observando el cambio en el comportamiento.

## Integración y desafíos:
Los tres patrones colaboran en la aplicación de manera integrada: el Observer notifica eventos que cambian el estado de las criaturas a través de State, mientras que Factory se encarga de la creación de las criaturas. La interacción fluye desde el evento (tecla) hasta la actualización del estado y el comportamiento de las criaturas. Los principales desafíos fueron entender cómo gestionar los punteros y organizar la implementación secuencial de los patrones. 
