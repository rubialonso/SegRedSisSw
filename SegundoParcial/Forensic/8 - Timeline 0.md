### Descripción
Can you find the flag in this disk image? Wrap what you find in the academy{} flag format. Download the disk image [here](https://challenge-files.cylabacademy.net/library/bf9a20c350075c5863371e078daee1d570d4062902edc8a4a042e02a7cebf161/partition4.img.gz).
### Solución
**1. Descompresión de la imagen de disco**
Las utilidades de TSK requieren analizar la imagen en crudo. El archivo inicial `partition4.img.gz` estaba comprimido, por lo que el primer paso fue extraerlo.

```
gunzip partition4.img.gz
```

**2. Extracción de metadatos (Body File)**
Se utilizó `fls` para recorrer el sistema de archivos de la imagen extraída y listar la información de los archivos y directorios (incluyendo metadatos de tiempo) en un archivo intermedio conocido como _body file_.

```
fls -r -m / partition4.img > body.txt
```

**3. Generación de la línea de tiempo MAC**
Con el archivo `body.txt` generado, se utilizó `mactime` para procesar los datos y crear una línea de tiempo legible y ordenada cronológicamente.

```
mactime -b body.txt > timeline.txt
```

**4. Análisis de la línea de tiempo y detección de anomalías**
Sabiendo que el _timestomping_ suele dejar fechas muy antiguas, se inspeccionaron las primeras líneas del archivo `timeline.txt` (que ordena los eventos del más antiguo al más reciente).

```
head -n 30 timeline.txt
```

**Hallazgo:** En la primera línea del resultado, se identificó un archivo con una fecha de modificación anómala que destaca claramente sobre el resto de los archivos del sistema (que datan de 2021 y 2023):`Tue Jan 01 1985 11:00:00 41 macb r/rrw-r--r-- 0 0 4945 /bin/bcab` El archivo sospechoso es `/bin/bcab` y su número de inodo es el **4945**.

**5. Volcado del contenido del inodo**
Con el número de inodo identificado, se utilizó `icat` para volcar el contenido exacto del bloque de datos asociado a ese archivo directamente en la terminal.

```
icat partition4.img 4945
```

**Salida:** `NzFtMzExbjNfMHU3MTEzcl9oM3JfNDNhMmU3YWYK`

**6. Decodificación de la bandera**
La cadena obtenida es un texto codificado en Base64. Se decodificó pasando la salida estándar a la utilidad `base64`.

```
echo "NzFtMzExbjNfMHU3MTEzcl9oM3JfNDNhMmU3YWYK" | base64 -d
```

**Salida:** `71m311n3_0u7113r_h3r_43a2e7af`

**Flag**: academy{71m311n3_0u7113r_h3r_43a2e7af}
### Notas Adicionales

### Referencias