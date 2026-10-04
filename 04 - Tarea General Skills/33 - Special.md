### Descripción
Don't power users get tired of making spelling mistakes in the shell? Not anymore! Enter Special, the Spell Checked Interface for Affecting Linux. Now, every word is properly spelled and capitalized... automatically and behind-the-scenes! Be the first to test Special in beta, and feel free to tell us all about how Special streamlines every development process that you face. When your co-workers see your amazing shell interface, just tell them: That's Special (TM)

Hint: Experiment with different shell syntax

ssh -p 61908 [ctf-player@saturn.picoctf.net](mailto:ctf-player@saturn.picoctf.net)
### Solución
Anduve a prueba y error porque no entendia porque los corregia en automatico, tampoco funciono poner un path porque no lo permitia.
Le consulte a Claude sobre como podia poner un comando sin que me lo corrigiera, al final fue con | y con eso use find, luego probe el comando more * y despues more /blargh/* y aparecio blargh/flag.txt, le di enter y se mostro.

```
❯ ssh -p 61908 ctf-player@saturn.picoctf.net

Special$ ls 
Is 
sh: 1: Is: not found
Special$ ls -la
Is la 
sh: 1: Is: not found

sh: 1: Les: not found
Special$ llls
Ills 

Special$ /bin/ls
Absolutely not paths like that, please!

Special$ ; ls
; is 

Special$ echo | date
Echo | date 
sh: 1: Echo: not found
Wed Aug 26 22:28:47 UTC 2026

Special$ a | find
A | find 
sh: 1: A: not found
.
./blargh
./blargh/flag.txt
./.cache
./.cache/motd.legal-displayed
Special$ a | cat flag.txt
A | cat flag.txt 


Special$ a | more *
A | more * 
sh: 1: A: not found

*** blargh: directory ***

Special$ a | more blargh/*
A | more blargh/* 
sh: 1: A: not found
::::::::::::::                      
blargh/flag.txt
::::::::::::::
picoCTF{5p311ch3ck_15_7h3_w0r57_0c61d335}

```
**Flag**: picoCTF{5p311ch3ck_15_7h3_w0r57_0c61d335}
### Notas Adicionales
- `;` — ejecuta comandos en secuencia, sin importar si el anterior falló
- `|` — conecta la salida de un comando con la entrada del siguiente (pipe)
- `&&` — ejecuta el segundo comando solo si el primero tuvo éxito

Una terminal normal solo se ejecuta un comando y listo, pero con special intenta corregir la ortografia por eso si ponía ls lo interpretaba como Is.
Pero la clave estaba en los simbolos y en las palabras que ya no s- `;` — ejecuta comandos en secuencia, sin importar si el anterior falló
- `|` — conecta la salida de un comando con la entrada del siguiente (pipe)
- `&&` — ejecuta el segundo comando solo si el primero tuvo éxito corrigen como el | y palabras bien escritas como date.

Un filtro de seguridad bloquea cosas "peligrosas" antes de que pasen. Y un bypass es una forma de lograr el mismo resultado bloqueado, sin usar exactamente lo que el filtro està buscando.
### Referencias