### Descripción
  Run the Python script `code.py` in the same directory as `codebook.txt`.
  Hints
1. On the webshell, use `ls` to see if both files are in the directory you are in
2. The `str_xor` function does not need to be reverse engineered for this challenge.
### Solución
```
~ via 🐍 v3.13.5 
➜ cd cylab

~/cylab via 🐍 v3.13.5 
➜ ls
codebook.txt  code.py

~/cylab via 🐍 v3.13.5 
➜ cat codebook.txt
azbycxdwevfugthsirjqkplomn

~/cylab via 🐍 v3.13.5 
➜ python code.py
picoCTF{c0d3b00k_455157_d9aa2df2}
```

**Flag**: picoCTF{c0d3b00k_455157_d9aa2df2}
### Notas Adicionales

### Ejemplo 
```python
def str_xor(data: str, key: str) -> str:
    return ''.join(
        chr(ord(c) ^ ord(key[i % len(key)]))
        for i, c in enumerate(data)
    )
```

**Cómo funciona paso a paso:**

1. `ord(c)` convierte cada carácter en su valor numérico (código ASCII/Unicode).
2. Se aplica `^` (operador XOR de Python) entre el carácter del dato y el carácter correspondiente de la clave.
3. `chr(...)` convierte el resultado numérico de vuelta a carácter.
4. `i % len(key)` hace que la clave se repita si es más corta que el texto.

### Propiedad clave de XOR

XOR es **reversible**: si aplicas la misma operación dos veces con la misma clave, recuperas el dato original.

python

```python
mensaje = "Hola"
clave = "k"

cifrado = str_xor(mensaje, clave)      # cifra
original = str_xor(cifrado, clave)     # descifra (vuelve a "Hola")
```

Esto la hace popular para cifrados simples y reversibles, pero **no es segura criptográficamente** para proteger información sensible: es vulnerable a análisis de frecuencia y ataques si la clave se reutiliza o es corta
### Referencias