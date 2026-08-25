### Descripción
  Can you find the flag in [file](https://challenge-files.picoctf.net/c_fickle_tempest/53c039e64942b1c4334781c4987ba7e2ba54f0b2bf39f52c65f3a65dfcbf4194/strings) without running it?
### Solución
```
wget https://challenge-files.picoctf.net/c_fickle_tempest/53c039e64942b1c4334781c4987ba7e2ba54f0b2bf39f52c65f3a65dfcbf4194/strings

strings strings | grep pico
```

**Flag**: picoCTF{5tRIng5_1T_A1b9ECAa}
### Notas Adicionales
strings: elimina caracteres extraños para filtrar solo texto, muestra solo las cadenas (caracteres imprimibles) en un archivo binario (no texto)

### Referencias
https://labex.io/es/tutorials/linux-linux-strings-command-with-practical-examples-422934