### Descripción
Unzip this archive and find the file named 'uber-secret.txt'
### Solución
```
~/Downloads 
➜ wget https://artifacts.picoctf.net/c/501/files.zip

~/Downloads 
➜ unzip files.zip

~/Downloads 
➜ cd files


~/Downloads/files 
➜ find . -name uber-secret.txt
./adequate_books/more_books/.secret/deeper_secrets/deepest_secrets/uber-secret.txt

➜ cat ./adequate_books/more_books/.secret/deeper_secrets/deepest_secrets/uber-secret.txt
picoCTF{f1nd_15_f457_ab443fd1}
```

**Flag**: picoCTF{f1nd_15_f457_ab443fd1}
### Notas Adicionales
## Comando find en Linux

El comando `find` se usa para localizar archivos en [Linux](https://www.stackscale.com/es/blog/linux/), basándose en los criterios especificados por el usuario. La sintaxis básica del comando es la siguiente:

find -opciones /ruta expresión

### Atributos del comando find

- `-opciones`: las opciones o parámetros de búsqueda permiten controlar el comportamiento y el método de optimización del proceso de `find`.
- `/ruta`: define la ruta de acceso al directorio a partir de la cual el comando `find` empezará a filtrar.
- `expresión`: define las acciones a realizar para crear un resultado.

### Referencias
https://www.stackscale.com/es/blog/comando-find-linux/