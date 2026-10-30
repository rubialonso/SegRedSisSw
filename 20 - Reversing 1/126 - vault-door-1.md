### Descripción
This vault uses some complicated arrays! I hope you can make sense of it, special agent. The source code for this vault is here: [VaultDoor1.java](https://challenge-files.cylabacademy.net/library/dd0ae9b406943de9f8bee5c8f5b509e72ad86fc3855bbe2f4f83228d6309a25c/VaultDoor1.java)
### Solución
1. Descargar el archivo
2. Luego checamos su contenido, en el código vamos a ver que el código hace una comparación con la entrada y la bandera, copiamos los charAt() del codigo y lo pasamos a un archivo por separado:
```
               password.charAt(00)  == 'd' &&
               password.charAt(01)  == '3' &&
               password.charAt(02)  == '5' &&
               password.charAt(03)  == 'c' &&
               password.charAt(04)  == 'r' &&
               password.charAt(05)  == '4' &&
               password.charAt(06)  == 'm' &&
               password.charAt(07)  == 'b' &&
               password.charAt(08)  == 'l' &&
               password.charAt(09)  == '3' &&
               password.charAt(10) == '_' &&
               password.charAt(11) == 't' &&
               password.charAt(12) == 'H' &&
               password.charAt(13) == '3' &&
               password.charAt(14) == '_' &&
               password.charAt(15) == 'c' &&
               password.charAt(16) == 'H' &&
               password.charAt(17) == '4' &&
               password.charAt(18) == 'r' &&
               password.charAt(19) == '4' &&
               password.charAt(20) == 'c' &&
               password.charAt(21) == 'T' &&
               password.charAt(22) == '3' &&
               password.charAt(23) == 'r' &&
               password.charAt(24) == '5' &&
               password.charAt(25) == '_' &&
               password.charAt(26) == '1' &&
               password.charAt(27) == '7' &&
               password.charAt(28) == '9' &&
               password.charAt(29) == 'f' &&
               password.charAt(30) == 'b' &&
               password.charAt(31) == 'd';
	
```

3. A ese archivo le aplicamos este comando (flag es el archivo que se creó):
`~/cylab via ☕ v25.0.4 via 🐍 v3.13.5
`➜ cat flag | sort | awk '{print $3}' | tr -d "'" | tr -d '\n'
`d35cr4mbl3_tH3_cH4r4cT3r5_179fbd;`

**Flag**: academy{d35cr4mbl3_tH3_cH4r4cT3r5_179fbd}
### Notas Adicionales

### Referencias