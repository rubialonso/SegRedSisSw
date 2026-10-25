### Descripción

Can you decrypt this message using this key "CYLAB"?

Archivo adjunto (`cipher.txt`):

```
caldfow{O0NU_WQ3_G1G3O3T3_A1AH3S_a0393cd7}
```

### Solución

1. El texto cifrado tiene formato `caldfow{...}`, muy parecido a `academy{...}`, lo que sugiere un cifrado por sustitución polialfabética (Vigenère) sobre el prefijo del flag.
2. Se escribe un script en Python que implementa el descifrado de Vigenère (resta el valor numérico de la letra de la clave, módulo 26, dejando intactos los caracteres no alfabéticos como `_`, `{`, `}` y dígitos):

```python
def vig_decrypt(cipher, key):
    key = key.lower()
    res = []
    ki = 0
    for ch in cipher:
        if ch.isalpha():
            k = ord(key[ki % len(key)]) - ord('a')
            base = ord('A') if ch.isupper() else ord('a')
            c = (ord(ch) - base - k) % 26
            res.append(chr(c + base))
            ki += 1
        else:
            res.append(ch)
    return ''.join(res)

print(vig_decrypt("caldfow{O0NU_WQ3_G1G3O3T3_A1AH3S_a0393cd7}", "CYLAB"))
```

3. Al aplicar la clave `CYLAB`, el prefijo `caldfow` se convierte correctamente en `academy`, confirmando la clave.

```
~/cylab/crypto
➜ python3 vigenere.py
academy{D0NT_US3_V1G3N3R3_C1PH3R_y0393es7}
```

Flag: `academy{D0NT_US3_V1G3N3R3_C1PH3R_y0393es7}`

### Notas Adicionales

El mensaje descifrado ("Don't use Vigenère cipher") hace referencia a que el cifrado de Vigenère es inseguro frente a ataques de criptoanálisis de frecuencias (test de Kasiski / índice de coincidencia), ya que es una sustitución polialfabética periódica.

### Referencias

- [Vigenère cipher - Wikipedia](https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher)