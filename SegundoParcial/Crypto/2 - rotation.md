### Descripción

You will find the flag after decrypting this file. Download the encrypted flag here (`rotation_enc.txt`).

_by Loic Shema · picoCTF 2023_

### Solución

1. Se descarga `rotation_enc.txt`, que contiene el texto cifrado: `ikilmug{z0bib1wv_l3kzgxb3l_76m5m998}`.
2. El patrón `ikilmug{...}` sugiere un cifrado César sobre la palabra `academy{...}` (mismo número de letras y misma posición de la llave `{`), por lo que se prueban las 26 rotaciones posibles y se conserva la que produce un prefijo `academy`:

```python
c = 'ikilmug{z0bib1wv_l3kzgxb3l_76m5m998}'
for s in range(26):
    r = ''.join(
        chr((ord(ch) - 97 - s) % 26 + 97) if ch.isalpha() else ch
        for ch in c
    )
    if r.startswith('academy'):
        print(s, r)
```

3. La rotación correcta es `shift = 8`, obteniendo: `academy{r0tation_d3crypt3d_76e5e998}`

Flag: academy{r0tation_d3crypt3d_76e5e998}

### Notas Adicionales

Un cifrado César solo tiene 26 claves posibles, por lo que siempre es trivial de romper por fuerza bruta; basta con reconocer un prefijo o palabra esperada (aquí, `academy{`) para identificar automáticamente la rotación correcta sin inspección manual de las 26 opciones.

### Referencias

- [Caesar cipher - Wikipedia](https://en.wikipedia.org/wiki/Caesar_cipher)