# Codigos de  los conceptos 

## Codigo en c# 

``` c#
using System;

class Program
{
    static void Main()
    {
        // Ejemplo de Condicional
        int x = 5;
        if (x > 10)
        {
            Console.WriteLine(1);
        }
        else
        {
            Console.WriteLine(0);
        }

        // Ejemplo de Ciclo While
        int contador = 3;
        while (contador > 0)
        {
            Console.WriteLine(contador);
            contador--;
        }

        // Ejemplo de Ciclo For
        for (int i = 0; i < 4; i++)
        {
            Console.WriteLine(1);
        }

      
        // Llamado a función con parámetros (suma)
        int resultadoSuma = Sumar(3, 7);
        Console.WriteLine(resultadoSuma);

        // Llamado a función con retorno (multiplicación por sumas repetidas)
        int resultadoMult = Multiplicar(4, 6);
        Console.WriteLine(resultadoMult);
       escribirVariablesP();
       leerPunteros();
       manipularArreglos();
    }

    static int Sumar(int a, int b)
    {
        return a + b;
    }

    static int Multiplicar(int c, int d)
    {
        int resultado = 0;
        while (d > 0)
        {
            resultado += c;
            d--;
        }
        return resultado;
    }
// Escritura de variable por punteros
        static void escribirVariablesP()
        {
            int var = 42;
            int* ptr = &var;
            *ptr = 42;
        }

        // Lectura de variable por punteros
        static void leerPunteros()
        {
            int var = 42;
            int* ptr = &var;
            Console.WriteLine(*ptr);
        }

```

## codigo en asm
``` asm
//Ejemplo condicional
@5
D=A
@16
M=D
@16
D=M
@10
D=D-A
@13
D;JGT
@17
0;JMP
@16384
M=1
@20
0;JMP
@16384
M=0

//Ejemplo ciclo while
@3
D=A 
@16 
M=D 
@16 
D=M 
@16 
D;JLE 
@16 
D=M 
@16384 
M=D 
@16 
M=M-1 
@4 
0;JMP 

//Ejemplo ciclo for
@0 
D=A 
@16 
M=D 
@4 
D=A 
@17 
M=D 
@16 
D=M 
@17 
D=M-D 
@23 
D;JLE 
@16 
D=M 
@16384 
A=D+A 
M=1 
@16 
M=M+1 
@8 
0;JMP

//Escritura de variables por medio de punteros
@42
D=A
@16
M=D

//Lectura de variables por medio de punteros
@16
D=M
@16384
M=D

//Manipulación de un arreglo por medio de punteros.
@100  
D=A
@17
M=D 
@0
D=A
@18
M=D  
@5
D=A
@18
D=M-D
@29
D;JGE  
@17
D=M
@18
A=D+M  
D=M
D=D+1  
@17
D=M
@18
A=D+M  
M=D  
@18
M=M+1  
@8
0;JMP


//Llamado a funciones con parámetros.
@3
D=A
@16
M=D
@7
D=A
@17
M=D
@16
D=M
@17
D=D+M
@16384
M=D

//Llamado a funciones con retorno de parámetros
@4
D=A
@16
M=D  
@6
D=A
@17
M=D  
@0
D=A
@18
M=D  
@17
D=M
@24
D;JLE 
@16
D=M
@18
M=D+M  
@17
M=M-1  
@12
0;JMP
@18
D=M
@16384
M=D 

```
