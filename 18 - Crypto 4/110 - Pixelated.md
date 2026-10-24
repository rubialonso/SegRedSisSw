### Descripción

I have these 2 images, can you make a flag out of them? [scrambled1.png](https://challenge-files.cylabacademy.net/library/fa686cfe375627b0131e670a19ec4775a873562ee3006dae8a40796e3e2b5e3c/scrambled1.png) [scrambled2.png](https://challenge-files.cylabacademy.net/library/fa686cfe375627b0131e670a19ec4775a873562ee3006dae8a40796e3e2b5e3c/scrambled2.png)

### Solución

1. Ambas imágenes (256x256) a simple vista son ruido RGB puro, sin ningún patrón visible — típico de un cifrado tipo "one-time pad" sobre imágenes: una imagen es ruido aleatorio y la otra es ese mismo ruido combinado con la imagen real mediante XOR.
2. Se hace XOR píxel a píxel (por canal R, G, B) entre ambas imágenes:

```python
   from PIL import Image
   import numpy as np
   a = np.array(Image.open('scrambled1.png').convert('RGB'))
   b = np.array(Image.open('scrambled2.png').convert('RGB'))
   x = np.bitwise_xor(a, b)
   Image.fromarray(x).save('xor_result.png')
```

3. El resultado revela directamente un texto (con algo de ruido de color por el propio XOR, fácil de limpiar binarizando: todo lo que no sea blanco puro se vuelve negro):

```python
   mask = np.any(x < 240, axis=2)
   out = np.ones_like(x) * 255
   out[mask] = [0, 0, 0]
```

4. El texto resultante es la flag completa: `academy{2f16d0c4}`.

**Flag:** `academy{2f16d0c4}`

### Notas Adicionales

Si dos imágenes del mismo tamaño se generan como `ruido` y `ruido XOR mensaje`, el mensaje se recupera trivialmente con un XOR directo entre ambas — no hace falta "desordenar" ni revertir ningún proceso de scrambling de posiciones, pese al nombre del reto.

### Referencias