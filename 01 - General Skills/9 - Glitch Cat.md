### Descripción
  Our flag printing service has started glitching!
Pistas:
1. ASCII is one of the most common encodings used in programming

2. We know that the glitch output is valid Python, somehow!

3. Press Ctrl and c on your keyboard to close your connection and return to the command prompt.
$ nc saturn.picoctf.net 56190
### Solución
```
➜ nc saturn.picoctf.net 56190
'picoCTF{gl17ch_m3_n07_' + chr(0x62) + chr(0x64) + chr(0x61) + chr(0x36) + chr(0x38) + chr(0x66) + chr(0x37) + chr(0x35) + '}'

~ 
➜ python
Python 3.13.5 (main, May  5 2026, 21:05:52) [GCC 14.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> 'picoCTF{gl17ch_m3_n07_' + chr(0x62) + chr(0x64) + chr(0x61) + chr(0x36) + chr(0x38) + chr(0x66) + chr(0x37) + chr(0x35) + '}'
'picoCTF{gl17ch_m3_n07_bda68f75}'
>>> 
```

**Flag**: picoCTF{gl17ch_m3_n07_bda68f75}
### Notas Adicionales
* Python utiliza el + para concatenar cadenas
* chr() es una funciòn de python que convierte un número a su correspondiente caracter ASCII
* Esto fue simplemente una uma de cadenas y caracteres

### Referencias