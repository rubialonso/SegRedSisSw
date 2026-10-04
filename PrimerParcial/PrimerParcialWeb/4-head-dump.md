**Descripción:**
Welcome to the challenge! In this challenge, you will explore a web application and find an endpoint that exposes a file containing a hidden flag.

The application is a simple blog website where you can read articles about various topics, including an article about API Documentation. Your goal is to explore the application and find the endpoint that generates files holding the server’s memory, where a secret flag is hidden. The website is running [picoCTF News](http://chatelaine.cylabacademy.net:26288/).
**Solución 1:**
voy al sitio y explorando un poco veo que un enlace "API documentation" lleva a otra pagina
![[Pasted image 20261003215259.png]]

una vez en esa pagina voy abajo del todo y en **Diagnosing** voy a headhump lo ejecuto y descargo el archivo de una captura que hay
![[Pasted image 20261003215434.png]]
ahora hago por ver el contenido del archivo pero mas especificamente por la bandera así que filtro por la palabra "academy"

como el documento es una sola linea continua tuve que hacer el siguiente comando para que buscara solo la palabra academy que contuviera parentesis y demas texto entre ellos
![[Pasted image 20261003221715.png]]
academy{Pat!3nt_15_Th3_K3y_abc961cc}

**Solución 2:**

**Referencias:**  


**Notas:**