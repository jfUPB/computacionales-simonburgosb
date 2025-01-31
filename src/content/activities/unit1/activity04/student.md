# Profundizacion en ensamblador 

## Instrucciones

### A-instruction (@value)

Su función principal es cargar un valor en el registro A.
•	Este valor puede ser: 
1. Una dirección en la memoria de datos (RAM) o de instrucciones (ROM).
2. Un valor constante que será usado en operaciones posteriores.
3. La dirección de destino para una instrucción de salto.

### C-instruction (dest=comp;jump)

Es la instrucción principal para realizar operaciones. Define: 
1. comp: La operación a realizar (por ejemplo, suma, resta, comparación).
2. dest: Dónde almacenar el resultado (registro A, D o memoria M).
3. jump: Condición para saltar a una dirección previamente almacenada en el registro A.

## Representación binaria

### A-instruction
•	Formato binario: 0 vvvvvvvvvvvvvvv 

### C-instruction
•	Formato binario: 111 a cccc ccdd djjj 

## Ejemplos de instrucciones

### A-instructions
1. @5
Binario: 0000000000000101
Descripción: Carga el valor 5 en el registro A.

2. @100
Binario: 0000000001100100
Descripción: Carga el valor 100 en el registro A, que puede ser usado como dirección de memoria o constante.

3. @7
Binario: 0000 0000 0000 0111
Descripción: Carga el valor 7 en el registro A, que puede ser usado como dirección de memoria o constante.

### C-instructions
1. D=A+1
Binario: 1110110111100000
Descripción: Calcula A + 1 y almacena el resultado en el registro D.

2. M=D|A
Binario: 1111010101001000
Descripción: Realiza una operación OR entre D y A, almacenando el resultado en M (dirección apuntada por A).

3. D;JMP
Binario: 1110001100000001
Descripcion: Realiza un salto a la posicion indica por D
