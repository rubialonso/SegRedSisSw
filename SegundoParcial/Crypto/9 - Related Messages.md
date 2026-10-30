### Descripción

Oops! I have a typo in my first message so i sent it again! I used RSA twice so this is secure right? Download the challenge code (`chall.py`) and output (`output.txt`).

_picoCTF 2026_

### Solución

1. Se descargan `rm_chall.py` y `rm_output.txt` con la terminal web.
2. `rm_chall.py` revela el escenario: el mismo mensaje (con una pequeña corrección, un "typo") se cifra **dos veces** bajo la **misma** clave pública RSA (mismo módulo `N`, mismo exponente público pequeño `e = 0x11 = 17`):

```python
Message = bytes_to_long(b"...")
Message_fixed = bytes_to_long(b"...")  # el mensaje "corregido"
e = 0x11
p = getPrime(1024)
q = getPrime(1024)
phi = (p - 1) * (q - 1)
d = inverse(e, phi)
N = p * q

ciphertext = pow(Message, e, N)
ciphertext2 = pow(Message_fixed, e, N)

print(ciphertext, ciphertext2)
print(Message - Message_fixed)   # ¡la diferencia exacta entre ambos mensajes se filtra!
print(N)
```

3. `rm_output.txt` contiene 4 líneas: `ciphertext` (c1), `ciphertext2` (c2), la diferencia exacta `diff = Message - Message_fixed` (en este caso `-3`) y `N`.
4. Esto es el escenario clásico del **ataque de Coppersmith / Franklin-Reiter de mensajes relacionados**: si dos mensajes `m1` y `m2 = m1 - diff` (una relación lineal conocida) se cifran con el mismo `(N, e)` pequeño, se puede recuperar `m1` sin factorizar `N`, calculando el máximo común divisor de dos polinomios sobre `Z/NZ`:
    
    - `f1(x) = x^e - c1` (tiene a `m1` como raíz)
    - `f2(x) = (x - diff)^e - c2` (tiene a `m1` como raíz, puesto que `m2 = m1 - diff`)
    
    El `gcd(f1, f2)` sobre `Z/NZ` es, con muy alta probabilidad, un polinomio lineal `(x - m1)`, de donde se despeja `m1` directamente.
5. Se implementa aritmética polinomial manual (resta, división larga con inverso modular del coeficiente líder, y Euclides) para calcular el gcd sobre `Z/NZ`, usando `e = 17` vía expansión binomial:

```python
from math import comb

c1, c2, diff, N = [...]   # leídos de rm_output.txt
e = 0x11

def poly_trim(p):
    while len(p) > 1 and p[-1] % N == 0:
        p.pop()
    return p

def poly_sub(a, b):
    n = max(len(a), len(b))
    a = a + [0]*(n-len(a)); b = b + [0]*(n-len(b))
    return poly_trim([(a[i]-b[i]) % N for i in range(n)])

def poly_divmod(a, b):
    a = poly_trim(a[:]); b = poly_trim(b[:])
    inv_lead = pow(b[-1], -1, N)
    q = [0]*(max(len(a)-len(b)+1, 1))
    while len(a) >= len(b) and not (len(a) == 1 and a[0] % N == 0):
        coef = (a[-1]*inv_lead) % N
        deg = len(a) - len(b)
        q[deg] = coef
        a = poly_trim(poly_sub(a, [0]*deg + [(coef*x) % N for x in b]))
    return q, a

def poly_gcd(a, b):
    a = poly_trim(a[:]); b = poly_trim(b[:])
    while not (len(b) == 1 and b[0] % N == 0):
        _, r = poly_divmod(a, b)
        a, b = b, r
    return a

f1 = [(-c2) % N] + [0]*(e-1) + [1]          # x^e - c2  (ver nota sobre el orden de c1/c2)
f2 = [0]*(e+1)
for k in range(e+1):
    f2[k] = (comb(e, k) * pow(diff, e-k, N)) % N
f2[0] = (f2[0] - c1) % N

g = poly_gcd(f1, f2)
a1, a0 = g[1], g[0]
m = (-a0 * pow(a1, -1, N)) % N
flag = m.to_bytes((m.bit_length()+7)//8, 'big')
print(flag)
```

6. Un primer intento, construyendo `f1` a partir de `c1` y `f2 = (x+diff)^e - c2` a partir de `c2`, dio un `gcd` de grado 0 (constante), señal de que la relación entre polinomios y ciphertexts no era la correcta. Probando sistemáticamente las combinaciones de asignación de `c1`/`c2` a cada polinomio junto con el signo de `diff`, la combinación que produce un `gcd` de grado 1 válido resultó ser la de arriba (`f1` con `c2`, `f2` con `c1` y `diff` positivo).
7. Resultado: `academy{m3ssage_w1th_typ0}`

Flag: academy{m3ssage_w1th_typ0}

### Notas Adicionales

Cifrar dos veces el "mismo" mensaje con RSA —incluso con una pequeña variación conocida entre ambos— con un exponente público pequeño y la misma clave no aporta seguridad adicional; al contrario, filtra suficiente estructura algebraica (vía el ataque de mensajes relacionados de Franklin-Reiter) para recuperar el mensaje sin factorizar el módulo. El punto más delicado de la implementación fue determinar experimentalmente el orden/signo correcto en que la relación conocida (`diff`) y los dos ciphertexts entran en los polinomios, ya que un error de signo produce un gcd degenerado (constante) en vez del factor lineal esperado.

### Referencias

- [Coppersmith's attack - Wikipedia](https://en.wikipedia.org/wiki/Coppersmith%27s_attack)
- [Polynomial greatest common divisor - Wikipedia](https://en.wikipedia.org/wiki/Polynomial_greatest_common_divisor)