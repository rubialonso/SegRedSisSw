### Descripción

A message has been encrypted using RSA. The public key is gone… but someone might have been careless with the private key. Can you recover it and decrypt the message? Download the flag (`flag.enc`) and image (`image.jpg`).

_by Yahaya Meddy · picoCTF 2026_

### Solución

1. Se descargan `flag.enc` (el mensaje cifrado con RSA) e `image.jpg` con la terminal web.
2. El enunciado insinúa esteganografía: la clave privada RSA estaría oculta dentro de la imagen. Se inspecciona la imagen con Pillow, revisando sus metadatos (en particular el segmento de comentario JFIF/COM de un JPEG):

```python
from PIL import Image
img = Image.open('image.jpg')
print(img.info.keys())
comment = img.info['comment']
```

3. El campo `comment` contiene una cadena hexadecimal larga. Al decodificarla (`bytes.fromhex(...)`) se obtiene texto plano que es, literalmente, una clave privada RSA completa en formato PEM (`-----BEGIN RSA PRIVATE KEY-----...`). Se guarda como `privkey.pem`.
4. Con la clave privada recuperada, se descifra `flag.enc`. Al probar con `PKCS1_OAEP` falla con "Incorrect decryption", así que se prueba el esquema de relleno clásico `PKCS1_v1_5`, que sí funciona:
```python
from Crypto.PublicKey import RSA
from Crypto.Cipher import PKCS1_v1_5

key = RSA.import_key(open('privkey.pem').read())
c = open('flag.enc', 'rb').read()
cipher = PKCS1_v1_5.new(key)
pt = cipher.decrypt(c, None)
print(pt)
```

5. Resultado: `b'academy{rs4_k3y_1n_1mg_d97b7bfb}\n'`

Flag: academy{rs4_k3y_1n_1mg_d97b7bfb}

### Notas Adicionales

Este reto combina esteganografía (ocultar datos binarios dentro de los metadatos de una imagen JPEG) con RSA: aunque el algoritmo RSA en sí mismo no está roto, la seguridad de todo el sistema colapsa si la clave privada queda accesible por cualquier canal, en este caso embebida descuidadamente en una imagen "pública". También fue necesario probar más de un esquema de relleno (OAEP vs PKCS1 v1.5) hasta encontrar el que el cifrado original utilizó.

### Referencias

- [JPEG File Interchange Format (JFIF) - Wikipedia](https://en.wikipedia.org/wiki/JPEG_File_Interchange_Format)
- [PKCS #1 - Wikipedia](https://en.wikipedia.org/wiki/PKCS_1)