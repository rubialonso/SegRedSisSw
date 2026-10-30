### Descripción

Can you abuse the oracle? An attacker was able to intercept communications between a bank and a fintech company. They managed to get the message (ciphertext) and the password that was used to encrypt the message. After some intensive reconnaissance they found out that the bank has an oracle that was used to encrypt the password and can be found here: `nc chatelaine.cylabacademy.net 36378`. Decrypt the password and use it to decrypt the message. The oracle can decrypt anything except the password.

_by Geoffrey Njogu · picoCTF 2024_

### Solución

1. Se lanza la instancia del reto desde la plataforma (botón "Launch Instance"), lo cual expone un servicio accesible por `nc chatelaine.cylabacademy.net <puerto>`, y se descargan dos archivos con la terminal web:
    - `password.enc`: un entero decimal, el ciphertext RSA (`c = password^e mod n`) de la contraseña.
    - `secret.enc`: un archivo binario en formato `Salted__...` de OpenSSL, es decir, el mensaje cifrado simétricamente (AES) usando la contraseña como passphrase.
2. Al conectarse al oráculo (usando un socket de Python desde la terminal web, ya que es un servicio de red real) se descubre un menú simple:

```
***************THE ORACLE***************
what should we do for you?
E --> encrypt D --> decrypt.
```

- `E` pide un texto, lo codifica como un entero `m` (concatenando el valor hexadecimal de cada carácter) y devuelve `ciphertext (m ^ e mod n)`.
- `D` pide un ciphertext y devuelve `decrypted ciphertext as hex (c ^ d mod n): <hex>` — es decir, el oráculo descifra **cualquier** ciphertext que se le entregue y devuelve el resultado en hexadecimal, **excepto** si coincide exactamente con el ciphertext de la contraseña (`password.enc`).

3. Esto es un **ataque de blinding (desenmascaramiento multiplicativo) contra un oráculo de descifrado RSA**, el ejemplo canónico de por qué RSA "de libro de texto" (sin padding aleatorio) no es CPA-seguro: dado el ciphertext objetivo `c = m^e mod n` que el oráculo rechaza descifrar directamente, se elige un factor de cegado conocido `k` y se pide al oráculo:
    - Primero, usando `E`, se cifra un texto corto (por ejemplo, el carácter de código ASCII 2) para obtener `c_k = k^e mod n` con `k` conocido.
    - Luego se calcula `c' = c * c_k` (sin necesidad de reducir módulo `n`: la exponenciación modular del servidor lo hace automáticamente), y se envía a `D`. Como `c' = (m*k)^e mod n`, el oráculo (que no sabe que `c'` "en el fondo" codifica la contraseña) responde con `m' = (m * k) mod n`.
    - Finalmente, como `m` y `k` son pequeños frente a `n`, no hay desbordamiento (`m*k < n`), así que `m = m' // k` es una división entera exacta, sin necesidad siquiera de conocer `n` explícitamente ni calcular un inverso modular.
4. Se automatiza todo el intercambio con un script de Python usando `socket`:

```python
import socket, re

def recvall(s, t=1.5):
    s.settimeout(t)
    chunks = b''
    try:
        while True:
            d = s.recv(65536)
            if not d:
                break
            chunks += d
    except socket.timeout:
        pass
    return chunks

c_password = int(open('password.enc').read().strip())

s = socket.create_connection(("chatelaine.cylabacademy.net", 36378), timeout=10)
recvall(s)
s.sendall(b"E\n")
recvall(s)
s.sendall(b"\x02\n")                       # cifra el valor conocido k = 2
r = recvall(s).decode(errors='replace')
c2 = int(re.findall(r'\d{5,}', r)[-1])      # extrae c_k del texto de respuesta

c_blind = c_password * c2                   # c' = c * c_k  (sin reducir mod n)

s.sendall(b"D\n")
recvall(s)
s.sendall((str(c_blind) + "\n").encode())
r2 = recvall(s).decode(errors='replace')
hx = re.search(r'hex.*?:\s*([0-9a-fA-F]+)', r2).group(1)

m_blind = int(hx, 16)
m_password = m_blind // 2                   # división entera exacta
pw_bytes = m_password.to_bytes((m_password.bit_length() + 7) // 8, 'big')
print(pw_bytes)                             # b'20373'
```

5. Se recupera la contraseña: `20373`.
6. Con la contraseña en mano, se descifra `secret.enc` (formato OpenSSL `Salted__`) usando el esquema de derivación de clave "legacy" (`EVP_BytesToKey`, el método con el que originalmente se cifró el archivo, dado que `-pbkdf2` falla con "bad decrypt"):

```
openssl enc -aes-256-cbc -d -in secret.enc -pass pass:20373
```

7. Resultado: `academy{su((3ss_(r@ck1ng_r3@_20373ec2}`

Flag: academy{su((3ss_(r@ck1ng_r3@_20373ec2}

### Notas Adicionales

Este reto ilustra por qué RSA de libro de texto (sin un esquema de padding aleatorizado como OAEP) no cumple el requisito mínimo de seguridad bajo ataques de texto plano elegido (CPA): la propiedad **multiplicativamente homomórfica** de RSA (`E(m1) * E(m2) = E(m1*m2) mod n`) permite a un atacante, con acceso a un oráculo de descifrado que rechaza solo el ciphertext exacto objetivo, "disfrazar" ese ciphertext multiplicándolo por el cifrado de un valor conocido, pedir al oráculo que lo descifre sin levantar sospechas, y luego deshacer el disfraz dividiendo el resultado. La defensa estándar es usar un esquema de padding con aleatoriedad (OAEP), que rompe la homomorfía multiplicativa.

### Referencias

- [RSA (cryptosystem) - plain RSA security - Wikipedia](https://en.wikipedia.org/wiki/RSA_\(cryptosystem\))
- [Chosen-ciphertext attack - Wikipedia](https://en.wikipedia.org/wiki/Chosen-ciphertext_attack)
- [Optimal Asymmetric Encryption Padding (OAEP) - Wikipedia](https://en.wikipedia.org/wiki/Optimal_asymmetric_encryption_padding)