### Descripción
I accidentally wrote the flag down. Good thing I deleted it!

Hints
- Version control can help you recover files if you change or lose them!
- Read the chapter on Git from the picoPrimer [here](https://primer.picoctf.org/#_git_version_control)
- You can 'checkout' commits to see the files inside them
### Solución
1. Descargar el archivo
2. Extraer los archivos, se va a crear la carpeta drop-in
3. Entrar a drop-in y ver el git log
4. Veremos unos archivos ahi, para recuperar la version anterior donde aun no se borraba nada se usa git checkout y seguido de eso ahi pegado el commit_hash que es algo como e002..cbd...
5. Ahi ya estaremos en la version anterior, con ls vemos los archivos y vemos que hay un archivo message.txt
6. Le hacemos un cat al message.txt y listo sale la flag!

```
wget https://artifacts.picoctf.net/c_titan/77/challenge.zip

➜ unzip challenge.zip
Archive:  challenge.zip

~/cylab via 🐍 v3.13.5 took 19s 
➜ ls -la

~/cylab via 🐍 v3.13.5 
➜ cd drop-in

drop-in on  master 
➜ git log
commit e1237df82d2e69f62dd53279abc1c8aeb66f6d64 (HEAD -> master)
Author: picoCTF <ops@picoctf.com>
Date:   Sat Mar 9 21:10:14 2024 +0000

    remove sensitive info

commit 3d5ec8a26ee7b092a1760fea18f384c35e435139
Author: picoCTF <ops@picoctf.com>
Date:   Sat Mar 9 21:10:14 2024 +0000

    create flag
    


drop-in on  master 
➜ git checkout 3d5ec8a26ee7b092a1760fea18f384c35e435139

drop-in on  HEAD (3d5ec8a) 
➜ ls
message.txt

drop-in on  HEAD (3d5ec8a) 
➜ cat message.txt
picoCTF{s@n1t1z3_30e86d36}
```

**Flag**: picoCTF{s@n1t1z3_30e86d36}
### Notas Adicionales

### Referencias
https://primer.picoctf.org/#_git_version_control