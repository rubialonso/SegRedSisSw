### Descripción
Fix the syntax error in the Python script to print the flag.

  Hints
- Are equality and assignment the same symbol?
- To view the file in the webshell, do: `$ nano fixme2.py`
- To exit `nano`, press Ctrl and x and follow the on-screen prompts.
- The `str_xor` function does not need to be reverse engineered for this challenge.
### Solución
```
~/cylab via 🐍 v3.13.5 
➜ wget https://artifacts.picoctf.net/c/5/fixme2.py

~/cylab via 🐍 v3.13.5 
➜ python fixme2.py
  File "/home/rubi/cylab/fixme2.py", line 22
    if flag = "":
       ^^^^^^^^^
SyntaxError: invalid syntax. Maybe you meant '==' or ':=' instead of '='?

~/cylab via 🐍 v3.13.5 
❯ nano fixme2.py

```

Luego corregi poniendo un signo de = extra para que pudiera hacer la comparacion con ==
```
~/cylab via 🐍 v3.13.5 took 49s 
➜ nano fixme2.py

~/cylab via 🐍 v3.13.5 took 11s 
➜ python fixme2.py
That is correct! Here's your flag: picoCTF{3qu4l1ty_n0t_4551gnm3nt_4863e11b}
```

**Flag**: picoCTF{3qu4l1ty_n0t_4551gnm3nt_4863e11b}
### Notas Adicionales

### Referencias