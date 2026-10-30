### Descripción

A new modular challenge! Download the message here (`mod2_message.txt`).

Take each number mod 41 and find the modular inverse for the result. Then map to the following character set: 1-26 are the alphabet, 27-36 are the decimal digits, and 37 is an underscore.

Wrap your decrypted message in the academy flag format (i.e. `academy{decrypted_message}`).

_by Will Hong · picoCTF 2022_

### Solución

1. Se descarga `mod2_message.txt` con la terminal web integrada de la plataforma, obteniendo una lista de números separados por espacios.
2. El enunciado describe exactamente el algoritmo inverso a aplicar sobre cada número `n` del mensaje:
    - Reducir `n mod 41`.
    - Calcular el inverso modular de ese resultado respecto a 41.
    - Traducir el inverso (un valor entre 1 y 40) al alfabeto indicado: 1-26 → `a`-`z`, 27-36 → `0`-`9`, 37 → `_`.
3. Se automatiza con Python usando `pow(x, -1, 41)` (inverso modular nativo de Python ≥3.8):

```python
nums = [int(x) for x in open('mod2_message.txt').read().split()]

def charmap(v):
    if 1 <= v <= 26:
        return chr(ord('a') + v - 1)
    if 27 <= v <= 36:
        return str(v - 27)
    if v == 37:
        return '_'
    return '?'

out = ''
for n in nums:
    r = n % 41
    inv = pow(r, -1, 41)
    out += charmap(inv)
print(out)
```

4. Resultado: `1nv3r53ly_h4rd_950d690f`

Flag: academy{1nv3r53ly_h4rd_950d690f}

### Notas Adicionales

El reto es un ejercicio directo de aritmética modular: dado que el cifrado multiplicó cada carácter por un valor fijo módulo 41 (un primo, por lo que todo elemento no nulo tiene inverso), basta con invertir esa multiplicación calculando el inverso modular de cada número recibido.

### Referencias