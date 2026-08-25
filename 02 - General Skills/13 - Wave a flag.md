### Descripción
Can you invoke help flags for a tool or binary? This program has extraordinarily helpful information...

Pistas
* This program will only work in the webshell or another Linux computer.
* To get the file accessible in your shell, enter the following in the Terminal prompt: `$ wget  <URL here>` where the url can be found in the details section.
* Run this program by entering the following in the Terminal prompt: $ ./warm, but you'll first have to make it executable with $ chmod +x warm.
* -h and --help are the most common arguments to give to programs to get more information from them!
* Not every program implements help features like -h and --help.
### Solución
```
wget https://challenge-files.picoctf.net/c_wily_courier/5a478d0b24d6a4f4185e3adb7a78c41cdad626fb02fe80e083dc33bf8b197d3d/warm

chmod +x warm

➜ ./warm
Hello user! Pass me a -h to learn what I can do!

~ 
❯ ./warm -h
Oh, help? I actually don't do much, but I do have this flag here: picoCTF{b1scu1ts_4nd_gr4vy_ac5832c}
```

**Flag**: picoCTF{b1scu1ts_4nd_gr4vy_ac5832c}
### Notas Adicionales
chmod es un comando para modificar los permisos

### Referencias
