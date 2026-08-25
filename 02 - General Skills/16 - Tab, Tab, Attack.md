### Descripción
  Using tabcomplete in the Terminal will add years to your life, esp. when dealing with long rambling directory structures and filenames.
  
  Pista:  After `unzip`ing, this problem can be solved with 11 button-presses...(mostly Tab)...
### Solución
```
wget https://challenge-files.picoctf.net/c_wily_courier/1dae7c1135f37a638408ed516c26d8312c89896cfdfdd5200e1cfca96aac768f/Addadshashanammu.zip

unzip Addadshashanammu.zip

ls

cd Addadshashanammu

~/Addadshashanammu 
➜ ls
Almurbalarammi

~/Addadshashanammu 
➜ cd Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku/


Maelkashishi/Onnissiralis/Ularradallaku via C v14.2.0-gcc 
❯ ls
fang-of-haynekhtnamet  fang-of-haynekhtnamet.c

Maelkashishi/Onnissiralis/Ularradallaku via C v14.2.0-gcc 
➜ strings fang-of-haynekhtnamet | grep pico
*ZAP!* picoCTF{l3v3l_up!_t4k3_4_r35t!_fc588427}

```

**Flag**: picoCTF{l3v3l_up!_t4k3_4_r35t!_fc588427}
### Notas Adicionales
- ctrl + a : va al inicio de la linea de comando
- ctrl + e : va al final de la linea de comando
- La tecla tab ayuda a autocompletar algun path, nombre de archivos o comandos

### Referencias