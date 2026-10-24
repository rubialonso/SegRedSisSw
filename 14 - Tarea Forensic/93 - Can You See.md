### Descripción

How about some hide and seek? Download this file here (`unknown.zip`). [unknown.zip](https://challenge-files.cylabacademy.net/library/3781b74e6ee2cd04bb03da6614e1c184422f725bf14a19d5b61f8b2038e1c11c/unknown.zip)

### Solución

1. Descomprimir `unknown.zip`, contiene una sola imagen: `ukn_reality.jpg` (4308x2875).
2. `PIL`/`Image._getexif()` no reporta EXIF estándar, así que se revisan los metadatos XMP embebidos, igual que en el reto 1 ("information"):

```python
   d = open('ukn_reality.jpg','rb').read()
   idx = d.find(b'<x:xmpmeta')
   idx2 = d.find(b'</x:xmpmeta>')
   print(d[idx:idx2+12].decode())
```

3. Aparece un campo `cc:attributionURL` con un valor en Base64:

```xml
   <cc:attributionURL rdf:resource='YWNhZGVteXtNRTc0RDQ3QV9ISUREM05fOTI2NmRlMWV9Cg=='/>
```

4. Se decodifica el Base64:

```python
   import base64
   base64.b64decode('YWNhZGVteXtNRTc0RDQ3QV9ISUREM05fOTI2NmRlMWV9Cg==')
   # b'academy{ME74D47A_HIDD3N_9266de1e}\n'
```

**Flag:** `academy{ME74D47A_HIDD3N_9266de1e}`

### Notas Adicionales

Mismo patrón que el reto "information": la flag no está en los píxeles sino en los metadatos XMP (campo de licencia/atribución), codificada en Base64. No hacía falta tocar la imagen en sí (ni LSB, ni EOF/carving).

### Referencias