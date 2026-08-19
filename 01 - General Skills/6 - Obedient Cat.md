### Descripción
  This file has a flag in plain sight (aka "in-the-clear").

	file: flag

Pistas:
1 Any hints about entering a command into the Terminal (such as the next one), will start with a '$'... everything after the dollar sign will be typed (or copy and pasted) into your Terminal.

2 To get the file accessible in your shell, enter the following in the Terminal prompt: $ wget and a link to the flag. The link can be copied from the details section.

3 $ man cat
### Solución
Ejecutar los siguientes comandos en la terminal:
```
wget https://challenge-files.picoctf.net/c_wily_courier/eaf5dbd32acd6d3318c402247156552fc789474a5328dc436404e97932ab34c3/flag

cat flag
```

**Flag**: picoCTF{s4n1ty_v3r1f13d_9b8fa0bc}
### Solución 2
Una vez descargado el archivos ejecutar el comando:
```
grep "$" flag
```

**Flag**: picoCTF{s4n1ty_v3r1f13d_9b8fa0bc}

### Notas Adicionales
wget: este comando se usa para descargar archivos
cat: se usa para ver el contenido de un archivo

### Referencias
