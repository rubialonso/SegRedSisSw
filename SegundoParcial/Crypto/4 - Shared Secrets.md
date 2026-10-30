### Descripción

A message was encrypted using a shared secret... but it looks like one side of the exchange leaked something. Can you piece together the secret and get the flag? Download the message and source code.

_by Yahaya Meddy · picoCTF 2026_

### Solución

1. Se descargan `ss_message.txt` y `ss_encryption.py` con la terminal web.
2. `ss_encryption.py` implementa un intercambio de claves Diffie-Hellman clásico:
```python
from Crypto.Util.number import getPrime
from random import randint

g = 2
p = getPrime(1048)

a = randint(2, p - 2)
A = pow(g, a, p)

b = randint(2, p - 2)
B = pow(g, b, p)

shared = pow(A, b, p)

flag = b"academy{...}"
enc = bytes([x ^ (shared % 256) for x in flag])

with open("message.txt", "w") as f:
    f.write(f"g = {g}\n")
    f.write(f"p = {p}\n")
    f.write(f"A = {A}\n")
    f.write(f"b = {b}\n")   # <-- ¡el exponente secreto "b" se filtra!
    f.write(f"enc = {enc.hex()}\n")
```

3. El archivo de salida escribe, además de los parámetros públicos `g`, `p`, `A`, el exponente **privado** `b` del otro lado del intercambio (que nunca debería revelarse). Con `b` filtrado, el secreto compartido se puede recalcular directamente como `shared = pow(A, b, p)`, exactamente igual que lo haría el receptor legítimo.
4. El flag fue cifrado con un XOR de un solo byte: cada byte de `flag` se combina con `shared % 256`. Al conocer `shared`, basta con aplicar el mismo XOR sobre `enc` para recuperarlo:
```python
lines = dict(l.strip().split(' = ') for l in open('ss_message.txt') if '=' in l)
g = int(lines['g']); p = int(lines['p']); A = int(lines['A']); b = int(lines['b'])
enc = bytes.fromhex(lines['enc'])

shared = pow(A, b, p)
flag = bytes(x ^ (shared % 256) for x in enc)
print(flag)
```

5. Resultado: `academy{dh_s3cr3t_e3954beb}`

Flag: academy{dh_s3cr3t_e3954beb}

### Notas Adicionales

Diffie-Hellman es seguro siempre que los exponentes privados (`a`, `b`) se mantengan en secreto; aquí el propio script de cifrado comete el error de escribir el exponente privado del receptor en el archivo de salida, lo cual anula por completo la seguridad del intercambio, sin necesidad de resolver el problema del logaritmo discreto.

### Referencias

- [Diffie–Hellman key exchange - Wikipedia](https://en.wikipedia.org/wiki/Diffie%E2%80%93Hellman_key_exchange)