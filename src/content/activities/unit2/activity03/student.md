# Ciclo For

``` asm
// Inicialización de variables
@sum
M=0     // sum = 0
@i
M=1     // i = 1

(LOOP)
    @i
    D=M     // D = i
    @100
    D=D-A   // D = i - 100
    @END
    D;JGT   // Si i > 100, salir del bucle

    @i
    D=M     // D = i
    @sum
    M=M+D   // sum = sum + i

    @i
    M=M+1   // i = i + 1
    @LOOP
    0;JMP   // Volver a LOOP

(END)
    @END
    0;JMP   // Bucle infinito para detener el programa
```

* El código ensamblador resultante es prácticamente el mismo en ambas versiones.
* La diferencia clave entre while y for en lenguajes de alto nivel (C, Java, etc.) es más sintáctica que funcional. En ensamblador, ambos terminan traduciéndose en un bucle con inicialización, condición, cuerpo y actualización.
