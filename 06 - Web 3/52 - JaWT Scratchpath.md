### Descripción
Check the admin scratchpad!
Hints:
- What is that cookie?
- Have you heard of JWT?
### Solución
1. Primero vemos la cookie generada al poner un usuario cualquiera
2. Luego nos vamos a https://jwt.lannysport.net/ y metemos el token, cambiamos el paylaod por admin
3. Usando Jonh The Ripper tomamos rockyou.txt
4. Dentro encontraremos la firma "ilovepico"
5. Modificamos esto en https://jwt.lannysport.net/  en la sección de signature
6. Editamos la cookie con el token que nos dio y nos dara la flag

**Flag**: picoCTF{jawt_was_just_what_you_thought_bbb82bd4a57564aefb32d69dafb60583}
### Notas Adicionales

### Referencias
https://jwt.lannysport.net/