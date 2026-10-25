### Descripción

A type of transposition cipher is the rail fence cipher. Here is one such cipher encrypted using the rail fence with 4 rails. Can you decrypt it? The decoded message names a phrase. Put that phrase, and nothing else, in the academy flag format: `academy{phrase}`.

Archivo adjunto (`message_1.txt`):

```
Ta _7N6DD5hlg:W3D_H3C31N__37Fef sHR053F38N43DA1 i33___NB
```

### Solución

1. Se implementa el algoritmo de descifrado del cifrado de rieles (rail fence) para un número arbitrario de rieles, reconstruyendo el patrón en zigzag y colocando cada carácter del texto cifrado en su posición original:

```python
def rail_decrypt(cipher, rails):
    n = len(cipher)
    pattern, rail, direction = [], 0, 1
    for i in range(n):
        pattern.append(rail)
        rail += direction
        if rail == rails - 1 or rail == 0:
            direction *= -1
    positions = []
    for r in range(rails):
        positions += [i for i in range(n) if pattern[i] == r]
    res = [None]*n
    for pos, ch in zip(positions, cipher):
        res[pos] = ch
    return ''.join(res)
```

2. Se prueba con 4 rieles (como indica el enunciado):

```
~/cylab/crypto
➜ python3 railfence.py
The flag is: WH3R3_D035_7H3_F3NC3_8361N_4ND_3ND_D3AB175F
```

3. Se verifica re-cifrando el mensaje obtenido con 4 rieles y comprobando que reproduce exactamente el texto cifrado original (confirmando que la clave de 4 rieles es correcta).
4. Se extrae la frase pedida (todo lo que sigue a "The flag is: ") y se envuelve en el formato `academy{}`:

Flag: `academy{WH3R3_D035_7H3_F3NC3_8361N_4ND_3ND_D3AB175F}`

### Notas Adicionales

El mensaje en leetspeak se lee como "WHERE DOES THE FENCE BEGIN AND END...", una referencia humorística a la propia naturaleza del cifrado de rieles (rail fence = "cerca" en inglés).

### Referencias

- [Rail fence cipher - Wikipedia](https://en.wikipedia.org/wiki/Rail_fence_cipher)