### Descripción

We have recovered a binary and a text file. Can you reverse the flag.

Hint: objdump and Gihdra are some tools that could assist with this

### Solución

1. Descargar el binario `rev` y el archivo de texto `rev_this` desde los enlaces del reto.
2. Revisar el archivo de texto, que contiene el "cifrado" de la flag (24 bytes, sin salto de línea):

```
$ xxd rev_this
00000000: 6163 6164 656d 797b 7731 7b31 7771 3833  academ{w1{1wq83
00000010: 3b34 3c31 685f 367d                      ;4<1h_6}
```

Es decir: `academy{w1{1wq83;4<1h_6}` 3. Desensamblar `main` con `objdump -d -M intel rev` (el binario no está "stripped", así que los símbolos están disponibles). Se observa que el programa:

- Abre dos archivos con `fopen` (uno para lectura, otro para escritura) y lee 24 bytes del primero a un buffer local.
- En un primer bucle escribe sin modificar los primeros 8 bytes del buffer (índices 0–7) al archivo de salida con `fputc`.
- En un segundo bucle, para los índices 8 a 22 (15 bytes), aplica una transformación según la paridad del índice `i`:
    - si `i` es par: `output = input + 5`
    - si `i` es impar: `output = input - 2`
- El último byte (índice 23) se escribe también sin modificar.

4. Como el texto que tenemos (`rev_this`) es justamente la salida (el cifrado) de ese programa, para recuperar la flag original hay que invertir la transformación en los índices 8–22:
    - si `i` es par: `original = cifrado - 5`
    - si `i` es impar: `original = cifrado + 2`
    - los índices 0–7 y 23 quedan igual.
5. Se automatiza la inversión con un pequeño script en Python dentro del servidor:

```
$ python3 -c "
c=open('rev_this','rb').read()
out=bytearray(c)
for i in range(8,23):
    if i%2==0: out[i]=(c[i]-5)%256
    else: out[i]=(c[i]+2)%256
print(out.decode())
"
academy{r3v3rs356673ca1}
```

**Flag**: academy{r3v3rs356673ca1}

### Notas Adicionales

El binario no estaba "stripped", por lo que los nombres de las variables/funciones y la lógica del bucle de cifrado se pudieron leer directamente con `objdump`, sin necesidad de Ghidra, aunque también es una excelente opción (como sugiere la pista) para visualizar el pseudocódigo de forma más cómoda.

### Referencias