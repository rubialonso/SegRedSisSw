### Descripción

We found this file. Recover the flag. `tunn3l_v1s10n`

### Solución

**1. Identificación y reparación del encabezado BMP**
Después de descargar el archivo, al inspeccionar sus primeros bytes me di cuenta de que se trataba de una imagen en formato BMP (Bitmap Image). Sin embargo, el archivo no se podía abrir de forma nativa.

Busqué en línea el mapa hexadecimal estándar de un archivo BMP para comparar el formato de los encabezados. Al hacer la comparación, noté que los bytes que definen la ubicación de los datos de la imagen y el tamaño de la cabecera tenían valores incorrectos (figuraban como `BA D0 00 00` en lugar de los valores por defecto).

Para solucionar esto, descargué y utilicé **GHex**. La interfaz gráfica evita tener que calcular los desplazamientos manualmente. Usando GHex, modifiqué los bytes corruptos para dejarlos como los de un BMP sano:

- En el offset `0x0A` (que indica dónde empiezan los pixeles), cambié los bytes a `36 00 00 00`.
- En el offset `0x0E` (el tamaño del DIB header), los cambié a `28 00 00 00`.

**2. Análisis de metadatos de la imagen recortada**
Tras guardar los cambios, el archivo finalmente se pudo abrir. Sin embargo, en la imagen solo se veía una pequeña parte superior (parecía un falso paisaje), lo que indicaba que la imagen estaba recortada y ocultaba información.

Para saber cuánto debía medir realmente y ver si necesitábamos modificar más bytes, revisé sus metadatos utilizando **ExifTool**. El resultado de la terminal arrojó que la imagen tenía actualmente un ancho de 1134 y un alto de 306.  

**3. Ajuste de la altura desde el código hexadecimal**
Como el objetivo era hacer la imagen más alta para revelar el contenido oculto, utilicé la consola de Python como conversor para pasar la nueva altura deseada a formato hexadecimal.

Decidí probar con una altura de 850. En Python, al convertir 850 a hexadecimal obtenemos `0x0352`, que escrito en formato _little-endian_ (el formato que leen estos archivos) se traduce a los bytes `52 03 00 00`. Volví a abrir la imagen en GHex, me dirigí al offset correspondiente a la altura de la imagen (`0x16`) y reemplacé los valores originales por estos nuevos bytes.

**4. Deducción de la bandera**
Después de probar varias combinaciones en el editor hexadecimal, comprobé que el límite máximo al que podía expandir la imagen era un ancho de 1134 y una altura de 850.

Al visualizar la imagen resultante con estas dimensiones máximas, noté que no importaba lo que hiciera, no se podía ver toda la bandera con claridad. Esto se debe a que al actualizar este reto, la imagen de la bandera fue cortada a nivel de datos sin considerar que ya no bastaría con modificar las dimensiones lógicas en la cabecera.

Aun así, con los fragmentos de caracteres que pude revelar en la imagen renderizada y apoyándome en búsquedas en línea de la versión original del reto, pude deducir el resto del texto.

**Flag:** academy{qu1t3_a_v13w_2020}

### Notas adicionales 

### Referencias
https://www.youtube.com/watch?v=d63buMlAUHM&t=4s