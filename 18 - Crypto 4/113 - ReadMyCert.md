### Descripción

How about we take you on an adventure on exploring certificate signing requests. Take a look at this CSR file here ([readmycert.csr](https://challenge-files.cylabacademy.net/library/fdbbcbcc7853e60fabb2da5aaa990243c596fd00c58aa0d2270258d3ff6574df/readmycert.csr)).

### Solución

1. El archivo es un CSR (Certificate Signing Request) en formato PEM.
2. Se inspecciona su contenido con OpenSSL:

```bash
   openssl req -in readmycert.csr -noout -text
```

3. En el campo `Subject` del certificado aparece directamente la flag, en el `Common Name (CN)`:

```
   Subject: CN = academy{read_mycert_d5121f1c}, name = ctfPlayer
```

**Flag:** `academy{read_mycert_d5121f1c}`

### Notas Adicionales

No había que verificar firma ni clave privada; el dato sensible estaba a simple vista en uno de los campos estándar (CN) del propio CSR, visible con cualquier herramienta que parsee certificados/CSRs X.509 (OpenSSL, o incluso decodificando el Base64 a mano, ya que el CN va embebido sin cifrar en la estructura ASN.1 del request).

### Referencias
