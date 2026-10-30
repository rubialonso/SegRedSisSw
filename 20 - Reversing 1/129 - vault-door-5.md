### Descripción

In the last challenge, you mastered octal (base 8), decimal (base 10), and hexadecimal (base 16) numbers, but this vault door uses a different change of base as well as URL encoding! The source code for this vault is here: [VaultDoor5.java](https://challenge-files.cylabacademy.net/library/e0c427718db4f670d4a09df9a1ce5c4d2ff6dec848cbbda005a892acccaa4097/VaultDoor5.java)

### Solución

1. Se descarga el código fuente con la terminal web:

```
~ $ curl -sS -o VaultDoor5.java "https://challenge-files.cylabacademy.net/library/.../VaultDoor5.java" && cat -n VaultDoor5.java
```

2. El método `checkPassword` esta vez no compara la contraseña directamente, sino que le aplica dos transformaciones y compara el resultado contra una constante en Base64 (la "otra base" mencionada en el enunciado, además del URL encoding):
```java
public boolean checkPassword(String password) {
    String urlEncoded = urlEncode(password.getBytes());
    String base64Encoded = base64Encode(urlEncoded.getBytes());
    String expected = "JTYzJTMwJTZlJTc2JTMzJTcyJTc0JTMxJTZlJTY3Jk" +
                       "YzJTJjcyUYxJTYwJTZk..." /* concatenada en varias líneas */;
    return base64Encoded.equals(expected);
}
```

Es decir: `password -> URL-encode -> Base64-encode -> comparar con "expected"`.

3. Para recuperar la contraseña original hay que invertir el proceso en orden opuesto: primero decodificar Base64 (para obtener la cadena URL-encoded), y luego aplicar URL-decode sobre esa cadena para obtener la contraseña en texto plano. Se automatiza con Python directamente en la terminal web, extrayendo el literal `expected` (reconstruyéndolo a partir de los trozos de string concatenados con `+` en el código fuente) para evitar errores de transcripción manual de una cadena Base64 tan larga:

```python
import re, base64, urllib.parse
src = open('VaultDoor5.java').read()
m = re.search(r'expected\s*=\s*(".*?");', src, re.S)
expected = ''.join(re.findall(r'"([^"]*)"', m.group(1)))

decoded = base64.b64decode(expected).decode()      # cadena URL-encoded
pw = urllib.parse.unquote(decoded)                 # contraseña en texto plano
print(pw)
```

4. Resultado: `c0nv3rt1ng_fr0m_ba5e_64_e340c3ed`
5. Se verifica ejecutando el propio `VaultDoor5.java` con la contraseña obtenida:

```
~ $ echo "academy{c0nv3rt1ng_fr0m_ba5e_64_e340c3ed}" | java VaultDoor5.java
Enter vault password: Access granted.
```

Flag: `academy{c0nv3rt1ng_fr0m_ba5e_64_e340c3ed}`

### Notas Adicionales

Este reto encadena dos codificaciones (URL encoding y Base64) en vez de dos "bases numéricas" clásicas. La clave para resolverlo es identificar el orden exacto en que se aplican las transformaciones en el cifrado (`urlEncode` primero, luego `base64Encode`) para poder revertirlas en el orden inverso (`base64 decode` primero, luego `url decode`); invertir el orden incorrecto produce una cadena corrupta o un error de decodificación.