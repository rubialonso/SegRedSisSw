### Descripción
  
What does this bDNhcm5fdGgzX3IwcDM1 mean? I think it has something to do with bases.
### Solución
Ir al sitio web https://gchq.github.io/CyberChef/

**Flag**: picoCTF{l3arn_th3_r0p35}

### Solución 2
Ejecutar desde python:
```
import base64
base64.b64decode("bDNhcm5fdGgzX3IwcDM1")
>>> b'l3arn_th3_r0p35
```

### Notas Adicionales
- Termina con`=`: Base64/Base32.
- Sólo 0–9A–F: Hex.
- `%20`,`%3D` : URL codificada.
- Binario (0/1 bytes): binario ASCII o cifrado de bits.
### Referencias
https://ctf.support/crypto/encodings/