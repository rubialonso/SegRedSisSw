### Descripción
Download this disk image, find the key and log into the remote machine.

Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.

- [Download disk image](https://challenge-files.cylabacademy.net/library/32b4f7450d7368e22562f75fed35fecd7bdfa2172559a90a42a149e27d781464/disk.img.gz)
- Remote machine: `ssh -i key_file -p 37126 ctf-player@xebec.cylabacademy.net`
## Solución
#### 1. Descarga y descompresión de la imagen
Se trabaja en `/tmp` como indica el enunciado.
```bash
cd /tmp/operationoni
wget https://challenge-files.cylabacademy.net/library/<hash>/disk.img.gz
gzip -d disk.img.gz
```

#### 2. Análisis de la tabla de particiones

Con `mmls` (The Sleuth Kit) se listan las particiones de la imagen:

```bash
mmls disk.img

DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000206847   0000204800   Linux (0x83)
003:  000:001   0000206848   0000471039   0000264192   Linux (0x83)
```

Hay dos particiones Linux. La segunda (offset `206848`) es la más grande y contiene el sistema de archivos con los directorios de usuario.

#### 3. Búsqueda de la llave SSH

Se recorre el sistema de archivos de la segunda partición de forma recursiva con `fls` y se filtran las coincidencias con `ssh`:

```bash
fls -o 206848 -r disk.img | grep -i "ssh"

+ d/d 3916:	.ssh
```

Aparece un directorio `.ssh` (inodo `3916`). Se lista su contenido indicando el inodo:
```bash
fls -o 206848 disk.img 3916

r/r 2345:	id_ed25519
r/r 2346:	id_ed25519.pub
```

Se encuentra un par de llaves SSH: la privada (`id_ed25519`, inodo `2345`) y la pública (`id_ed25519.pub`, inodo `2346`).
#### 4. Extracción de la llave privada
Con `icat` se extrae el contenido de un archivo a partir de su inodo:
```bash
icat -o 206848 disk.img 2345 > key
chmod 600 key
```

El `chmod 600` es necesario: SSH rechaza llaves privadas con permisos demasiado abiertos.

#### 5. Acceso a la máquina remota
```bash
ssh -i key -p 37126 ctf-player@xebec.cylabacademy.net
```

Una vez dentro, la flag está en el home del usuario:

```bash
ctf-player@challenge:~$ ls
flag.txt
ctf-player@challenge:~$ cat flag.txt
academy{k3y_5l3u7h_f52dbc2c}
```

**Flag:** academy{k3y_5l3u7h_f52dbc2c}
## Notas Adicionales

## Referencias
