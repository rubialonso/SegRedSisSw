### Descripción
Decrypt this message. Message: [message](https://challenge-files.cylabacademy.net/library/9675ff2c4cd01b781e54a9ae01d22a9338eeb32023e5dd42013e6a9479753d75/data.enc)

Hint: Caesar cipher [tutorial](https://learncryptography.com/classical-encryption/caesar-cipher)
### Solución
1. Descargar el archivo y ver su contenido
```
~/cylab/crypto 
➜ wget https://challenge-files.cylabacademy.net/library/9675ff2c4cd01b781e54a9ae01d22a9338eeb32023e5dd42013e6a9479753d75/data.enc

~/cylab/crypto 
➜ cat data.enc 
academy{mbyccsxqdrobelsmyxwxeyvmah}
```

2. Pasarselo a la pagina cryptii y ponerle el texto, que sera cifrado cesar y cambiamos el número de rotaciones donde dice a → q (en mi caso hice 16 rotaciones) y ya me dio: crossingtherubiconmnuolcqx

**Flag**: academy{crossingtherubiconmnuolcqx}
### Notas Adicionales

### Referencias