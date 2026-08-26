### Descripción
  Fix the syntax error in this Python script to print the flag.
Hints
- Indentation is very meaningful in Python
- To view the file in the webshell, do: `$ nano fixme1.py`
- To exit `nano`, press Ctrl and x and follow the on-screen prompts.
- The `str_xor` function does not need to be reverse engineered for this challenge.
### Solución
```
➜ wget https://artifacts.picoctf.net/c/27/fixme1.py

~/cylab via 🐍 v3.13.5 took 2m20s 
➜ python fixme1.py
  File "/home/rubi/cylab/fixme1.py", line 20
    print('That is correct! Here\'s your flag: ' + flag)
IndentationError: unexpected indent

~/cylab via 🐍 v3.13.5 
❯ nano fixme1.py
```

Luego en esa linea solo le quite la identacion para que no estuviera dentro de un bloque y ya solo lo ejecute de nuevo

```
~/cylab via 🐍 v3.13.5 took 2m24s 
➜ python fixme1.py
That is correct! Here's your flag: picoCTF{1nd3nt1ty_cr1515_182342f7}
```

**Flag**: picoCTF{1nd3nt1ty_cr1515_182342f7}
### Notas Adicionales
- En Pyhton los espacios / identaciones ubican a una linea dentro de un bloque de codigo, es sensible a espacios

### Referencias