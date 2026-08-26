### Descripción
  Can you crack the password to get the flag?

Download the password checker [here](https://artifacts.picoctf.net/c/17/level3.py) and you'll need the encrypted [flag](https://artifacts.picoctf.net/c/17/level3.flag.txt.enc) and the [hash](https://artifacts.picoctf.net/c/17/level3.hash.bin) in the same directory too.

There are 7 potential passwords with 1 being correct. You can find these by examining the password checker script.

Hints
- To view the level3.hash.bin file in the webshell, do: `$ bvi level3.hash.bin`
- To exit `bvi` type `:q` and press enter.
- The `str_xor` function does not need to be reverse engineered for this challenge.
### Solución

Descargar los archivos, luego ver su contenido y como la pista decia que habian 7 potenciales contraseñas entonces se probaron una a una cada contraseña 😿

```
~/cylab via 🐍 v3.13.5 took 2s 
➜ wget https://artifacts.picoctf.net/c/17/level3.py

~/cylab via 🐍 v3.13.5 
➜ wget https://artifacts.picoctf.net/c/17/level3.flag.txt.enc

~/cylab via 🐍 v3.13.5 
➜ wget https://artifacts.picoctf.net/c/17/level3.hash.bin

~/cylab via 🐍 v3.13.5 
➜ cat level3.hash.bin
�mU�]���R�>��W+{
~/cylab via 🐍 v3.13.5 
➜ cat level3.flag.txt.enc  
{c'UT
SVPP
    _hRP]U
~/cylab via 🐍 v3.13.5 
➜ tail level3.py



level_3_pw_check()


# The strings below are 7 possibilities for the correct password. 
#   (Only 1 is correct)
pos_pw_list = ["f09e", "4dcf", "87ab", "dba8", "752e", "3961", "f159"]

~/cylab via 🐍 v3.13.5 
➜ python level3.py
Please enter correct password for flag: f159
That password is incorrect

~/cylab via 🐍 v3.13.5 took 6s 
➜ python level3.py
Please enter correct password for flag: dba8
That password is incorrect

~/cylab via 🐍 v3.13.5 took 11s 
➜ python level3.py
Please enter correct password for flag: f09e
That password is incorrect

~/cylab via 🐍 v3.13.5 took 6s 
➜ python level3.py
Please enter correct password for flag: 4dcf
That password is incorrect

~/cylab via 🐍 v3.13.5 took 6s 
➜ python level3.py
Please enter correct password for flag: 87ab
Welcome back... your flag, user:
picoCTF{m45h_fl1ng1ng_cd6ed2eb}
```

**Flag**: picoCTF{m45h_fl1ng1ng_cd6ed2eb}
### Notas Adicionales

### Referencias