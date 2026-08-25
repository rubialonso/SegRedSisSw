### Descripción
  Unzip this archive and find the flag.

Pista:  Can grep be instructed to look at every file in a directory and its subdirectories?
### Solución
```
~ 
➜ wget https://artifacts.picoctf.net/c/503/big-zip-files.zip

~ 
➜ unzip big-zip-files.zip

~ 
➜ cd big-zip-files/

~/big-zip-files 
➜ ls

~/big-zip-files 
➜ grep -R pico
folder_pmbymkjcya/folder_cawigcwvgv/folder_ltdayfmktr/folder_fnpfclfyee/whzxrpivpqld.txt:information on the record will last a billion years. Genes and brains and books encode picoCTF{gr3p_15_m4g1c_ef8790dc}
```

**Flag**: picoCTF{gr3p_15_m4g1c_ef8790dc}
### Notas Adicionales
## Recursively Grep Through Directories

When you want to search for a specific pattern across multiple files within a directory, ****grep**** can be used recursively. The recursive option ****(-R)**** allows the command to traverse through subdirectories as well.

### ****Example 1: Search Current Working Directory Recursively with grep Command****

Grep can be used ****recursively**** if we need to search for a string pattern across multiple files in a directory. In order to use grep recursively, we must add the -****R**** tag after grep and change __"__****file_to_be_searched****" to "****directory_path****".

#### ****Syntax:**** 

grep -R "string_to_be_searched" "directory_path"

> ****Note****__:  If the "__****directory_path****__" is not mentioned with grep -R it will consider__ _****current directory or working directory****_ __as "__****directory_path****__".__

### Referencias
https://www.geeksforgeeks.org/linux-unix/how-to-recursively-grep-all-directories-and-subdirectories-in-linux/