### Descripción
  Do you know how to move between directories and read files in the shell? Start the container, ssh to it, and then ls once connected to begin.
  
Login via `ssh` as `ctf-player` with the password, `8c606eb1` on the host `wily-courier.picoctf.net` and port `63153`.

Pista:  Finding a cheatsheet for bash would be really helpful!
### Solución
```
ssh ctf-player@wily-courier.picoctf.net -p 63153

ctf-player@pico-chall$ ls
1of3.flag.txt  instructions-to-2of3.txt
ctf-player@pico-chall$ cat 1of3.flag.txt 
picoCTF{xxsh_

cat instructions-to-2of3.txt 
Next, go to the root of all things, more succinctly `/`
ctf-player@pico-chall$ cd /
ctf-player@pico-chall$ ls
2of3.flag.txt  boot	 dev  home			lib	media  opt   root  sbin  sys  usr
bin	      challenge  etc  instructions-to-3of3.txt  lib64	mnt    proc  run   srv	tmp  var
ctf-player@pico-chall$ cat 2of3.flag.txt 
0ut_0f_//4t3r_

ctf-player@pico-chall$ cat instructions-to-3of3.txt 
Lastly, ctf-player, go home... more succinctly `~`
ctf-player@pico-chall$ cd ~
ctf-player@pico-chall$ ls
3of3.flag.txt  drop-in
ctf-player@pico-chall$ cat 3of3.flag.txt 
0b24fc4f}ctf-player@pico-chall$ 

```

**Flag**: picoCTF{xxsh_0ut_0f_//4t3r_0b24fc4f}
### Notas Adicionales
cd /  te lleva a la carpeta raiz
cd ~ te lleva a tu home sin importar en que carpeta estes parado

### Referencias