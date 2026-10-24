### Descripción

Every file gets a flag. The SOC analyst saw one image been sent back and forth between two people. They decided to investigate and found out that there was more than what meets the eye here. [flag.png](https://challenge-files.cylabacademy.net/library/f7b0490c7122b66d8882c3da0c6b027eab5a9ffa3ea6b5e4c903bc3f30a950aa/flag.png)

### Solución

1. Descargar `flag.png` (700x450, RGB).
2. `file` identifica el archivo como PNG válido, pero el tamaño en disco (21768 bytes) es mayor al que ocuparía solo la imagen. Se buscó el marcador `IEND` del PNG y se revisó si había datos después de él:

```python
   d = open('flag_hideme.png','rb').read()
   idx = d.find(b'IEND')
   print(len(d) - (idx+8))   # 5839 bytes extra
   print(d[idx+8:idx+8+50])  # empieza con 'PK\x03\x04' -> firma de ZIP
```

3. Efectivamente hay un archivo ZIP concatenado después del PNG. Se extrae ese bloque y se descomprime:

```python
   zipdata = d[idx+8:]
   open('hidden.zip','wb').write(zipdata)
```


```bash
   unzip hidden.zip
   # secret/flag.png  (1225x41, escala de grises)
```

4. Al abrir `secret/flag.png` se ve directamente el texto de la flag.

**Flag:** `academy{Hiddinng_An_imag3_within_@n_ima9e_404ff71e}`

### Notas Adicionales

Técnica de "file carving"/concatenación: un PNG es válido hasta su chunk `IEND`; cualquier cosa después es ignorada por los visores de imágenes pero sigue siendo un archivo válido (en este caso un ZIP) si se extrae por separado.

### Referencias