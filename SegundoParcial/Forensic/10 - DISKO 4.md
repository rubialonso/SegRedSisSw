**Descripción:**
Can you find the flag in this disk image? This time I deleted the file! Let see you get it now! Download the disk image [here](https://challenge-files.cylabacademy.net/library/eb382e7a661cefeb2a260ce85a423ae53331e859032f82b2a8375fe1ce68c2e8/disko-4.dd.gz).

**Solución1:**
primero descargo el archivo en mi pc :
```
sdlmxd@sdlmxd-HP-Laptop-15-dw0xxx:~/disko4$ wget https://challenge-files.cylabacademy.net/library/eb382e7a661cefeb2a260ce85a423ae53331e859032f82b2a8375fe1ce68c2e8/disko-4.dd.gz
```
luego lo descomprimo de la siguiente manera :
```
sdlmxd@sdlmxd-HP-Laptop-15-dw0xxx:~/disko4$ gunzip disko-4.dd.gz
```
buscando en los archivos borrados  del disco encontramos lo siguiente:
```
sdlmxd@sdlmxd-HP-Laptop-15-dw0xxx:~/disko4$ fls -p -r disko-4.dd | grep -e "*"
r/r * 522629:	log/messages
r/r * 532021:	log/dont-delete.gz

```
ahora recuperare el segundo archivo:
```
sdlmxd@sdlmxd-HP-Laptop-15-dw0xxx:~/disko4$ icat disko-4.dd 532021 > dont-delete.gz

```
lo leemos con zcat: 
```
sdlmxd@sdlmxd-HP-Laptop-15-dw0xxx:~/disko4$ zcat dont-delete.gz
Here is your flag
academy{d3l_d0n7_h1d3_w3ll_d257c742}

```
obtuvimos la bandera 
academy{d3l_d0n7_h1d3_w3ll_d257c742}
**Solución2:**

**Notas adicionales:**

**Referencias:**
- https://www.youtube.com/watch?v=5y5v8scP2uQ