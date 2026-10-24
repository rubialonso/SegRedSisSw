### Descripción

The Network Operations Center (NOC) of your local institution picked up a suspicious file, they're getting conflicting information on what type of file it is. They've brought you in as an external expert to examine the file. Can you extract all the information from this strange file? [flag2of2-final.pdf](https://challenge-files.cylabacademy.net/library/fbc63a04a60481fd928460868dee05e60ab0bcdf6582dc786ddf1f1cec3f8c8b/flag2of2-final.pdf)

### Solución

1. Descargar el archivo (nombre `flag2of2-final.pdf`), pero `file` lo identifica como **PNG**, no PDF — es un polyglot.
2. Se inspecciona el binario buscando ambas firmas:

```python
   d = open('flag2of2-final.pdf','rb').read()
   d.find(b'%PDF')   # -> 453  (un PDF empieza en el byte 453)
   d[:20]            # b'\x89PNG\r\n\x1a\n...' (empieza como PNG)
```

3. Se separa el archivo en sus dos partes:
    - **Parte PNG:** desde el inicio hasta el chunk `IEND` (byte 453).
    - **Parte PDF:** desde el byte 453 (`%PDF-...`) hasta el final.
```python
   idx_iend = d.find(b'IEND')
   open('parte1.png','wb').write(d[:idx_iend+8])
   open('parte2.pdf','wb').write(d[453:])
```

4. Al abrir `parte1.png` se ve una imagen con el texto `academy{f1u3n7_` (primera mitad de la flag, de ahí el nombre "flag**2of2**").
5. Al extraer el texto de `parte2.pdf` con `pdftotext` se obtiene la segunda mitad: `1n_pn9_&_pdf_96385309}`.
6. Uniendo ambas partes se arma la flag completa.

**Flag:** `academy{f1u3n7_1n_pn9_&_pdf_96385309}`

### Notas Adicionales

Un "polyglot" es un archivo válido simultáneamente en dos (o más) formatos distintos, aprovechando que cada formato ignora los bytes que no reconoce como propios (un lector de PNG se detiene en `IEND`; un lector de PDF busca `%PDF` donde sea que empiece). El reto estaba literalmente dividido en dos mitades de la flag, una por cada "personalidad" del archivo.

### Referencias