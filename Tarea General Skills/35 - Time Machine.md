### Descripción
What was I last working on? I remember writing a note to help me remember...

Hints
- The `cat` command will let you read a file, but that won't help you here!
- Read the chapter on Git from the picoPrimer [here](https://primer.picoctf.org/#_git_version_control).
- When committing a file with git, a message can (and should) be included.
### Solución

- Se hizo lo mismo que con Commitment Issues excepto por el cat, al parecer el archivo tenia ASCII text, pero esa no era la respuesta habia que usar git log y con eso mostro la flag
```
➜ wget https://artifacts.picoctf.net/c_titan/66/challenge.zip

➜ unzip challenge.zip 

~/cylab via 🐍 v3.13.5 
➜ cd drop-in

drop-in on  master 
➜ ls
message.txt


drop-in on  master 
➜ file message.txt
message.txt: ASCII text, with no line terminators

drop-in on  master 
❯ strings message.txt
This is what I was working on, but I'd need to look at my commit history to know why...

drop-in on  master 
➜ git log
commit 3339c144a0c78dc2fbd3403d2fb37d3830be5d94 (HEAD -> master)
Author: picoCTF <ops@picoctf.com>
Date:   Sat Mar 9 21:10:22 2024 +0000

    picoCTF{t1m3m@ch1n3_d3161c0f}


```
**Flag**:  picoCTF{t1m3m@ch1n3_d3161c0f}
### Notas Adicionales

### Referencias
https://primer.picoctf.org/#_git_version_control
https://cloud.donweb.com/borrar-carpetas-y-archivos-en-linux/