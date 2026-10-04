### Descripción
Can you win in a convincing manner against this chess bot? He won't go easy on you! You can find the challenge [here](http://xebec.cylabacademy.net:30288/).

Hint: Try understanding the code and how the websocket client is interacting with the server
### Solución
1. Al inspeccionar el código fuente de la página (`Ctrl + U`), identificamos la función `sendMessage(message)` que transmite datos directamente a través del WebSocket. También observamos que el cliente JavaScript evalúa la partida y envía el resultado al servidor utilizando formatos como `mate X` o `eval X`.

2. Como el servidor confía ciegamente en los datos que provienen del cliente, no necesitamos jugar ni usar herramientas externas. Abrimos las Herramientas de Desarrollador del navegador (`F12`) y nos dirigimos a la pestaña **Consola**.

3. Para convencer al bot de que está sufriendo una derrota absoluta, probamos manipular la evaluación del juego enviando valores extremos. Ejecutamos directamente la función con un número negativo masivo:
    ```
    sendMessage("eval -100000000000000000000000000000000000000000000000000000000000000000000000000000000")
    ```
    
4. El servidor procesa esta evaluación falsa y el bot se rinde inmediatamente. La burbuja de chat en la interfaz gráfica se actualiza mostrando el mensaje de rendición junto con la bandera: "Huh???? How can I be losing this badly... I resign... here's your flag: academy{c1i3nt_s1d3_w3b_s0ck3t5_906748f0}".

**Flag**: academy{c1i3nt_s1d3_w3b_s0ck3t5_906748f0}

### Notas Adicionales

Este desafío demuestra una vulnerabilidad crítica de **Client-Side Trust** (Confianza en el lado del cliente). 
### Referencias
