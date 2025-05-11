# Codigo swap
``` cp
// Función que modifica el parámetro pasado por valor
void swapPorValor(int a, int b) {
    cout << "Dentro de swapPorValor, valor inicial de a: " << a << "Dentro de swapPorValor, valor inicial de b: " << b << endl;
    int c = a;
    a = b;
    b = c;
    cout << "Dentro de swapPorValor, valor modificado: " << a << "Dentro de swapPorValor, valor modificado de b: " << b << endl;
}

// Función que modifica el parámetro pasado por referencia
void swapPorReferencia(int& a, int& b) {
    cout << "Dentro de swapPorReferencia, valor inicial de a: " << a << "Dentro de swapPorReferencia, valor inicial de b: " << b << endl;
    int c = a;
    a = b;
    b = c;
    cout << "Dentro de swapPorReferencia, valor modificado a: " << a << " Dentro de swapPorReferencia, valor modificado de b: " << b << endl;
}

// Función que modifica el parámetro utilizando punteros
void swapPorPuntero(int* a, int* b) {
    cout << "Dentro de swapPorPuntero, valor inicial de a: " << *a << "Dentro de swapPorPuntero, valor inicial de b: " << *b << endl;
    int c = *a;
    *a = *b; 
    *b = c;
    cout << "Dentro de swapPorPuntero, valor modificado: " << *a << "Dentro de swapPorPuntero, valor modificado de b: " << *b << endl;
}

int main() {
    int x = 5;
    int y = 10;

    cout << "Valor inicial de x (paso por valor): " << x << endl;
    cout << "Valor inicial de y (paso por valor): " << y << endl;

    cout << "\nLlamando a swapPorValor(x,y)..." << endl;
    swapPorValor(x,y);
    cout << "Después de swapPorValor, valor de x: " << x << endl;
    cout << "Después de swapPorValor, valor de y: " << y << endl;

    cout << "Valor inicial de x (paso por referencia): " << x << endl;
    cout << "Valor inicial de y (paso por referencia): " << y << endl;

    cout << "\nLlamando a swapPorReferencia(x,y)..." << endl;
    swapPorReferencia(x,y);
    cout << "Después de swapPorReferencia, valor de x: " << x << endl;
    cout << "Después de swapPorReferencia, valor de y: " << y << endl;
    x = 5;
    y = 10;

    cout << "Valor inicial de x (paso por puntero): " << x << endl;
    cout << "Valor inicial de y (paso por puntero): " << y << endl;

    cout << "\nLlamando a swapPorPuntero(&x, &y)..." << endl;
    swapPorPuntero(&x,&y);
    cout << "Después de swapPorPuntero, valor de x: " << x << endl;
    cout << "Después de swapPorPuntero, valor de y: " << y << endl;

    return 0;
}
```

¿Por qué la versión de swapPorValor no logra intercambiar los valores de x e y en el main()?
* Porque crea variables temporales dentro de la memoria

¿Cómo y por qué logran las otras dos funciones (por referencia y por puntero) modificar las variables originales?
* Esto lo logran ya que ellas acceceden a la avriables originales una atraves de la direcicon y valo y otra atraves de un "alias" 

¿Cuáles son las ventajas y consideraciones de usar referencias versus punteros en este caso?
* Que estas 2 modifican de manera optima los valores "globales" de las variables ingresadas como parametros. 
