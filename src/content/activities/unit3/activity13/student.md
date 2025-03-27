# Ejemplos de los codigos 

``` c++
#include <iostream>
#include <string>
using namespace std;

class Cuenta {
private:
    string titular;
    double saldo;
    static int totalCuentas; // Variable estática (compartida entre todas las cuentas)

public:
    // Constructor
    Cuenta(string _titular, double _saldo) : titular(_titular), saldo(_saldo) {
        totalCuentas++;
        cout << "Cuenta creada: " << titular << " con saldo " << saldo << "\n";
    }
    
    // Destructor
    ~Cuenta() {
        totalCuentas--;
        cout << "Cuenta de " << titular << " eliminada.\n";
    }

    // Método para depositar dinero
    void depositar(double cantidad) {
        saldo += cantidad;
    }

    // Método para retirar dinero con paso por referencia
    bool retirar(double cantidad, string& mensaje) {
        if (cantidad > saldo) {
            mensaje = "Fondos insuficientes.";
            return false;
        }
        saldo -= cantidad;
        mensaje = "Retiro exitoso.";
        return true;
    }

    // Método para mostrar saldo
    void mostrarSaldo() {
        cout << "Saldo de " << titular << ": " << saldo << "\n";
    }

    // Método estático
    static int getTotalCuentas() {
        return totalCuentas;
    }
};

// Inicialización de variable estática
int Cuenta::totalCuentas = 0;

int main() {
    // Objeto en el stack
    Cuenta cuenta1("Carlos", 1000);
    cuenta1.mostrarSaldo();
    
    // Objeto en el heap
    Cuenta* cuenta2 = new Cuenta("Ana", 5000);
    cuenta2->mostrarSaldo();
    
    // Prueba de paso por referencia
    string resultado;
    if (cuenta1.retirar(200, resultado)) {
        cout << "Retiro exitoso: " << resultado << "\n";
    } else {
        cout << "Error: " << resultado << "\n";
    }
    cuenta1.mostrarSaldo();

    // Prueba de paso por valor (se crea una copia de cuenta1)
    Cuenta copia = cuenta1;
    copia.mostrarSaldo();
    
    // Uso de punteros
    Cuenta* ptrCuenta = &cuenta1;
    ptrCuenta->depositar(500);
    ptrCuenta->mostrarSaldo();

    cout << "Total de cuentas activas: " << Cuenta::getTotalCuentas() << "\n";
    
    // Liberar memoria del objeto en el heap
    delete cuenta2;
    
    cout << "Total de cuentas activas tras eliminar cuenta2: " << Cuenta::getTotalCuentas() << "\n";
    
    return 0;
}
```
## Explicacion de conceptos

### Clases y objetos:
* Cuenta es una clase que representa una cuenta bancaria con atributos y métodos.
* Se crean objetos cuenta1 y cuenta2 para demostrar su uso.

### Paso de parámetros por valor y por referencia:
* retirar(double cantidad, string& mensaje): usa paso por referencia en mensaje para modificarlo dentro del método.
* copia = cuenta1;: usa paso por valor, creando una copia independiente.

### Constructores y destructores:
* Cuenta(string _titular, double _saldo): constructor que inicializa los atributos.
* ~Cuenta(): destructor que se ejecuta al eliminar una cuenta.

### Métodos y atributos:
* Métodos como depositar(), retirar() y mostrarSaldo().
* Atributo estático totalCuentas compartido entre todas las instancias.

### Objetos en el stack y en el heap:
* Cuenta cuenta1("Carlos", 1000); → Objeto en el stack.
* Cuenta* cuenta2 = new Cuenta("Ana", 5000); → Objeto en el heap (requiere delete para liberar memoria).

### Punteros y referencias:
* Cuenta* ptrCuenta = &cuenta1; → Puntero que apunta a cuenta1.
* ptrCuenta->depositar(500); → Se accede a métodos a través del puntero.

### Variables estáticas:
* static int totalCuentas; cuenta cuántas cuentas existen en el sistema.

## Ubicacion en Memoria

* cuenta1: Stack	
* cuenta2: Heap	
* copia: Stack	
* ptrCuenta: Stack
* mensaje: Stack	
* totalCuentas: Segmento de datos
