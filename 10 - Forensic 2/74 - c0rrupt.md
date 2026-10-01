### Descripción
We found this file. Recover the flag.

Pista: *Try fixing the file header* (intenta arreglar la cabecera del archivo).

### Solución
Primero hay que descargar el archivo:

```
~/cylab via 🐍 v3.13.5 (mivenv) 
➜ wget https://challenge-files.cylabacademy.net/library/8388ecc430588d15064755583476bec46e23d42a6d8de6e8995c19e40f2e4c58/c0rrupt-mystery

```

Luego vemos qué tipo de archivo es:

```
➜ file c0rrupt-mystery
c0rrupt-mystery: data
```

`file` no lo reconoce. Al volcar los primeros bytes en hexadecimal se ve que parece un PNG con la cabecera dañada, porque aparecen los chunks `sRGB`, `gAMA`, `pHYs`, `IDAT` e `IEND`:

```
89 65 4e 34 0d 0a b0 aa 00 00 00 0d 43 22 44 52 ...
```

Una firma PNG válida es `89 50 4e 47 0d 0a 1a 0a`, seguida del chunk `IHDR`. Para localizar los errores se recorren los chunks (longitud, tipo, datos, CRC) y se comprueba el CRC de cada uno. Los bytes corruptos eran:

| Offset | Valor corrupto | Valor correcto | Dónde |
|---|---|---|---|
| 0–7 | `89 65 4e 34 0d 0a b0 aa` | `89 50 4e 47 0d 0a 1a 0a` | Firma PNG |
| 12–15 | `43 22 44 52` (`C"DR`) | `49 48 44 52` (`IHDR`) | Tipo del primer chunk |
| 70 | `aa` | `00` | Datos de `pHYs` |
| 83–84 | `aa aa` | `00 00` | Longitud del primer `IDAT` |
| 87–90 | `ab 44 45 54` | `49 44 41 54` (`IDAT`) | Tipo del primer `IDAT` |

Se pueden corregir con este script en Python, que además valida los CRC de todos los chunks:

```python
import struct, zlib

d = bytearray(open('c0rrupt-mystery', 'rb').read())
d[0:8]   = bytes.fromhex('89504e470d0a1a0a')  # firma PNG
d[12:16] = b'IHDR'                             # tipo del primer chunk
d[70]    = 0x00                                # datos de pHYs
d[83:85] = b'\x00\x00'                         # longitud del primer IDAT
d[87:91] = b'IDAT'                             # tipo del primer IDAT

# Verificar CRC de todos los chunks
i = 8
while i < len(d):
    l = struct.unpack('>I', d[i:i+4])[0]
    t = bytes(d[i+4:i+8])
    crc = struct.unpack('>I', d[i+8+l:i+12+l])[0]
    print(i, l, t, crc == zlib.crc32(bytes(d[i+4:i+8+l])))
    i += 12 + l

open('fixed.png', 'wb').write(d)
```

Todos los CRC salen `True` y la imagen se abre correctamente (1642×1095 px). Al abrir `fixed.png` aparece la flag en texto negro, parcialmente cubierta por garabatos rojos.

Flag:
```
academy{c0rrupt10n_1847995}
```

### Notas Adicionales
- La firma de un PNG siempre es `89 50 4e 47 0d 0a 1a 0a`. Si un archivo "data" tiene `0d 0a` en los bytes 4–5 y chunks con nombres como `IDAT` o `IEND`, probablemente es un PNG dañado.
- Cada chunk PNG tiene la estructura `longitud (4 B) | tipo (4 B) | datos | CRC32 (4 B)`. Que un CRC falle indica dónde hay corrupción.
- El texto de la flag estaba tapado en parte por ruido rojo, pero se leía bien.
- Herramientas alternativas: un editor hexadecimal (`hexed.it`, `bless`, `ghex`) o `pngcheck -v` para localizar los errores.

### Referencias
- Especificación PNG (estructura de chunks y firma): https://www.w3.org/TR/png/
- Lista de firmas de archivos (magic numbers): https://en.wikipedia.org/wiki/List_of_file_signatures