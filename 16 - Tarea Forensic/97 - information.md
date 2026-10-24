### Descripción

Files can always be changed in a secret way. Can you find the flag? [cat.jpg](https://challenge-files.cylabacademy.net/library/c585b4adbdaa06f409db7bf5012c2e58e9aab24669764a5f1cf0f9ce0d60dcfd/cat.jpg)
### Solución

1. Descargar `cat.jpg`.
2. La imagen no tiene EXIF estándar (`_getexif()` de PIL devuelve vacío), así que se revisaron los metadatos XMP embebidos buscando el bloque `<x:xmpmeta>`:

```python
   d = open('cat.jpg','rb').read()
   idx = d.find(b'<x:xmpmeta')
   idx2 = d.find(b'</x:xmpmeta>')
   print(d[idx:idx2+12].decode())
```

3. Dentro del XMP aparece un campo `cc:license` con un valor en Base64:

```xml
   <cc:license rdf:resource='YWNhZGVteXt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9'/>
```

4. Se decodifica el Base64:

```python
   import base64
   base64.b64decode('YWNhZGVteXt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9')
   # b'academy{the_m3tadata_1s_modified}'
```

**Flag:** `academy{the_m3tadata_1s_modified}`

### Notas Adicionales

El nombre del reto ("information") apunta directo a los metadatos del archivo. No bastaba con mirar el EXIF clásico (cámara, GPS, etc.), había que revisar también el bloque XMP, que suele quedar embebido por herramientas como ExifTool.

### Referencias
