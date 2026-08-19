### Descripción
  Can you find the flag in the file? This would be really tedious to look through manually, something tells me there is a better way.

	file: file
Pista >>   grep tutorial
### Solución
En la terminal usar el comando: 
```
grep -Eo "picoCTF{.{0,50}" file
```
salida: picoCTF{grep_is_good_to_find_things_9C6Ef2F7}Jb,,TM1F||	2+

**Flag**: picoCTF{grep_is_good_to_find_things_9C6Ef2F7}
### Notas Adicionales
El comando grep es para buscar coincidencias de string dentro de un archivo.
-E se usa para encontrar expresiones regulares
-o para mostrar solo la coincidencia que se encontro y no todo el contenido del archivo

.{0,50} se usa para delimitar los caracteres que queremos despues de la coincidencia, en este caso picoCTF{ + los 50 caracteres despues para que nos muestre la flag.

### Referencias
https://www.aprendolinux.com/como-se-usa-el-comando-grep-con-ejemplos/
https://www.freecodecamp.org/espanol/news/grep-command-tutorial-how-to-search-for-a-file-in-linux-and-unix-with-recursive-find/