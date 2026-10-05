### Descripción

### Solución
1. Descargar los archivos con wget
2. Abrir el pcap en wireshark
```
~/cylab/webnet1 
➜ wireshark webnet1-capture.pcap
```
1. Pasar el key que nos dieron al protocolo TLS. Para eso primero entramos a Edición > Preferencias > Protocolos > TLS > Importamos la key.
2. Luego en la seccion de Archivo > Exportar Objetos > HTTP vamos a guardar el archivo 'vulture.jpg'
3. En la terminal vamos a la carpeta donde esta el archivo, estando ahi ejecutamos el siguiente comando, y en la salida en la propiedad de Artista nos dará la flag:
```
~/cylab/webnet1 
❯ exiftool vulture.jpg 
.
.
.
Artist                          : academy{honey.roasted.peanuts}
```

**Flag**: academy{honey.roasted.peanuts}
### Notas Adicionales

### Referencias