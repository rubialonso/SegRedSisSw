### Descripción
Use `srch_strings` from the sleuthkit and some terminal-fu to find a flag in this disk image. [dds1-alpine.flag.img.gz](https://challenge-files.cylabacademy.net/library/0e33413e7b309ae38964211ca09f5c86005b6fe4f2cc95b75ad5b482d98a2d76/dds1-alpine.flag.img.gz)

Hints:
1. Have you ever used `file` to determine what a file was?
2. Relevant terminal-fu in Challenge Library: [https://learn.cylabacademy.org/library/85](https://learn.cylabacademy.org/library/85)
3. Mastering this terminal-fu would enable you to find the flag in a single command: [https://learn.cylabacademy.org/library/48](https://learn.cylabacademy.org/library/48)
4. Using your own computer, you could use qemu to boot from this disk!
### Solución
1. Descargar el archivo del reto, una imagen de disco.
2. Instalamos sleuth.
3. Ahora en la carpeta donde se encuentre el archivo hay que usar el comando y nos dará la flag directamente:
```
~/cylab/diskdisk took 2s 
➜ srch_strings dds1-alpine.flag.img | grep academy
  SAY academy{f0r3ns1c4t0r_n30phyt3_6502313d}
```

**Flag**: academy{f0r3ns1c4t0r_n30phyt3_6502313d}
### Notas Adicionales
- **`srch_strings dds1-alpine.flag.img`**: Es una utilidad de Sleuth Kit (similar al comando estándar `strings` de Linux). Extrae e imprime todas las cadenas de caracteres de texto legible (ASCII/Unicode) que encuentra dentro del archivo de datos binarios `dds1-alpine.flag.img`, escaneando todo el disco byte por byte sin importar si los archivos están borrados, fragmentados o sin sistema de archivos montado.
    
- **`|` (Pipe)**: Redirige toda la salida generada por `srch_strings` hacia la entrada del siguiente comando.
### Referencias