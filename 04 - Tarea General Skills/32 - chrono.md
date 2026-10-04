### Descripción
How to automate tasks to run at intervals on linux servers?
### Solución
Use ssh to connect to this server:

Server: saturn.picoctf.net Port: 50123 Username: picoplayer Password: ENAFb6zfzn

ssh picoplayer@saturn.picoctf.net -p 50123 

```
~ via 🐍 v3.13.5 
➜ ssh picoplayer@saturn.picoctf.net -p 50123 

picoplayer@challenge:~$ cat /etc/crontab
# picoCTF{Sch3DUL7NG_T45K3_L1NUX_1d781160}
```

**Flag**: picoCTF{Sch3DUL7NG_T45K3_L1NUX_1d781160}
### Notas Adicionales
**Cron** es un programa en Linux/Unix que permite **ejecutar tareas automáticamente en momentos programados**

Le dices a cron: "ejecuta este script todos los días a las 3 AM" (o cada 5 minutos, cada domingo, el día 1 de cada mes, etc.), y él se encarga de hacerlo en segundo plano, indefinidamente.

`/etc/crontab` es el archivo donde se configuran las tareas programadas del sistema.

### Referencias
https://www.digitalocean.com/community/tutorials/how-to-use-cron-to-automate-tasks-ubuntu-1804