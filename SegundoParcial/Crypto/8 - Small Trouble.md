### Descripción

Everything seems secure; strong numbers, familiar parameters but something small might ruin it all. Can you recover the message? Download the message and source code.

_by Yahaya Meddy · picoCTF 2026_

### Solución

1. Se descargan `st_message.txt` y `st_encryption.py` con la terminal web.
2. `st_encryption.py` genera una clave RSA de 2096 bits de forma aparentemente normal, pero con un detalle crítico: en lugar de elegir primero el exponente público `e` (como se hace habitualmente), elige primero el exponente **privado** `d` como un número pequeño (`getPrime(256)`, es decir, de solo 256 bits frente a un módulo de ~2096 bits), y deriva `e` a partir de él:

```python
from Crypto.Util.number import getPrime, inverse, bytes_to_long

p = getPrime(1048)
q = getPrime(1048)
n = p * q
phi = (p - 1) * (q - 1)

d = getPrime(256)          # <-- exponente privado deliberadamente pequeño
e = inverse(d, phi)        # e resulta gigantesco (~2095 bits)

flag = b'academy{...}'
m = bytes_to_long(flag)
c = pow(m, e, n)
```

3. Un `d` pequeño en relación al módulo `n` (en general, cuando `d < n^0.25 / 3` aproximadamente) es explotable mediante el **ataque de Wiener**: a partir de la fracción `e/n` se calcula su expansión en fracción continua, y se prueba cada convergente `k/d'` como candidato, verificando si factoriza correctamente `n` (es decir, si `d'` recupera los primos `p`, `q` correctos).
4. Se implementa el ataque de Wiener en Python (fracciones continuas + verificación de la ecuación `e*d - 1 = k*phi` y factorización de `n` vía la fórmula de las raíces de `x² - (n-phi+1)x + n = 0`):

```python
def continued_fraction(num, den):
    cf = []
    while den:
        cf.append(num // den)
        num, den = den, num % den
    return cf

def convergents(cf):
    n0, d0, n1, d1 = 0, 1, 1, 0
    for a in cf:
        n0, n1 = n1, a * n1 + n0
        d0, d1 = d1, a * d1 + d0
        yield n1, d1

e = ...; n = ...; c = ...
cf = continued_fraction(e, n)   # aprox. de e/n
for k, d_cand in convergents(cf):
    if k == 0:
        continue
    if (e * d_cand - 1) % k != 0:
        continue
    phi_cand = (e * d_cand - 1) // k
    # x^2 - (n - phi_cand + 1) x + n = 0
    b = n - phi_cand + 1
    disc = b * b - 4 * n
    if disc < 0:
        continue
    sq = int(disc**0.5)
    if sq * sq == disc and (b - sq) % 2 == 0:
        p_cand = (b - sq) // 2
        q_cand = (b + sq) // 2
        if p_cand * q_cand == n:
            d = d_cand
            break

m = pow(c, d, n)
flag = m.to_bytes((m.bit_length() + 7) // 8, 'big')
print(flag)
```

5. Se recupera `d = 98884991171849433242575812190111020882886360413844675438543286862305004210131` (256 bits, exactamente como predecía el script de generación), se verifica que `p * q == n`, y se descifra el mensaje.
6. Resultado: `academy{sm4ll_d_073963cb}`

Flag: academy{sm4ll_d_073963cb}

### Notas Adicionales

RSA requiere que **tanto** `e` como `d` sean suficientemente grandes: no basta con elegir un módulo `n` de tamaño robusto. Un exponente privado `d` pequeño es tan peligroso como un exponente público `e` pequeño mal usado, porque el ataque de Wiener permite recuperarlo en tiempo polinomial a partir únicamente de `(n, e)`, sin necesidad de factorizar `n` directamente.

### Referencias

- [Wiener's attack - Wikipedia](https://en.wikipedia.org/wiki/Wiener%27s_attack)
- [Continued fraction - Wikipedia](https://en.wikipedia.org/wiki/Continued_fraction)