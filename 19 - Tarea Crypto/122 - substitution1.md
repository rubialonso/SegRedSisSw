### Descripción

A second message has come in the mail, and it seems almost identical to the first one. Maybe the same thing will work again.

Archivo adjunto (`message_3.txt`), sin clave dada esta vez:

```
NDQy (yzkjd qkj nbwdaje dze qsbc) bje b dfwe kq nklwadej yenajmdf nklwedmdmki. ...
```

### Solución

1. A diferencia del reto anterior, aquí **no** se entrega la clave de sustitución, así que hay que deducirla por criptoanálisis manual (ataque por palabra probable / "crib dragging"), apoyándose en el contexto (claramente describe qué es un CTF).
2. Se identifican palabras cortas repetidas y muy probables por contexto: `NDQy` → "CTFs" (aparece dos veces), `yzkjd qkj` → "short for", `nbwdaje dze qsbc` → "capture the flag", etc. Cada coincidencia aporta nuevas letras del mapeo cifrado→texto plano.
3. Se va completando la tabla de sustitución letra por letra, verificando cada nueva palabra con el mapeo parcial ya deducido (p. ej. `nzbsseicey` → "challenges", `wjkosel-yksxmic` → "problem-solving", etc.), hasta cubrir las 26 letras.
4. Con el mapeo completo se descifra el texto completo con un script en Python:

python

```python
m = {'n':'c','d':'t','q':'f','y':'s','z':'h','k':'o','j':'r','w':'p',
     'a':'u','b':'a','e':'e','s':'l','c':'g','f':'y','l':'m','m':'i',
     'i':'n','v':'d','h':'w','x':'v','u':'k','o':'b','g':'q'}
```

5. Resultado:

```
CTFs (short for capture the flag) are a type of computer security competition.
Contestants are presented with a set of challenges which test their creativity,
technical (and googling) skills, and problem-solving ability. ...

For this problem, the flag is: academy{FR3QU3NCY_4774CK5_4R3_C001_26A742EB}
```

Flag: `academy{FR3QU3NCY_4774CK5_4R3_C001_26A742EB}`

### Notas Adicionales

El texto descrifrado es, de hecho, una descripción casi textual de qué es un CTF, lo que facilitó mucho encontrar palabras clave ("CTF", "flag", "challenge", "competition") para arrancar el ataque por palabra probable.

### Referencias

- [Capture the flag (cybersecurity) - Wikipedia](https://en.wikipedia.org/wiki/Capture_the_flag_\(cybersecurity\))
- [Known-plaintext / crib-dragging attack - Wikipedia](https://en.wikipedia.org/wiki/Known-plaintext_attack)