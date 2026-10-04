### Descripción
Find the flag being held on this server to get ahead of the competition

Hints:
- Maybe you have more than 2 choices
- Check out tools like Burpsuite to modify your requests and look at the responses
### Solución
ejecutar en la teminal:
```
~ via 🐍 v3.13.5 took 7s 
➜ curl -s -I http://wily-courier.picoctf.net:59294/
HTTP/1.1 200 OK
Date: Mon, 07 Sep 2026 16:23:52 GMT
Server: Apache/2.4.38 (Debian)
X-Powered-By: PHP/7.2.34
flag: picoCTF{r3j3ct_th3_du4l1ty_8b13f07}
Content-Type: text/html; charset=UTF-8
```

**Flag**: picoCTF{r3j3ct_th3_du4l1ty_8b13f07}
### Notas Adicionales
Los comandos de cURL están diseñados para funcionar como una forma de verificar la conectividad a las URL y como una gran herramienta para transferir datos.

curl -I → sirve para obtener la información del head
### Referencias
https://www.hostinger.com/mx/tutoriales/comando-curl/