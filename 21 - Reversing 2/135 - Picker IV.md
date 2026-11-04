### Descripción
Can you figure out how this program works to get the flag?

Hints:
1. With Python, there are no binaries. With compiled languages like C, there is source code, and there are binaries. Binaries are created from source code, they are a conversion from the human-readable source code, to the highly efficient machine language, in this case: x86_64.
2. How can you find the address that `win` is at?
### Solución
1. Inicial instancia y descargar todos los archivos
2. Viendo el código nos daremos cuenta que esta vez no se manda a llamar a la función win
3. Vamos a ver la dirección de memoria ejecutando el comando: `
	`nm picker-IV
4. Veremos que win esta al final, vamos a copiar la dirección:
```
.
.
0000000000404068 B stdout@GLIBC_2.2.5
0000000000404068 D __TMC_END__
00000000004012a1 T win
```
5. Nos conectamos al servidor y le pasamos la dirección de win:
```
➜ nc xebec.cylabacademy.net 19184
Enter the address in hex to jump to, excluding '0x': 00000000004012a1               
You input 0x4012a1
You won!
academy{n3v3r_jump_t0_u53r_5uppl13d_4ddr35535_cccc13c1}
```

**Flag**: academy{n3v3r_jump_t0_u53r_5uppl13d_4ddr35535_cccc13c1}
### Notas Adicionales

### Referencias