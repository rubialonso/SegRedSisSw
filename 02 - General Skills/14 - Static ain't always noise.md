### Descripción
  Can you look at the data in this binary? The bash script might help!

### Solución 1
```
wget https://challenge-files.picoctf.net/c_wily_courier/b6c2dd492eb053dfbb3fcfa9eb142c8d11f6a00c0691031fc92b045d65b6e56a/static

wget https://challenge-files.picoctf.net/c_wily_courier/b6c2dd492eb053dfbb3fcfa9eb142c8d11f6a00c0691031fc92b045d65b6e56a/ltdis.sh

strings static | grep pico
picoCTF{d15a5m_t34s3r_20335e41}
```

**Flag**: picoCTF{d15a5m_t34s3r_20335e41}

### Solución 2

```
➜ file ltdis.sh
ltdis.sh: Bourne-Again shell script, ASCII text executable

~ 
➜ file static
static: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=9a00d4dca6b92d22aa0cd1fceffa4ed7495b8534, for GNU/Linux 3.2.0, not stripped

~ 
➜ cat ltdis.sh
#!/bin/bash
. 
.
.

else
	echo "Disassembly failed!"
	echo "Usage: ltdis.sh <program-file>"
	echo "Bye!"
fi

~ 
➜ls -la

~ 
➜chmod +x ltdis.sh


~ 
➜ ./ltdis.sh
Attempting disassembly of  ...
objdump: «a.out»: No hay tal fichero
objdump: la sección «.text» se menciona en una opción -j, pero no se encuentra en ningún fichero de entrada
Disassembly failed!
Usage: ltdis.sh <program-file>
Bye!

~ 
➜ ./ltdis.sh static
Attempting disassembly of static ...
Disassembly successful! Available at: static.ltdis.x86_64.txt
Ripping strings from binary with file offsets...
Any strings found in static have been written to static.ltdis.strings.txt with file offset


~ 
➜ cat static.ltdis.strings.txt | grep pico
   3020 picoCTF{d15a5m_t34s3r_20335e41}
```

### Notas Adicionales

hay que revisar los permisos de los archivos, la solucion se podria encontrar dentro de los ejecutables
### Referencias