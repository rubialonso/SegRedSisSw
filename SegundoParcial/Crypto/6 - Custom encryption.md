### Descripción

Can you get sense of this code file and write the function that will decode the given encrypted file content. Find the encrypted file here (`flag_info` / `enc_flag`) and code file (`custom_encryption.py`).

_by NGIRIMANA Schadrack · picoCTF 2024_

### Solución

1. Se descargan `enc_flag` y `custom_encryption.py` con la terminal web.
2. `enc_flag` resulta ser la salida de consola ya capturada de una ejecución del script (no el ciphertext puro), y contiene directamente los valores de los secretos efímeros `a` y `b` del intercambio tipo Diffie-Hellman, además del arreglo de enteros `cipher`:

```
a = 87
b = 22
cipher is: [...]
```

3. El código fuente de `custom_encryption.py` revela un esquema en capas:

```python
def generator(g, x, p):
    return pow(g, x) % p

def encrypt(plaintext, key):
    cipher = []
    for char in plaintext:
        cipher.append(((ord(char) * key * 311)))
    return cipher

def dynamic_xor_encrypt(plaintext, text_key):
    cipher_text = ""
    key_length = len(text_key)
    for i, char in enumerate(plaintext[::-1]):     # ¡el texto se invierte antes del XOR!
        key_char = text_key[i % key_length]
        encrypted_char = chr(ord(char) ^ ord(key_char))
        cipher_text += encrypted_char
    return cipher_text

def test(plain_text, text_key):
    p = 97
    g = 31
    a = randint(p - 10, p)
    b = randint(p - 10, g)
    u = generator(g, a, p)     # A = g^a mod p
    v = generator(g, b, p)     # B = g^b mod p
    key = generator(v, a, p)   # shared = B^a mod p
    b_key = generator(u, b, p) # shared = A^b mod p  (verificación)
    shared_key = key if key == b_key else None

    semi_cipher = dynamic_xor_encrypt(plain_text, text_key)   # XOR con clave de texto fija "trudeau"
    cipher = encrypt(semi_cipher, shared_key)                  # multiplicación por shared_key*311
    print(f'cipher is: {cipher}')

if __name__ == "__main__":
    message = sys.argv[1]
    test(message, "trudeau")
```

4. Para descifrar hay que invertir las dos capas **en orden opuesto** al cifrado: primero deshacer la multiplicación por `shared_key * 311` para recuperar los códigos ASCII del `semi_cipher`, y luego deshacer el XOR con la clave `"trudeau"` (recordando que el texto original estaba invertido):

```python
import re

text = open('enc_flag').read()
a = int(re.search(r'a = (\d+)', text).group(1))
b = int(re.search(r'b = (\d+)', text).group(1))
cipher = eval(re.search(r'cipher is: (\[.*\])', text).group(1))

p, g = 97, 31
u = pow(g, a) % p
v = pow(g, b) % p
shared_key = pow(v, a) % p   # = pow(u, b) % p

semi_cipher = ''.join(chr(c // (shared_key * 311)) for c in cipher)

text_key = "trudeau"
plain_rev = ''.join(
    chr(ord(ch) ^ ord(text_key[i % len(text_key)]))
    for i, ch in enumerate(semi_cipher)
)
flag = plain_rev[::-1]   # se revierte de nuevo para deshacer plaintext[::-1]
print(flag)
```

5. Resultado: `academy{custom_d2cr0pt6d_b1f6d02d}`

Flag: academy{custom_d2cr0pt6d_b1f6d02d}

### Notas Adicionales

El punto más sutil del reto es el orden de las transformaciones: el cifrado aplica primero el XOR (sobre el texto invertido) y después la multiplicación, por lo que al descifrar hay que revertir ambas capas en el orden contrario. Además, `enc_flag` no es un volcado "limpio" del ciphertext sino literalmente la salida de `print()` del programa, lo que convenientemente filtra los secretos `a` y `b` usados para derivar la clave compartida, evitando tener que atacar el logaritmo discreto.

### Referencias