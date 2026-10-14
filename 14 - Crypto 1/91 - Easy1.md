### Descripción
The one time pad can be cryptographically secure, but not when you know the key. Can you solve this? We've given you the encrypted flag, key, and a table to help `UFJKXQZQUNB` with the key of `SOLVECRYPTO`. Can you use this [table](https://challenge-files.cylabacademy.net/library/14a944b4b00c6d6e9213b62098e0c8a8d77219757b1a51d9af4bc15e263b6b92/table.txt) to solve it?.

Hints:  
1. Submit your answer in our flag format. For example, if your answer was 'hello', you would submit 'academy{HELLO}' as the flag.
2. Please use all caps for the message.
### Solución
Descargue el archivo con wget, luego abriendolo vi que el mensaje estaba cifrado.
Sabiendo que en el mensaje estas son la llave y el cifrado:
cifrado:UFJKXQZQUNB
llave:SOLVECRYPTO
usando cyberchef se puede decifrar usando el viegenere decode

**Flag**: academy{CRYPTOISFUN}
### Notas Adicionales

### Referencias