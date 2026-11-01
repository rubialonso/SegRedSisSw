#### Descripción

This file seems broken... or is it? Maybe a couple of bytes could make all the difference. Can you figure out how to bring it back to life? Download the file here.

**Hints:**
1. Try checking the file's header.
2. JPEG
3. Tools like xxd or hexdump can help you inspect and edit file bytes.
#### Solución

1. Descargar el archivo proporcionado por el reto usando la terminal.
```
wget [URL_DEL_ARCHIVO] -O file
```

2. Analizar el tipo de archivo con el comando `file`. Al estar corrupto, el sistema operativo no sabrá qué es y simplemente devolverá que es de tipo "data".
```
file file
# Output: file: data
```

3. Como las pistas nos indican que debería ser un JPEG y que debemos revisar la cabecera (header), abrimos el archivo con un editor hexadecimal (como `hexeditor` o `bless`).

```
hexeditor file
```

4. Al observar los primeros bytes, notaremos que el archivo comienza con `5C 78 FF E0` (que en representación ASCII se ve como `\xÿà`, seguido de `JFIF`). El formato estándar para los "Magic Bytes" de una cabecera JPEG válida es `FF D8 FF E0`.
    
5. Dentro del editor hexadecimal, debemos sobrescribir los dos primeros bytes corruptos (`5C 78`) por los bytes correctos para un JPEG (`FF D8`).
    
6. Guardamos los cambios en el editor hexadecimal (en `hexeditor`, presiona `Ctrl + X`, luego `Y` para guardar).
    
7. Verificamos que el archivo ahora sí es reconocido como imagen y lo abrimos para leer la bandera que está escrita en ella.
    

```
file file
# Output esperado: file: JPEG image data, JFIF standard...
xdg-open file
```

**Flag**: academy{r3st0r1ng_th3_by73s_d28873c8}

#### Notas Adicionales

- Los **Magic Bytes** o firmas de archivo son los primeros números hexadecimales en un archivo. Sirven para que el sistema operativo identifique el tipo de formato real sin importar la extensión que tenga el archivo (como `.jpg`, `.txt`, etc.).
    
- Al reparar manualmente el encabezado de un archivo a su formato correspondiente (en este caso JPEG), logramos que los visores de imágenes estándar puedan interpretarlo para poder visualizar su contenido de forma normal.
    

#### Referencias

- [List of file signatures / Magic Bytes - Wikipedia](https://en.wikipedia.org/wiki/List_of_file_signatures "null")
    
- [Comando Hexeditor - Ubuntu Manpage](https://manpages.ubuntu.com/manpages/trusty/man1/hexeditor.1.html "null")