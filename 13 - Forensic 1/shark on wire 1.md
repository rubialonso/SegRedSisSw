### Descripción
We found this packet capture. Recover the flag.
Hints:
* Try using a tool like Wireshark, What are streams?
### Solución
Checar que este instalado wireshark, sino instalarlo
```
~/cylab took 44s 
➜ which wireshark
/usr/bin/wireshark
```

Con wget descargamos el archivo del pcap
```
~ 
➜ wget https://challenge-files.cylabacademy.net/library/e64f2c2aaf9bf531af7be1787c1407c47a4cc7b57f251d5108a1151e9721a2d6/shark-on-wire-1-capture.pcap
```

Ejecutamos wireshark y luego abrimos el archivo shark-on-wire-1-capture.pcap

Vamos a la pestaña de Analizar > Seguir > UDP Stream

Ya estando ahí cambiamos la secuencia a 6 y ahi estará la flag

**Flag**: academy{StaT31355_636f6e6e}
### Notas Adicionales


### Referencias