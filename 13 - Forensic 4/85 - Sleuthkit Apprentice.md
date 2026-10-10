### Descripción
Download this disk image and find the flag.

Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.
### Solución
1. Primero se descarga el archivo comprimido del reto desde el servidor y se utiliza `gzip` para descomprimir la imagen de disco en formato `.img`:
```
wget https://challenge-files.cylabacademy.net/library/135adeee1de1ceb2e2838061773078678e93ff1d16535b39a17481b2ba5868ff/disk.flag.img.gz
gzip -d disk.flag.img.gz
```

2. Para analizar la estructura del disco se utiliza la herramienta `mmls` de **The Sleuth Kit**. Esto permite identificar las particiones existentes y obtener el sector de inicio (_offset_) de cada una:
```
mmls disk.flag.img
```

```
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000206847   0000204800   Linux (0x83)
003:  000:001   0000206848   0000360447   0000153600   Linux Swap / Solaris x86 (0x82)
004:  000:002   0000360448   0000614399   0000253952   Linux (0x83)
```

De la salida anterior se observa que la partición Linux principal se ubica en el sector de inicio **`360448`**.

3. Con el offset identificado (`-o 360448`), se utiliza `fls` con la opción `-r` para realizar un listado recursivo del sistema de archivos, filtrando el resultado mediante `grep` para localizar referencias al archivo de la bandera:
```
fls -o 360448 -r disk.flag.img | grep -i "flag"
```

```
++ r/r * 2082(realloc):	flag.txt
++ r/r 2371:	flag.uni.txt
```

#### Análisis de Inodes encontrados:

- **Inode 2082 (`flag.txt`):** Presenta la marca `*` y la etiqueta `(realloc)`, lo que indica que se trata de un archivo eliminado cuyos bloques de datos fueron sobrescritos/reutilizados por el sistema de archivos. Al intentar extraerlo con `icat` sólo devolvió basura residual:
    ```
    icat -o 360448 disk.flag.img 2082
    # Salida: 3.449677            13.056403
    ```
    
- **Inode 2371 (`flag.uni.txt`):** Es un archivo existente e intacto en el sistema de archivos.

4. Extracción del Archivo Válido
Se ejecuta `icat` apuntando al inode **`2371`** para leer el contenido directo de los bloques asignados a ese archivo:
```
icat -o 360448 disk.flag.img 2371

academy{by73_5urf3r_217f681f}
```

**Flag**: academy{by73_5urf3r_217f681f}
### Notas Adicionales

### Referencias