### Descripción
Can you find the flag in this disk image? Wrap what you find in the academy{} flag format. Download the disk image [here](https://challenge-files.cylabacademy.net/library/0b369ed5974a5e777ca3bc323bd39d75a6f27762a449d16cd2a0ffc08b2a6aa8/timeline-1-partition4.img.gz).

Hints:
1. Create a Sleuthkit MAC timeline
2. Look at recent timestamps
3. Pay close attention to timestamps near an anti-forensic action
4. Filter only new files by grepping for `macb`
### Solución
1. Descargar el archivo con wget y descomprimir la imagen de disco:
```
~/cylab/sp_forensic 
➜ wget https://challenge-files.cylabacademy.net/library/0b369ed5974a5e777ca3bc323bd39d75a6f27762a449d16cd2a0ffc08b2a6aa8/timeline-1-partition4.img.gz

~/cylab/sp_forensic 
➜ gunzip timeline-1-partition4.img.gz
```

2. Utilizar The Sleuth Kit (`fls`) para generar el archivo de metadatos (_body file_):
```
~/cylab/sp_forensic 
➜ fls -r -m / timeline-1-partition4.img > body.txt
```

3. Crear la línea de tiempo MAC utilizando `mactime`:

```
~/cylab/sp_forensic 
➜ mactime -b body.txt > timeline.txt
```

4. Filtrar por creaciones o modificaciones absolutas (`macb`) y examinar la actividad reciente. Al revisar los últimos registros, se identifica el archivo malicioso `/etc/chat` (inodo 32716) creado casi al mismo tiempo que una modificación en `/root/.ash_history`:

```
~/cylab/sp_forensic 
➜ grep 'macb' timeline.txt | tail -n 50
                               49 macb r/rrw-r--r-- 0        0        32716    /etc/chat
                             1024 macb d/drwxr-xr-x 0        0        33017    /lib/rc/cache
                                8 macb r/rrw-r--r-- 0        0        33020    /lib/rc/cache/softlevel
                                9 macb r/rrw------- 0        0        4943     /root/.ash_history
```

5. Extraer el contenido del inodo encontrado con `icat` y decodificar la cadena Base64 resultante para obtener el contenido de la bandera:

```
~/cylab/sp_forensic 
➜ icat timeline-1-partition4.img 32716
NTczNDE3aDEzcl83aDRuXzdoM18xNDU3XzU4NTI3YmIyMjIK

~/cylab/sp_forensic 
➜ echo "NTczNDE3aDEzcl83aDRuXzdoM18xNDU3XzU4NTI3YmIyMjIK" | base64 -d
573417h13r_7h4n_7h3_1457_58527bb222
```

**Flag**: academy{573417h13r_7h4n_7h3_1457_58527bb222}

### Notas Adicionales

La modificación coincidente del archivo `/root/.ash_history` representa la "acción anti-forense" mencionada en las pistas. Es una táctica común que los atacantes manipulen o eliminen el historial de comandos del usuario root para evadir la detección inmediatamente después de interactuar con el sistema.

### Referencias