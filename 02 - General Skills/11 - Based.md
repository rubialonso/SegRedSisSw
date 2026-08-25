### Descripción
  
To get truly 1337, you must understand different data encodings, such as hexadecimal or binary. Can you get the flag from this program to prove you are on the way to becoming 1337?
#### Pistas
* I hear python can convert things.
* It might help to have multiple windows open.
### Solución
Ingresar en la consola el comando:
```
nc fickle-tempest.picoctf.net 49438
```
Pasar de binario - ascii: 01110011 01110100 01110010 01100101 01100101 01110100
Pasar de octal - ascii: o143 o157 o156 o164 o141 o151 o156 o145 o162
Pasar de hexadecimal - ascii: 736f636b6574

**Flag**: picoCTF{learning_about_converting_values_acdCcfCa}
### Notas Adicionales

### Referencias
* https://gchq.github.io/CyberChef
* https://madformath.com/calculators/digital-systems/binary-codes/octal-to-ascii-converter/octal-to-ascii-converter
* https://www.rapidtables.org/convert/number/hex-to-ascii.html