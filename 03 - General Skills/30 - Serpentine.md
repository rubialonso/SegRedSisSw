### Descripción
  Find the flag in the Python script!
  Hints
- Try running the script and see what happens
- In the webshell, try examining the script with a text editor like `nano`
- To exit `nano`, press Ctrl and x and follow the on-screen prompts.
- The `str_xor` function does not need to be reverse engineered for this challenge.
### Solución
Descargar el archivo, para arreglar el codigo haciendo que la opcion b diera a la función print_flag() para que imprimiera la bandera y listoo!!
```
~/cylab via 🐍 v3.13.5 took 5s 
➜ wget https://artifacts.picoctf.net/c/37/serpentine.py

~/cylab via 🐍 v3.13.5 
➜ python serpentine.py

Welcome to the serpentine encourager!

a) Print encouragement
b) Print flag
c) Quit

What would you like to do? (a/b/c) b

Oops! I must have misplaced the print_flag function! Check my source code!


a) Print encouragement
b) Print flag
c) Quit

What would you like to do? (a/b/c) c

~/cylab via 🐍 v3.13.5 took 15s 
➜ nano serpentine.py

~/cylab via 🐍 v3.13.5 took 48s 
➜ python serpentine.py
Welcome to the serpentine encourager!

a) Print encouragement
b) Print flag
c) Quit

What would you like to do? (a/b/c) b
picoCTF{7h3_r04d_l355_7r4v3l3d_8e47d128}

```

**Flag**: picoCTF{7h3_r04d_l355_7r4v3l3d_8e47d128}
### Notas Adicionales

### Referencias