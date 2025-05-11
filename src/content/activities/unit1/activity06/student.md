# Manejo basico de la memoria

## 1. ¿Qué es el direccionamiento directo? ¿Cómo se usa en el lenguaje ensamblador Hack?

El direccionamiento directo se refiere a acceder directamente a una dirección específica de memoria para leer o escribir datos. En el lenguaje ensamblador Hack, esto se logra cargando primero la dirección deseada en el registro A mediante una A-instruction (@dirección), y luego utilizando una C-instruction para operar sobre la memoria en esa dirección.

## 2. ¿Qué significa M=D en lenguaje ensamblador Hack? ¿Y D=M?

•	M=D: Copia el valor del registro D a la dirección de memoria apuntada por el registro A.
Ejemplo: Si A=3 y D=45, esta instrucción almacenará 45 en RAM[3].

•	D=M: Copia el valor de la dirección de memoria apuntada por A al registro D.
Ejemplo: Si A=7 y RAM[7]=30, esta instrucción cargará 30 en D.

## 3. Explica el concepto de "puntero" en el contexto de la memoria y proporciona un ejemplo sencillo

Un puntero es una dirección de memoria que apunta a otra dirección de memoria. En el contexto del lenguaje ensamblador Hack, un puntero puede ser utilizado para acceder a una ubicación de memoria dinámica o indirectamente, utilizando el valor almacenado en un registro como referencia.

``` asm
@1     
D=M     
A=D     
D=M     
```
