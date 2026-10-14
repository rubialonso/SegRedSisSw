### Descripción
I found this cipher in an old book.

Hints:
1. There are tools that make this easy.
2. Perhaps looking at history will help
### Solución
1. Nos conectamos al servidor y le pasamos la salida a un archivo:
```
~/cylab/crypto 
➜ nc xebec.cylabacademy.net 14710 > message.txt
```

2. Abrimos el archivo y copiamos el contenido
3. Entramos a la página: https://www.guballa.de/vigenere-solver buscando viegenere solver y pegamos el contenido del archivo.
4. En la salida buscamos la flag

**Flag**: academy{b311a50_0r_v1gn3r3_c1ph3r181ba1aa}
### Notas Adicionales

### Referencias