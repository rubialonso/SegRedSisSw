### Descripción
  Run the Python script and convert the given number from decimal to binary to get the flag.
Hints
- Look up a decimal to binary number conversion app on the web or use your computer's calculator!
- The `str_xor` function does not need to be reverse engineered for this challenge.
- If you have Python on your computer, you can download the script normally and run it. Otherwise, use the `wget` command in the webshell.
- To use `wget` in the webshell, first right click on the download link and select 'Copy Link' or 'Copy Link Address'
- Type everything after the dollar sign in the webshell: `$ wget` , then paste the link after the space after `wget` and press enter. This will download the script for you in the webshell so you can run it!
- Finally, to run the script, type everything after the dollar sign and then press enter: `$ python3 convertme.py`.
### Solución
Primero descargar el archivo con wget:
```
➜ wget https://artifacts.picoctf.net/c/22/convertme.py
```
Luego ejecutar el archivo convertme.py:
```
~/cylab via 🐍 v3.13.5 took 28s 
➜ python convertme.py
```

Calcular el binario:
44 / 2 = 22 residuo 0
22 / 2 = 11 residuo 0
11/ 2 = 5 residuo 1
5 / 2 = 2 residuo 1
2 / 2 = 1 residuo 0
1 / 2 = 0 residuo 1

binario: 101100

Poner la respuesta:
```
~/cylab via 🐍 v3.13.5 took 34s 
➜ python convertme.py
If 44 is in decimal base, what is it in binary base?
Answer: 101100
That is correct! Here's your flag: picoCTF{4ll_y0ur_b4535_762f748e}
```

**Flag**: picoCTF{4ll_y0ur_b4535_762f748e}

### Solución 2
En CyberChef usar la formula to base con radix 2: 101100

### Notas Adicionales
Para obtener el binario podemos dividir entre 2 y vemos el residuo, luego se lee de abajo hacia arriba:

54 / 2 = 27   residuo 0
27 / 2 = 13   residuo 1
13 / 2 = 6    residuo 1
 6 / 2 = 3    residuo 0
 3 / 2 = 1    residuo 1
 1 / 2 = 0    residuo 1

54 en binario: 110110

### Referencias
https://gchq.github.io/CyberChef/