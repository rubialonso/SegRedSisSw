### Descripción
I made a cool website where you can announce whatever you want! Try it out!

Hint: Server Side Template Injection
### Solución

1. Iniciamos la instancia y entramos al sitio web a través del enlace proporcionado. Buscamos el cuadro de texto donde podemos escribir nuestro anuncio.

2. Como sabemos que no hay filtros que bloqueen nuestro texto, podemos probar la vulnerabilidad enviando una operación matemática básica encerrada entre llaves dobles (el formato estándar de plantillas como Jinja2 en Python). Enviamos como anuncio:  
    ```
    {{ 7 * 7 }}
    ```
3. Si el anuncio publicado dice `49` en lugar del texto literal, confirmamos que el servidor está evaluando nuestra entrada como código.

4. Ahora que sabemos que funciona, procedemos a realizar un **RCE (Remote Code Execution)**. Enviaremos un payload estándar de SSTI en Python para escalar posiciones en los objetos del sistema e importar la librería `os`. Con esto, ejecutamos el comando `ls` para ver qué archivos hay en el servidor:
    ```
    {{ self.__init__.__globals__.__builtins__.__import__('os').popen('ls').read() }}
    ```

5. El anuncio publicado nos devolverá una lista de los archivos que están en el directorio actual (como `app.py`, `requirements.txt` y `flag`).

6. Ahora que sabemos el nombre exacto del archivo, modificamos nuestro payload anterior. Cambiamos la instrucción `ls` por `cat flag` para leer el contenido de la bandera:
    ```
    {{ self.__init__.__globals__.__builtins__.__import__('os').popen('cat flag').read() }}
    ```
    
7. Al publicar este anuncio final, el servidor ejecutará la lectura y plasmará la bandera ganadora directamente en el texto de tu publicación.

**Flag**: academy{s4rv3r_s1d3_t3mp14t3_1nj3ct10n5_4r3_c001_dee0a1a6}
### Notas Adicionales

Una **Inyección de Plantillas del Lado del Servidor (SSTI)** ocurre cuando un desarrollador toma la entrada de un usuario y la concatena directamente dentro de una plantilla, en lugar de pasarla de forma segura como un parámetro o contexto. 
### Referencias
