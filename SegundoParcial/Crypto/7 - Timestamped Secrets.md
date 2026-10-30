### Descripción

Someone encrypted a message using AES in ECB mode but they weren't very careful with their key. Turns out it's derived from something as simple as the current time! Can you uncover the key and decrypt the flag? Download the encrypted message and the encryption script.

_by Yahaya Meddy · picoCTF 2026_

### Solución

1. Se descargan `ts_message.txt` y `ts_encryption.py` con la terminal web.
2. `ts_encryption.py` muestra que la clave AES de 16 bytes se deriva directamente del timestamp Unix en el momento del cifrado:

```python
from hashlib import sha256
import time
from Crypto.Cipher import AES
from Crypto.Util.Padding import pad

def encrypt(plaintext: str, timestamp: int) -> str:
    timestamp = int(time.time())
    key = sha256(str(timestamp).encode()).digest()[:16]
    cipher = AES.new(key, AES.MODE_ECB)
    padded = pad(plaintext.encode(), AES.block_size)
    ciphertext = cipher.encrypt(padded)
    return ciphertext.hex()
```

3. `ts_message.txt` da una pista del momento aproximado del cifrado y el ciphertext en hexadecimal:

```
Hint: The encryption was done around 1790147508 UTC
Ciphertext (hex): 1677f86f41155474ff5233bc79d0ec79ab610074d921fea1140a448f8c8329d9...
```

4. Como la clave depende únicamente de un entero (el timestamp), el espacio de claves es muy pequeño: basta con probar una ventana de tiempo razonable alrededor del valor dado (por ejemplo, ±600 segundos) y, para cada candidato, intentar desencriptar y verificar si el _unpadding_ PKCS#7 es válido (lo que indica, con altísima probabilidad, la clave correcta):

```python
from hashlib import sha256
from Crypto.Cipher import AES
from Crypto.Util.Padding import unpad

ciphertext = bytes.fromhex("1677f86f41155474ff5233bc79d0ec79ab610074d921fea1140a448f8c8329d9...")
hint_ts = 1790147508

for ts in range(hint_ts - 600, hint_ts + 600):
    key = sha256(str(ts).encode()).digest()[:16]
    cipher = AES.new(key, AES.MODE_ECB)
    try:
        pt = unpad(cipher.decrypt(ciphertext), AES.block_size)
        if pt.startswith(b"academy{"):
            print(ts, pt)
            break
    except ValueError:
        continue
```

5. Resultado: `academy{sa3S_sEc9t_65bbf411}`

Flag: academy{sa3S_sEc9t_65bbf411}

### Notas Adicionales

Usar el tiempo actual del sistema como semilla de una clave criptográfica es un error clásico: el timestamp Unix es un número relativamente pequeño y predecible (más aún si se da una pista del rango temporal), por lo que el "espacio de claves" efectivo se reduce a unos pocos miles de posibilidades, completamente viables para un ataque de fuerza bruta.

### Referencias

- [Advanced Encryption Standard - Wikipedia](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)
- [Block cipher mode of operation (ECB) - Wikipedia](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#ECB)