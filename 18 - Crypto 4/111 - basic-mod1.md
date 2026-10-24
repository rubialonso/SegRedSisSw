### Descripción

We found this weird message being passed around on the servers, we think we have a working decryption scheme. Download the message here ([message.txt](https://challenge-files.cylabacademy.net/library/f3895827512c6fab64095a69942e62ba9e367bb32d70ff69dc0e8fd9a826936a/message.txt)). Take each number mod 37 and map it to the following character set: 0-25 is the alphabet (uppercase), 26-35 are the decimal digits, and 36 is an underscore. Wrap your decrypted message in the academy flag format (i.e. academy{decrypted_message}).

### Solución

1. El archivo contiene una lista de números separados por espacio:

```
   313 396 353 161 336 73 198 406 202 285 57 346 151 332 328 216 214 70 286 360 72 216
```

2. Se aplica literalmente la regla indicada por el enunciado: cada número mod 37, mapeado a un charset de 37 símbolos (A-Z, luego 0-9, luego `_`):

```python
   nums = "313 396 353 161 336 73 198 406 202 285 57 346 151 332 328 216 214 70 286 360 72 216".split()
   charset = [chr(ord('A')+i) for i in range(26)] + [str(i) for i in range(10)] + ['_']
   out = ''.join(charset[int(n) % 37] for n in nums)
   print("academy{" + out + "}")
```

3. Resultado: `R0UND_N_R0UND_65371195`.

**Flag:** `academy{R0UND_N_R0UND_65371195}`

### Notas Adicionales

No hace falta ninguna herramienta extra: el propio enunciado da la "clave" de descifrado completa (operación mod 37 + tabla de caracteres), solo hay que implementarla tal cual.

### Referencias