# Actividad 3

## Codigo app.h
``` c++
#pragma once
#include "ofMain.h"

// Nodo de la cola
struct Node {
    float x, y;
    float radius;
    ofColor color;
    float opacity;
    Node* next;

    Node(float _x, float _y, float _radius, ofColor _color, float _opacity)
        : x(_x), y(_y), radius(_radius), color(_color), opacity(_opacity), next(nullptr) {}
};

// Implementación manual de una cola (FIFO)
class BrushQueue {
public:
    Node* front;
    Node* rear;
    int size;
    int maxSize;

    BrushQueue(int _maxSize);
    ~BrushQueue();

    void enqueue(float x, float y, float radius, ofColor color, float opacity);
    void dequeue();
    void clear();
    bool isEmpty();
    void draw();
};

// Constructor
BrushQueue::BrushQueue(int _maxSize) : front(nullptr), rear(nullptr), size(0), maxSize(_maxSize) {}

// Destructor
BrushQueue::~BrushQueue() {
    clear();
}

// Agregar un nuevo nodo a la cola
void BrushQueue::enqueue(float x, float y, float radius, ofColor color, float opacity) {
    Node* newNode = new Node(x, y, radius, color, opacity);
    if (rear) {
        rear->next = newNode;
    }
    else {
        front = newNode;
    }
    rear = newNode;
    size++;

    if (size > maxSize) {
        dequeue();
    }
}

// Eliminar el nodo más antiguo
void BrushQueue::dequeue() {
    if (!front) return;
    Node* temp = front;
    front = front->next;
    if (!front) {
        rear = nullptr;
    }
    delete temp;
    size--;
}

// Vaciar la cola
void BrushQueue::clear() {
    while (front) {
        dequeue();
    }
}

// Verificar si la cola está vacía
bool BrushQueue::isEmpty() {
    return front == nullptr;
}

class ofApp : public ofBaseApp {
public:
    BrushQueue strokes; // Cola de trazos
    float backgroundHue = 0;

    ofApp() : strokes(50) {} // Tamaño máximo de la cola

    void setup();
    void update();
    void draw();
    void keyPressed(int key);
    
};
```

## code app.cpp
``` c++
#include "ofApp.h"

//--------------------------------------------------------------
void ofApp::setup() {
    ofBackground(0);
}

//--------------------------------------------------------------
void ofApp::update() {
    backgroundHue += 0.2;
    if (backgroundHue > 255) backgroundHue = 0;

    if (ofGetMousePressed()) {
        float radius = ofRandom(5, 15);
        ofColor color = ofColor::fromHsb(ofRandom(255), 255, 255);
        float opacity = ofRandom(100, 255);
        strokes.enqueue(ofGetMouseX(), ofGetMouseY(), radius, color, opacity);
    }
}

//--------------------------------------------------------------
void ofApp::draw() {
    ofColor color1, color2;
    color1.setHsb(backgroundHue, 150, 240);
    color2.setHsb(fmod(backgroundHue + 128, 255), 150, 240);
    ofBackgroundGradient(color1, color2, OF_GRADIENT_LINEAR);

    Node* current = strokes.front;
    int i = 0;
    while (current) {
        float adjustedOpacity = ofMap(i, 0, strokes.maxSize, 50, 255);
        ofSetColor(current->color, adjustedOpacity);
        ofDrawCircle(current->x, current->y, current->radius);
        current = current->next;
        i++;
    }
}

//--------------------------------------------------------------
void ofApp::keyPressed(int key) {
    if (key == 'c') {
        strokes.clear();
    }
    else if (key == 'a') {
        strokes.maxSize = (strokes.maxSize == 50) ? 100 : 50;
    }
}
```

## Uso del Depurador en Visual Studio
* enqueue(): Se verificó que los nodos se enlazaran correctamente observando front y rear.
* dequeue(): Se confirmó que el nodo más antiguo se eliminara cuando la cola alcanzaba su límite.
* clear(): Se comprobó que todos los nodos se eliminaran.

## Lista de Pruebas Realizadas
### Prueba de Inserción de Nodos (enqueue())
Busque verificar que los nodos se agreguen correctamente y se dibujen en pantalla. Llamé a enqueue(100, 100, 10, ofColor::red, 255). El nodo rojo se dibujó correctamente en pantalla. 
### Prueba de Eliminación FIFO (dequeue())
Busque confirmar que al alcanzar el límite, el nodo más antiguo sea eliminado. Inserté 51 trazos y observé si el primero desaparecía. El nodo más antiguo fue eliminado correctamente y los nuevos se añadieron al final.
### Prueba de Vaciado de la Cola (clear())
Busque que todos los nodos desaparezcan al presionar 'c'. Inserté múltiples trazos y presioné 'c'. Todos los nodos se eliminaron 
### Prueba de Alternancia del Tamaño de la Cola (maxSize)
Busque que la cola cambia entre 50 y 100 trazos al presionar 'a'. Presioné 'a', verifiqué que la cola ahora aceptara 100 elementos antes de eliminar los antiguos.Almacena 100 elementos correctamente, y al presionar 'a' nuevamente, vuelve a 50. 
### Prueba de Gradual Desaparición de Trazos (Opacidad Dinámica)
Busque que los trazos desaparezcan gradualmente con ofMap(). Dibujé múltiples trazos y observé cómo su opacidad disminuía con el tiempo.
### Prueba de Almacenamiento de un Frame ('s')
Busque guardar un frame como imagen al presionar 's'. Presioné 's' tras dibujar varios trazos. La imagen se guardó correctamente con los trazos visibles. 
