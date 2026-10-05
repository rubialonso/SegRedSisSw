### Descripción

### Solución
1. Crear una carpeta con mkdir y viajar hacia el directorio de esa carpeta, estando ahi descargamos la imagen con wget:
```
~ via C v14.2.0-gcc 
➜ mkdir matryoshka

~ via C v14.2.0-gcc 
➜ cd matryoshka/

~/matryoshka 
➜ wget https://challenge-files.cylabacademy.net/library/2eb277d09563812ad880fdd564d0fb59c084a64f514f6e12998534c8f7997405/dolls.jpg
```

2. Lo analizamos con binwalk, veremos que tiene dentro otro archivo:
```
~/matryoshka took 5m12s 
➜ binwalk dolls.jpg

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 594 x 1104, 8-bit/color RGBA, non-interlaced
3226          0xC9A           TIFF image data, big-endian, offset of first image directory: 8
272492        0x4286C         Zip archive data, at least v2.0 to extract, compressed size: 378929, uncompressed size: 383919, name: base_images/2_c.jpg
651587        0x9F143         End of Zip archive, footer length: 22
```

3. Usar unzip hasta descomprimir todas las imagenes internas, hasta que de un archivo flag.txt:
```
~/matryoshka 
➜ unzip dolls.jpg
inflating: base_images/2_c.jpg

~/matryoshka 
❯ unzip base_images/2_c.jpg
inflating: base_images/3_c.jpg

~/matryoshka 
➜ unzip base_images/3_c.jpg
inflating: base_images/4_c.jpg

~/matryoshka 
❯ unzip base_images/4_c.jpg
 extracting: flag.txt                

~/matryoshka 
❯ cat flag.txt
academy{ZNTyvSDXRNO1d0xCkBRMhAoiafpCTvgW}
```

**Flag**: academy{ZNTyvSDXRNO1d0xCkBRMhAoiafpCTvgW}
### Notas Adicionales

### Referencias