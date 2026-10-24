### Descripción

How about some hide and seek heh? Look at this image here ([atbash.jpg](https://challenge-files.cylabacademy.net/library/d1a6b6365f32679d90a52e42234c7bad12bdfb9ac5e87598af9f1202ee047227/atbash.jpg)).

### Solución

1. La imagen `atbash.jpg` es un gráfico de referencia del "Atbash Cipher" (una rueda con el alfabeto normal por fuera y el alfabeto invertido por dentro). No tiene EXIF, XMP, comentarios JPEG, datos concatenados ni nada legible a simple vista ni por LSB (al ser JPEG con compresión con pérdida, el LSB de los píxeles no sirve como canal de esteganografía confiable).
2. El nombre del archivo y la imagen son la pista: hay que usar **steghide**, una herramienta clásica que esconde datos dentro de los coeficientes DCT de un JPEG (resiste la compresión, a diferencia del LSB espacial). Se extrae con contraseña vacía:

```bash
   steghide extract -sf atbash.jpg
```

Esto produce un archivo de texto con el contenido:

```
  zxzwvnb{zgyzhs_xizxp_02u11yy3}
```

3. Pasamos la salida a un decorder atbash, yo use: https://www.boxentriq.com/ciphers/atbash-cipher
4. Y nos da la flag: academy{atbash_crack_02f11bb3}

**Flag:** academy{atbash_crack_02f11bb3}

### Notas Adicionales

### Referencias