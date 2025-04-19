# Primer Programa en Assembly 

**Explicacion**
Solo tuve cambiar los valores del @ por 60 y 9 y la direccion de salto que modificaba el PC la cambie de  6 a 0. 

``` asm
@60 
D=A 
@9 
D=D+A 
@6 
M=D 
@0
0;JMP 
```

