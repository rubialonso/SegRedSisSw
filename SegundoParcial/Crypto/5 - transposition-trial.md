### Descripción

Our data got corrupted on the way here. Luckily, nothing got replaced, but every block of 3 got scrambled around! The first word seems to be three letters long, maybe you can use that to recover the rest of the message. Download the corrupted message here.

_by Will Hong · picoCTF 2022_

### Solución

1. Se descarga `transp_message.txt`, un texto donde cada bloque consecutivo de 3 caracteres del mensaje original fue permutado internamente (sus 3 caracteres fueron reordenados según una permutación fija, la misma para todos los bloques).
2. Como solo hay `3! = 6` permutaciones posibles de 3 elementos, se prueban las 6 e, usando la pista de que la primera palabra tiene 3 letras (probablemente "the" en inglés, dado el contexto del curso), se identifica cuál permutación produce texto legible al aplicarla a todos los bloques:

```python
from itertools import permutations

cipher = open('transp_message.txt').read().strip()
blocks = [cipher[i:i+3] for i in range(0, len(cipher), 3)]

for perm in permutations(range(3)):
    candidate = ''.join(''.join(b[p] for p in perm) if len(b) == 3 else b for b in blocks)
    if candidate.lower().startswith('the'):
        print(perm, candidate)
```

3. Se encuentra la permutación correcta y se recupera el mensaje completo en texto plano.
4. Resultado: `academy{7R4N5P051N6_15_3XP3N51V3_27F6D45C}`

Flag: academy{7R4N5P051N6_15_3XP3N51V3_27F6D45C}

### Notas Adicionales

Un cifrado de transposición por bloques fijos de tamaño `n` solo tiene `n!` claves posibles, por lo que para `n=3` (6 claves) es trivial de romper por fuerza bruta en cuanto se tiene un fragmento de texto plano conocido (crib) para identificar la permutación correcta automáticamente.

### Referencias

- [Transposition cipher - Wikipedia](https://en.wikipedia.org/wiki/Transposition_cipher)