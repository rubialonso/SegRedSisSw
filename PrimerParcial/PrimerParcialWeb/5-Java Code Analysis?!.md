**Descripción:**
BookShelf Pico, my premium online book-reading service.

I believe that my website is super secure. I challenge you to prove me wrong by reading the 'Flag' book! Here are the credentials to get you started:

- Username: "user"
- Password: "user"

Source code can be downloaded [here](https://challenge-files.cylabacademy.net/library/28ee57c47715d1e39801d61bf462dd6cece648dba9dcf4e35332e849b863359f/bookshelf-pico.zip).

Website can be accessed [here!](http://xebec.cylabacademy.net:17667/).
**Solución 1:**
voy a la pagina y me logeo
![[Pasted image 20261003222315.png]]
también reviso el codigo que descargue y viendo el archivo "SectretGenerator.java"
![[Pasted image 20261003223151.png]]
veo el return "1234";
luego de haber hecho log en la pagina voy a libro llamado "flag", abro inspeccionar elementos y en la sección de almacenamiento y almacenamiento localr copio el "auth-token"
![[Pasted image 20261003223551.png]]
con ese token voy a una pagina para cambiar el acceso de este
![[Pasted image 20261003223833.png]]
lo edite para que quedara de la siguiente manera:
![[Pasted image 20261003224949.png]]
ahora pego el token en "auth-token" y el payload en "token-payload"
![[Pasted image 20261003225624.png]]
y ahí esta la bandera 
![[Pasted image 20261003225648.png]]
academy{w34k_jwt_n0t_g00d_1107047a}
**Solución 2:**

**Referencias:**  
https://www.youtube.com/watch?v=AT61XquM3mI

**Notas:**
- se pueden modificar los tokens de acceso a una pagina analizandolos o cambiandolos en sitios como "jwt.io"