### Descripción

We found a leak of a blackmarket website's login credentials. Can you find the password of the user `cultiris` and successfully decrypt it?

El primer usuario en `usernames.txt` corresponde a la primera contraseña en `passwords.txt`, y así sucesivamente.

Archivo adjunto: `leak.tar` (contiene `leak/usernames.txt` y `leak/passwords.txt`, 505 líneas cada uno).

### Solución

1. Se extrae el archivo tar:

```
~/cylab/crypto
➜ tar -xf leak.tar
➜ ls leak
passwords.txt  usernames.txt
```

2. Se busca la línea del usuario `cultiris` en `usernames.txt`:

```
➜ grep -n "cultiris" leak/usernames.txt
378:cultiris
```

3. Se obtiene la contraseña correspondiente en la misma línea (378) de `passwords.txt`:

```
➜ sed -n '378p' leak/passwords.txt
npnqrzl{P7e1S_54I35_71Z3}
```

4. La contraseña cifrada tiene el mismo formato `xxxxxxx{...}` que un flag `academy{...}`. Se calcula la diferencia letra a letra entre `npnqrzl` y `academy`, obteniendo un desplazamiento constante de 13 posiciones, es decir, un cifrado **ROT13** (César con desplazamiento 13, su propio inverso).
5. Se aplica ROT13 a toda la contraseña:

python

```python
import codecs
pw = "npnqrzl{P7e1S_54I35_71Z3}"
print(codecs.encode(pw, 'rot13'))
```

```
~/cylab/crypto
➜ python3 rot13.py
academy{C7r1F_54V35_71M3}
```

Flag: `academy{C7r1F_54V35_71M3}`

### Notas Adicionales

Este reto combina dos pasos: (1) correlacionar dos archivos mediante el número de línea para encontrar el dato de interés, y (2) reconocer que el "cifrado" de la contraseña filtrada es en realidad ROT13, un caso particular (y muy débil) del cifrado César, fácilmente identificable por mantener la estructura `palabra{...}` reconocible.

### Referencias

- [ROT13 - Wikipedia](https://en.wikipedia.org/wiki/ROT13)