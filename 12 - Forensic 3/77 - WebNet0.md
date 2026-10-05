### Descripción

### Solución
1. Descargar los archivos del reto con wget 

2. Instalamos ssldump
```
~/cylab via 🐍 v3.13.5 
❯ sudo apt install ssldump
```

3. En la carpeta donde esten los archivos que descargamos vamos a ejecutar el comando:
```
~/cylab via 🐍 v3.13.5 took 3s 
➜ ssldump -r webnet0-capture.pcap -k picopico.key -d | grep academy -A 2
    61 67 3a 20 61 63 61 64 65 6d 79 7b 6e 6f 6e 67    ag: academy{nong
    73 68 69 6d 2e 73 68 72 69 6d 70 2e 63 72 61 63    shim.shrimp.crac
    6b 65 72 73 7d 0d 0a 43 6f 6e 74 65 6e 74 2d 4c    kers}..Content-L
Cleaned 3 remaining connection(s) from connection pool
```


**Flag**: academy{nongshim.shrimp.crackers}
### Notas Adicionales
- -A 2 → sirve para que grep nos de los siguientes 2 renglones, porque solo con grep no sale la flag completa
### Referencias