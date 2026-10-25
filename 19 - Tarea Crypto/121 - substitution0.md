### Descripción

A message has come in but it seems to be all scrambled. Luckily it seems to have the key at the beginning. Can you crack this substitution cipher?

Archivo adjunto (`message_2.txt`), primera línea = alfabeto cifrado (clave):

```
KCXZUNDAOYVRHWLGFSIMQPTEBJ

Ausuqglw Rudskwz ksliu, toma k dskpu kwz imkmurb kos, kwz cslqdam hu mau cuumru
nslh k drkii xkiu ow taoxa om tki uwxrliuz. ...
```

### Solución

1. La primera línea del archivo es la clave: indica, para cada letra del alfabeto en orden (A, B, C, ..., Z), con qué letra fue sustituida en el texto cifrado (p. ej. A→K, B→C, C→X, ...).
2. Se construye el mapeo inverso (cifrado → texto plano) y se aplica a todo el cuerpo del mensaje, preservando mayúsculas/minúsculas y dejando sin cambios los caracteres no alfabéticos:

```python
import string
alphabet = string.ascii_uppercase
key_line = "KCXZUNDAOYVRHWLGFSIMQPTEBJ"
enc_map = {alphabet[i]: key_line[i] for i in range(26)}
dec_map = {v: k for k, v in enc_map.items()}

def decrypt(ch):
    if ch.isalpha():
        p = dec_map[ch.upper()]
        return p.lower() if ch.islower() else p
    return ch
```

3. El texto descifrado resulta ser un fragmento de "El escarabajo de oro" (The Gold-Bug) de Edgar Allan Poe:

```
Hereupon Legrand arose, with a grave and stately air, and brought me the beetle
from a glass case in which it was enclosed...

The flag is: academy{5UB5717U710N_3V0LU710N_1DDF0D6C}
```

Flag: `academy{5UB5717U710N_3V0LU710N_1DDF0D6C}`

### Notas Adicionales

Al dar explícitamente el alfabeto de sustitución, este reto no requiere criptoanálisis de frecuencias: basta con invertir la tabla de sustitución dada.

### Referencias

- [The Gold-Bug - Edgar Allan Poe (Wikipedia)](https://en.wikipedia.org/wiki/The_Gold-Bug)
- [Substitution cipher - Wikipedia](https://en.wikipedia.org/wiki/Substitution_cipher)