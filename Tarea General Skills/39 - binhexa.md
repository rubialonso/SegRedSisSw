### Descripción
How well can you perfom basic binary operations?
### Solución
Todo lo saque a mano con binario, en la multiplicacion pase a decimal y luego lo regrese a binario, al final use cyberchef para pasarlo a hexadecimal y para comprobar todas las operaciones estaba usando una calculadora.
```
~/cylab via 🐍 v3.13.5 
➜ nc titan.picoctf.net 55552

Welcome to the Binary Challenge!"
Your task is to perform the unique operations in the given order and find the final result in hexadecimal that yields the flag.

Binary Number 1: 10100000
Binary Number 2: 01100110


Question 1/6:
Operation 1: '<<'
Perform a left shift of Binary Number 1 by 1 bits.
Enter the binary result: 101000000
Correct!

Question 2/6:
Operation 2: '&'
Perform the operation on Binary Number 1&2.
Enter the binary result: 00100000
Correct!

Question 3/6:
Operation 3: '|'
Perform the operation on Binary Number 1&2.
Enter the binary result: 11100110
Correct!

Question 4/6:
Operation 4: '>>'
Perform a right shift of Binary Number 2 by 1 bits .
Enter the binary result: 001100110
Incorrect. Try again
Enter the binary result: 00110011    
Correct!

Question 5/6:
Operation 5: '+'
Perform the operation on Binary Number 1&2.
Enter the binary result: 100000110
Correct!

Question 6/6:
Operation 6: '*'
Perform the operation on Binary Number 1&2.
Enter the binary result: 11111111000000
Correct!

Enter the results of the last operation in hexadecimal: 3FC0

Correct answer!
The flag is: picoCTF{b1tw^3se_0p3eR@tI0n_su33essFuL_1367e2c6}
```

**Flag**: picoCTF{b1tw^3se_0p3eR@tI0n_su33essFuL_1367e2c6}
### Notas Adicionales

## 1. Desplazamientos (Shifts)

**Left shift `<<`** — mueve bits a la izquierda, rellena con `0` a la derecha. Los bits que "sobran" por la izquierda se descartan si mantienes un ancho fijo (ej. 8 bits).

```
10100000 << 1  →  01000000   (se pierde el 1 de la izquierda, entra 0 a la derecha)
```

Equivale a multiplicar por 2 (por cada posición desplazada).

**Right shift `>>`** — mueve bits a la derecha, rellena con `0` a la izquierda. El bit de más a la derecha se descarta.

```
01100110 >> 1  →  00110011   (entra 0 a la izquierda, se pierde el bit de la derecha)
```

Equivale a dividir entre 2 (por cada posición desplazada).

> Regla clave: el resultado siempre debe tener el mismo número de bits que el original (rellena con ceros a la izquierda si hace falta).

## 2. Operadores lógicos bit a bit

**AND `&`** — `1` solo si AMBOS bits son `1`.

```
1010
0110
----
0010
```

**OR `|`** — `1` si AL MENOS UNO de los bits es `1`.

```
1010
0110
----
1110
```

**XOR `^`** (por si aparece) — `1` solo si los bits son DIFERENTES.

```
1010
0110
----
1100
```

Tabla rápida:

|A|B|A&B|A\|B|A^B|
|---|---|---|---|---|
|0|0|0|0|0|
|0|1|0|1|1|
|1|0|0|1|1|
|1|1|1|1|0|

## 3. Suma binaria

Se suma columna por columna, de derecha a izquierda, llevando acarreo (carry):

```
0+0 = 0
0+1 = 1
1+0 = 1
1+1 = 0  (carry 1)
1+1+1(carry) = 1  (carry 1)
```

Si sobra un carry al final, se agrega como bit extra a la izquierda (el resultado puede tener un bit más que los operandos).

## 4. Multiplicación binaria

Igual que la multiplicación "larga" decimal, pero con reglas simples (`1×1=1`, todo lo demás `0`).

**Atajo práctico para números grandes:** convertir ambos binarios a decimal, multiplicar en decimal, y convertir el resultado de vuelta a binario.

## 5. Conversión Binario → Decimal

Suma las potencias de 2 donde hay un `1`, empezando desde la derecha en 2⁰:

```
10100000 = 1×128 + 0×64 + 1×32 + 0×16 + 0×8 + 0×4 + 0×2 + 0×1 = 160
```

## 6. Conversión Decimal → Binario

Divide sucesivamente entre 2, anota el residuo (0 o 1) en cada paso, y lee los residuos de abajo hacia arriba.

```
16320 ÷ 2 = 8160  r0
 8160 ÷ 2 = 4080  r0
 ...
    1 ÷ 2 =    0  r1
```

Lee de abajo hacia arriba.

## 7. Conversión a Hexadecimal

**Opción A — división entre 16:** igual que decimal→binario pero dividiendo entre 16. Residuos 10–15 se escriben como A–F (10=A, 11=B, 12=C, 13=D, 14=E, 15=F).

**Opción B — desde binario (más rápida):** agrupa el binario en bloques de 4 bits (de derecha a izquierda, rellenando con ceros a la izquierda si falta), y convierte cada bloque a su dígito hex:

```
0011 1111 1100 0000
  3    F    C    0
→ 3FC0
```
### Referencias
https://gchq.github.io/CyberChef/
https://calculadorasonline.com/calculadora-binaria/
www.ingmecafenix.com/electronica/general/operaciones-con-numeros-binarios/