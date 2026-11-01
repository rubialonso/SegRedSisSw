#### Descripción

Challenge de esteganografía: se entrega un archivo JPEG (`img.jpg`) que contiene una contraseña oculta en sus metadatos, necesaria para extraer un archivo oculto embebido con `steghide`.

#### Solución

1. Se descargó el archivo `img.jpg` del challenge.
2. Al inspeccionar el archivo con `file img.jpg`, se observó un campo de comentario JFIF no estándar:  
    `comment: "c3R1Z2hpZGU6Y0VGNmVuZHZjbVE9"`
3. Ese valor es texto codificado en base64. Decodificándolo una vez se obtiene:  
    `steghide:cEF6endvcmQ=`
4. La parte después de `steghide:` es a su vez base64. Decodificándola una segunda vez se obtiene la contraseña real:  
    `pAzzword`
5. Con la contraseña recuperada, se usó `steghide` para extraer el contenido oculto de la imagen:

```
   steghide extract -sf img.jpg -p pAzzword
```

6. Esto generó un archivo `flag.txt` con la bandera:

```
   academy{h1dd3n_1n_1m4g3_d0c4a4e2}
```

**Flag:** academy{h1dd3n_1n_1m4g3_d0c4a4e2}
#### Notas Adicionales

- La clave estaba oculta con una doble capa de base64 dentro de un campo de metadatos poco habitual (comentario JFIF), en lugar de en el EXIF estándar — vale la pena revisar todos los campos de metadatos, no solo EXIF, cuando se sospecha esteganografía.
- `steghide` embebe datos usando LSB (least significant bit) en archivos JPEG/BMP/WAV/AU, protegidos opcionalmente con contraseña; sin la contraseña correcta, `extract` falla silenciosamente o da error de passphrase incorrecta.

#### Referencias

- steghide — manual oficial: [https://steghide.sourceforge.net/documentation.php](https://steghide.sourceforge.net/documentation.php)
- “Steganography in JPEG images” — overview técnico: [https://www.garykessler.net/library/fsc_stego.html](https://www.garykessler.net/library/fsc_stego.html)