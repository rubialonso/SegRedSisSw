### Descripción

It seems that another encrypted message has been intercepted. The encryptor seems to have learned their lesson though and now there isn't any punctuation! Can you still crack the cipher?

Archivo adjunto (`message_4.txt`): texto cifrado de ~1250 caracteres, sin espacios ni puntuación, sin clave.

### Solución

1. Sin espacios ni puntuación, el "crib dragging" manual (como en `substitution1`) se vuelve mucho más difícil porque no se pueden identificar los límites de las palabras a simple vista.
2. Se opta por un ataque automatizado de criptoanálisis de frecuencias basado en **cuatrigramas** (quadgrams), el método estándar para romper cifrados de sustitución monoalfabética sin clave:
    - Se construye una tabla de frecuencias de cuatrigramas en inglés a partir de un corpus de texto local (documentación técnica en inglés disponible en el sistema).
    - Se implementa un algoritmo de "hill climbing" (ascenso de colina) con reinicios aleatorios: se parte de una sustitución aleatoria y en cada iteración se intercambian dos letras del mapeo; el intercambio se conserva solo si mejora la verosimilitud del texto resultante (suma de log-probabilidades de sus cuatrigramas) según la tabla de frecuencias.

```python
def score(text, logp, floor):
    return sum(logp.get(text[i:i+4], floor) for i in range(len(text)-3))

# 40 reinicios aleatorios x 4000 intercambios cada uno,
# aceptando el intercambio solo si mejora el score
```

3. Tras varias decenas de reinicios, el algoritmo converge a una sustitución que produce texto en inglés perfectamente legible:

```
There exists several other well established high school computer security
competitions including CyberPatriot and US Cyber Challenge. These competitions
focus primarily on systems administration fundamentals... Academy is an
offensively oriented high school computer security competition...

The flag is academy{N6R4M_4N41Y515_15_73D10U5_FD56C357}
```

Flag: `academy{N6R4M_4N41Y515_15_73D10U5_FD56C357}`

### Notas Adicionales

El propio flag resultante, "NGRAM ANALYSIS IS TEDIOUS" (análisis de n-gramas), hace un guiño directo a la técnica usada para resolverlo: un ataque de criptoanálisis por frecuencias de n-gramas (cuatrigramas), necesario precisamente porque el mensaje no tiene espacios ni puntuación que sirvieran de pista.

### Referencias

- [Frequency analysis - Wikipedia](https://en.wikipedia.org/wiki/Frequency_analysis)
- [N-gram - Wikipedia](https://en.wikipedia.org/wiki/N-gram)