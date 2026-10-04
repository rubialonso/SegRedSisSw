### Descripción
Reception of Special has been cool to say the least. That's why we made an exclusive version of Special, called Secure Comprehensive Interface for Affecting Linux Empirically Rad, or just 'Specialer'. With Specialer, we really tried to remove the distractions from using a shell. Yes, we took out spell checker because of everybody's complaining. But we think you will be excited about our new, reduced feature set for keeping you focused on what needs it the most. Please start an instance to test your very own copy of Specialer.

`ssh -p 39957 ctf-player@chatelaine.cylabacademy.net`. The password is `8d1db23b`

Hint: What programs do you have access to?
### Solución

1. Nos conectamos a la instancia del servidor mediante SSH al puerto 39957 utilizando el usuario `ctf-player`:
```
~/cylab via 🐍 v3.13.5 
❯ ssh -p 39957 ctf-player@chatelaine.cylabacademy.net
The authenticity of host '[chatelaine.cylabacademy.net]:39957 ([18.227.187.235]:39957)' can't be established.
ED25519 key fingerprint is: SHA256:TMzuFX+tQxG+rVL0CK63ywMGkWGIsWZEgT7sWWAVfMg
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[chatelaine.cylabacademy.net]:39957' (ED25519) to the list of known hosts.
ctf-player@chatelaine.cylabacademy.net's password: 
```

2. Al estar dentro de la consola, confirmamos que comandos binarios básicos como `ls` han sido eliminados del entorno. Para evadir la restricción y descubrir qué archivos existen, recurrimos al comando integrado `echo` junto con los comodines de expansión (`*` y `*/*`):
```
Specialer$ ls
-bash: ls: command not found
Specialer$ echo *
abra ala sim
Specialer$ echo */*
abra/cadabra.txt abra/cadaniel.txt ala/kazam.txt ala/mode.txt sim/city.txt sim/salabim.txt
```

3. Sabiendo que los comandos tradicionales de lectura tampoco funcionan, utilizamos una técnica de redirección de entrada nativa de Bash (`$<`) dentro de un `echo` para imprimir el contenido de cada archivo descubierto en la pantalla. Iteramos por los archivos hasta dar con la bandera en `ala/kazam.txt`:
```
Specialer$ echo "$(< sim/salabim.txt)"
#He was so kind, such a gentleman tied to the oceanside#
Specialer$ echo "$(< sim/city.txt)"
05ed181c-4aa0-4d4a-8505-2fe6ca9097d3
Specialer$ echo "$(< ala/mode.txt)"
Yummy! Ice cream!
Specialer$ echo "$(< ala/kazam.txt)"
return 0 academy{y0u_d0n7_4ppr3c1473_wh47_w3r3_d01ng_h3r3_17ec7048}
```

**Flag**: academy{y0u_d0n7_4ppr3c1473_wh47_w3r3_d01ng_h3r3_17ec7048}

### Notas Adicionales

Este desafío es una variante de "Bash Jail" que demuestra que bloquear binarios ejecutables comunes (como borrar `/bin/ls` o `/bin/cat`) no es suficiente para asegurar un sistema. Las funcionalidades integradas (built-ins) de Bash, como el comando `echo` y el _globbing_ (expansión de comodines), se ejecutan en la memoria de la propia shell sin depender de programas externos. Combinar comodines de rutas con las redirecciones nativas permite listar y extraer cualquier información del sistema directamente desde Bash.
### Referencias
