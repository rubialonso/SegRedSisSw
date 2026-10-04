### Descripción
Someone's commits seems to be preventing the program from working. Who is it?

Hints
- In collaborative projects, many users can make many changes. How can you see the changes within one file?
- Read the chapter on Git from the picoPrimer [here](https://primer.picoctf.org/#_git_version_control).
- You can use `python3 <file>.py` to try running the code, though you won't need to for this challenge.
### Solución
1. Descargar el archivo
2. Descomprimir el archivo
3. Revisar que contiene la carpeta
4. Revisar el log especifico para ese archivo que esta ahi y ya

```
~/cylab via 🐍 v3.13.5 
❯ wget https://artifacts.picoctf.net/c_titan/159/challenge.zip

~/cylab via 🐍 v3.13.5 
❯unzip challenge.zip

~/cylab via 🐍 v3.13.5 
➜ cd drop-in

drop-in on  master via 🐍 v3.13.5 
➜ ls
message.py

drop-in on  master via 🐍 v3.13.5 
❯ git log -- message.py
commit 23e9d4ce78b3cea725992a0ce6f5eea0bf0bcdd4
Author: picoCTF{@sk_th3_1nt3rn_81e716ff} <ops@picoctf.com>
Date:   Tue Mar 12 00:07:15 2024 +0000

    optimize file size of prod code

commit 3ce5c692e2f9682a866c59ac1aeae38d35d19771
Author: picoCTF <ops@picoctf.com>
Date:   Tue Mar 12 00:07:15 2024 +0000

    create top secret project
```
**Flag**: picoCTF{@sk_th3_1nt3rn_81e716ff}
### Notas Adicionales
- git log → muestra el historial de cambios generales
- git log -- message.py → es para ver los cambios especificos para ese archivo

### Referencias
https://primer.picoctf.org/#_git_version_control
https://cloud.donweb.com/borrar-carpetas-y-archivos-en-linux/
https://initialcommit.com/blog/git-log