### Descripción

We received an encrypted message. The modulus is built from primes large enough that factoring them isn't an option, at least not today. See if you can make sense of the numbers and reveal the flag.

Archivo adjunto (`message.txt`) con los valores RSA:

```
n = 374389...(4095 bits)
e = 20
c = 363505...(3813 bits)
```

### Solución

1. Se observa que el exponente público `e = 20` es muy pequeño en comparación con el módulo `n` (4095 bits). Esto es característico del clásico "ataque de exponente bajo" en RSA: si el mensaje `m` es lo suficientemente pequeño (como un flag corto convertido a entero), entonces `m^e` nunca llega a superar a `n`, por lo que la operación de cifrado `c = m^e mod n` en realidad nunca aplica el módulo, es decir, `c = m^e` como número entero puro.
2. Esto permite recuperar `m` simplemente calculando la raíz entera 20-ésima de `c`, sin necesidad de factorizar `n` ni conocer la clave privada.
3. Se implementa una búsqueda binaria para la raíz entera (ya que los números son demasiado grandes para `math.isqrt`/`round(c**(1/e))` con precisión de punto flotante):

```python
def iroot(x, n):
    if x == 0:
        return 0
    hi = 1
    while hi ** n <= x:
        hi *= 2
    lo = hi // 2
    while lo < hi:
        mid = (lo + hi + 1) // 2
        if mid ** n <= x:
            lo = mid
        else:
            hi = mid - 1
    return lo

m = iroot(c, e)
print(m ** e == c)                     # True -> confirma raiz exacta, sin resto modular
print(m.to_bytes((m.bit_length()+7)//8, 'big'))
```

4. Al ejecutar el script se confirma que `m**20 == c` exactamente (sin reducción modular), y al convertir el entero resultante a bytes se obtiene el flag directamente:

```
~/cylab/crypto
➜ python3 rsa_power.py
e= 20
root bits= 191
check r**e == c: True
b'academy{t1ny_e_d6b18b0b}'
```

Flag: `academy{t1ny_e_d6b18b0b}`

### Notas Adicionales

Este ataque solo funciona porque `m^e < n`. Si el mensaje fuera más largo (más bits) en relación al módulo, `m^e` superaría a `n` y la reducción módulo `n` sí tendría efecto, haciendo que la raíz entera directa ya no reproduzca el mensaje original. Por eso es importante en RSA usar un relleno (padding, p. ej. OAEP) y exponentes/mensajes que no permitan este tipo de ataque de raíz directa.

### Referencias
- [RSA low public exponent attack - Wikipedia (RSA cryptosystem, Security section)](https://en.wikipedia.org/wiki/RSA_\(cryptosystem\)#Low_private_exponent)