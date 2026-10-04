### Descripción
This website puts a two-factor prompt between you and the flag. Register an account, then take a close look at the requests your browser is actually sending.
Hints:
1. Try using burpsuite to intercept request to capture the flag.
2. Try mangling the request, maybe their server-side code doesn't handle malformed requests very well.
### Solución
1. Pasar el filtro del formulario
2. En el OTP vamos a iniciar foxy proxy para entrar a burp suite
3. Una vez que burp suite muestre que si se esta haciendo el intercept vamos a la página del reto y ponemos un número cualquiera '123'
4. Ya enviada la solicitud vamos a burp suite y mandamos la petición al repeater
5. Cambiamos el acept y el content-type por application/json y el otp por 0000
6. Le damos a Send, y nos va a dar la flag

**Flag**: academy{#0TP_Bypvss_SuCc3$S_10ea7681}
### Notas Adicionales

### Referencias