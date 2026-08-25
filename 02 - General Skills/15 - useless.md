### Descripción
There's an interesting script in the user's home directory

The work computer is running SSH. We've been given a script which performs some basic calculations, explore the script and find a flag.

`Hostname: saturn.picoctf.net Port: 54032 Username: picoplayer Password: password`
### Solución
```
ssh picoplayer@saturn.picoctf.net -p 54032

picoplayer@saturn.picoctf.net's password: 

picoplayer@challenge:~$ ls
useless

picoplayer@challenge:~$ man useless
```

**Flag**: picoCTF{us3l3ss_ch4ll3ng3_3xpl0it3d_6194}
### Notas Adicionales
* ssh remote_username@remote_host -p port:  es la sintaxis para acceder por medio de ssh

### Referencias
* https://www.digitalocean.com/community/tutorials/how-to-use-ssh-to-connect-to-a-remote-server-es
* https://wetopi.com/es/conectar-por-ssh/