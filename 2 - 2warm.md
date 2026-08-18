### Descripción
  
Can you convert the number 42 (base 10) to binary (base 2)?
### Solución
Ir al sitio web https://masterplc.com/calculadora/convertir-decimal-a-binario/

**Flag**: picoCTF{101010}

### Solución 2
```
python
bin (42)
> '0b101010'
```
![[2warm.png]]

### Notas Adicionales
Hay varias formar nativas como:
* Función bin() - built - in
* format () - sin el prefijo '0b'
* f-string  - f'{10:b}'
* con padding de ceros   - format(10,'08b')
### Referencias