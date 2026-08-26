### Descripción
  Can you crack the password to get the flag?

Download the password checker [here](https://artifacts.picoctf.net/c/10/level1.py) and you'll need the encrypted [flag](https://artifacts.picoctf.net/c/10/level1.flag.txt.enc) in the same directory too.

Hints
- To view the file in the webshell, do: `$ nano level1.py`
- To exit `nano`, press Ctrl and x and follow the on-screen prompts.
- The `str_xor` function does not need to be reverse engineered for this challenge.
### Solución

```
~/cylab via 🐍 v3.13.5 
❯ wget https://artifacts.picoctf.net/c/10/level1.py

~/cylab via 🐍 v3.13.5 
➜ wget https://artifacts.picoctf.net/c/10/level1.flag.txt.enc

~/cylab via 🐍 v3.13.5 
➜ nano level1.py

~/cylab via 🐍 v3.13.5 took 1m18s 
➜ python level1.py
Please enter correct password for flag: 691d
Welcome back... your flag, user:
picoCTF{545h_r1ng1ng_56891419}
```

En el archivo venia la contraseña :p ya nomás se reviso con nano

**Flag**: picoCTF{545h_r1ng1ng_56891419}
### Notas Adicionales

### Referencias