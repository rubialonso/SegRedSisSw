### Descripción

RED, RED, RED, RED. Download the image: [red.png](https://challenge-files.cylabacademy.net/library/fefcf06050d98347e1585e5cb9f2940967f82e0b89c591966473c752de9f3aba/red.png)

### Solución

1. Descargar `red.png` (128x128, RGBA). A simple vista es un cuadrado rojo sólido, pero al inspeccionar los píxeles con PIL se ve que los valores de R/G/B/A varían en ±1 entre píxeles (ej. `(254,0,0,255)`, `(255,1,0,254)`...), señal clara de esteganografía LSB.
2. Se extraen los bits menos significativos de los 4 canales (R, G, B, A) en orden, por píxel:

```python
   from PIL import Image
   im = Image.open('red.png').convert('RGBA')
   pixels = list(im.getdata())
   bits = []
   for p in pixels:
       for ci in (0,1,2,3):   # R, G, B, A
           bits.append(p[ci] & 1)
   chars = []
   for i in range(0, len(bits)-8+1, 8):
       byte = bits[i:i+8]
       val = 0
       for b in byte:
           val = (val<<1)|b
       chars.append(val)
   data = bytes(chars)
```

3. El resultado es una cadena Base64 que se repite muchas veces a lo largo de la imagen (el mensaje se "rellenó" varias veces hasta usar todos los píxeles):

```
   YWNhZGVteXtyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==...
```

4. Se decodifica Base64:

```python
   import base64
   base64.b64decode('YWNhZGVteXtyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==')
   # b'academy{r3d_1s_th3_ult1m4t3_cur3_f0r_54dn355_}'
```

**Flag:** `academy{r3d_1s_th3_ult1m4t3_cur3_f0r_54dn355_}`

### Notas Adicionales

A diferencia de St3g0 (mensaje ASCII directo en los LSB), acá el mensaje oculto en los LSB era él mismo una cadena Base64, que había que decodificar una vez más para llegar al texto final. Usar los 4 canales (incluyendo alfa) fue clave para que el mensaje decodificara limpio.

### Referencias