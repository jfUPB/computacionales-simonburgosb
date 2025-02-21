# Ciclo de suma

``` asm
@1 
M=A 
D=M 
@12 
M=0 
@5 
D=D-A 
@17 
D;JGE 
@1 
D=M 
@12
M=D+M 
@1 
M=D+M 
@5 
0;JMP 
@17 
0;JMP 
```

![Texto alternativo](../../../../assets/act9_1.png)
