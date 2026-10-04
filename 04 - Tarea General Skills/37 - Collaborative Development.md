### Descripción
My team has been working very hard on new features for our flag printing program! I wonder how they'll work together?

Hints
- `git branch -a` will let you see available branches
- How can file 'diffs' be brought to the main branch? Don't forget to `git config`!
- Merge conflicts can be tricky! Try a text editor like nano, emacs, or vim.
### Solución

```
~/cylab via 🐍 v3.13.5 
➜ wget https://artifacts.picoctf.net/c_titan/70/challenge.zip

~/cylab via 🐍 v3.13.5 took 3s 
➜ unzip challenge.zip

~/cylab via 🐍 v3.13.5 
➜ cd drop-in

drop-in on  main via 🐍 v3.13.5 
➜ ls
flag.py

drop-in on  main via 🐍 v3.13.5 
➜ python flag.py
Printing the flag...

drop-in on  main via 🐍 v3.13.5 
➜ nano flag.py

drop-in on  main via 🐍 v3.13.5 
❯ git branch -a
  feature/part-1
  feature/part-2
  feature/part-3
* main

drop-in on  main via 🐍 v3.13.5 
➜ git checkout feature/part-1
Cambiado a rama 'feature/part-1'

drop-in on  feature/part-1 via 🐍 v3.13.5 
➜ ls
flag.py

drop-in on  feature/part-1 via 🐍 v3.13.5 
➜ cat flag.py
print("Printing the flag...")
print("picoCTF{t3@mw0rk_", end='')
drop-in on  feature/part-1 via 🐍 v3.13.5 
➜ git checkout feature/part-2
Cambiado a rama 'feature/part-2'

drop-in on  feature/part-2 via 🐍 v3.13.5 
➜ cat flag.py
print("Printing the flag...")

print("m@k3s_th3_dr3@m_", end='')
drop-in on  feature/part-2 via 🐍 v3.13.5 
➜ git checkout feature/part-3
Cambiado a rama 'feature/part-3'

drop-in on  feature/part-3 via 🐍 v3.13.5 
➜ cat flag.py
print("Printing the flag...")

print("w0rk_7ffa0077}")
```
**Flag**: picoCTF{t3@mw0rk_m@k3s_th3_dr3@m_w0rk_7ffa0077}
### Notas Adicionales
- git branch -a → sirve para ver todas las ramas del repositorio
- git checkout '< branch >' → se usa para ir especificamente a la rama (igual aplica para el hash de un commit)
### Referencias