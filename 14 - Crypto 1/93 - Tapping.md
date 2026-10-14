### Descripción
Theres tapping coming in from the wires.

Hints:
1. [What kind of encoding uses dashes and dots?](https://en.wikipedia.org/wiki/Morse_code)
2.  The flag is in the format academy{}
### Solución
1. Entrar al servidor y pasar su salida a un archivo: 
```
~/cylab/crypto 
➜ nc chatelaine.cylabacademy.net 15515 > codigo_m.txt
```

2. Ver el contenido del archivo y copiarlo:
```
cat codigo_m.txt
```

3. Pasamos la salida a un decodificador de codigo morse y ya

**Flag**: academy{m0rs3c0d31sfun178da798}
### Notas Adicionales

### Referencias