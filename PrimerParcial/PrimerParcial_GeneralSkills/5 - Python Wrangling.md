### Descripción
Python scripts are invoked kind of like programs in the Terminal... Can you run [ende.py](https://challenge-files.cylabacademy.net/library/9524fad56d411feaebef2bff00dedd811236de9859d90c446ac88ffac47e0192/ende.py) using [password.txt](https://challenge-files.cylabacademy.net/library/9524fad56d411feaebef2bff00dedd811236de9859d90c446ac88ffac47e0192/password.txt) to get [flag.txt.en](https://challenge-files.cylabacademy.net/library/9524fad56d411feaebef2bff00dedd811236de9859d90c446ac88ffac47e0192/flag.txt.en)

Hints:
1. Get the Python script accessible in your shell by entering the following command in the Terminal prompt: `$ wget` followed by a link to the script. The link can be copied from the details section.
2. `$ man python`
### Solución

1. Descargamos los archivos del reto:
```
~/cylab via 🐍 v3.13.5 
➜ wget https://challenge-files.cylabacademy.net/library/9524fad56d411feaebef2bff00dedd811236de9859d90c446ac88ffac47e0192/ende.py

~/cylab via 🐍 v3.13.5 
➜ wget https://challenge-files.cylabacademy.net/library/9524fad56d411feaebef2bff00dedd811236de9859d90c446ac88ffac47e0192/password.txt

~/cylab via 🐍 v3.13.5 
➜ wget https://challenge-files.cylabacademy.net/library/9524fad56d411feaebef2bff00dedd811236de9859d90c446ac88ffac47e0192/flag.txt.en
```

2. Con cat checamos el archivo de la contraseña y copiamos el contenido
```
~/cylab via 🐍 v3.13.5 
➜ cat password.txt
563e47ddeaf84eca8b2a31201381a898
```

3. Al ejecutar ende.py, el menú de ayuda indica que hay que usar el modificador -d para descifrar seguido del archivo, así que ejecutamos el archivo siguiendo el formato usando el archivo flag.txt.en: 
```
~/cylab via 🐍 v3.13.5 
❯ python3 ende.py 
Usage: ende.py (-e/-d) [file]

~/cylab via 🐍 v3.13.5 
❯ python3 ende.py -d flag.txt.en
Please enter the password:563e47ddeaf84eca8b2a31201381a898
academy{4p0110_1n_7h3_h0us3_d6af8f37}
```

**Flag**: academy{4p0110_1n_7h3_h0us3_d6af8f37}
### Notas Adicionales

### Referencias