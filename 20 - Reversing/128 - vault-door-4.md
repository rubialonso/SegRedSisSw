### Descripción

This vault uses ASCII encoding for the password. The source code for this vault is here: [VaultDoor4.java](https://challenge-files.cylabacademy.net/library/59daf48711652c50a1e865dec9f451606471c2dd0ec3b699a5e3ee2b73cc446d/VaultDoor4.java)

### Solución

1. Se descarga el código fuente usando la terminal web integrada del workspace (al igual que en los retos anteriores, el archivo `.java` se descarga como adjunto y no se puede ver directamente navegando a la URL):

```
~ $ curl -sS -o VaultDoor4.java "https://challenge-files.cylabacademy.net/library/.../VaultDoor4.java" && cat -n VaultDoor4.java
```

2. El método `checkPassword` construye un arreglo de `byte[] myBytes` usando una mezcla deliberadamente confusa de literales en distintas bases numéricas de Java (decimal, hexadecimal `0x..`, octal `0..` y literales de carácter `'x'`), y compara byte a byte contra `password.getBytes()`:

```java
byte[] myBytes = {
    106, 85, 53, 116, 95, 52, 95, 98,
    0x55, 0x6e, 0x43, 0x68, 0x5f, 0x30, 0x66, 0x5f,
    0142, 0131, 0164, 063, 0163, 0137, 066, 0141,
    '8', 'a', '9', 'e', '9', '6', 'b', 'c',
};
for (int i=0; i<32; i++) {
    if (passBytes[i] != myBytes[i]) return false;
}
return true;
```

3. En lugar de convertir cada literal a mano (y arriesgarse a un error de transcripción con los octales `0142`, `0131`, etc.), se usa el propio intérprete de Python disponible en la terminal web para parsear el arreglo directamente desde el archivo fuente, respetando las reglas de Java (prefijo `0x` = hexadecimal, `0` + dígitos = octal, literal entre comillas simples = su valor ASCII):

```python
import re
src = open('VaultDoor4.java').read()
m = re.search(r'myBytes\s*=\s*\{(.*?)\};', src, re.S)
tokens = [t.strip() for t in m.group(1).split(',') if t.strip()]

def parse(t):
    if t.startswith("'") and t.endswith("'"):
        return ord(t[1:-1])
    if t.lower().startswith('0x'):
        return int(t, 16)
    if len(t) > 1 and t[0] == '0' and t[1:].isdigit():
        return int(t[1:], 8)
    return int(t)

pw = bytes(parse(t) for t in tokens).decode()
print(pw)
```

4. Resultado: `jU5t_4_bUnCh_0f_bYt3s_6a8a9e96bc`
5. Se verifica compilando y ejecutando el propio `VaultDoor4.java` con la contraseña obtenida, confirmando "Access granted.":

```
~ $ echo "academy{jU5t_4_bUnCh_0f_bYt3s_6a8a9e96bc}" | java VaultDoor4.java
Enter vault password: Access granted.
```

Flag: `academy{jU5t_4_bUnCh_0f_bYt3s_6a8a9e96bc}`

### Notas Adicionales

Java permite escribir un mismo tipo de dato (`byte`) con literales en varias bases distintas (decimal, `0x` hexadecimal, `0` octal) e incluso como literales de carácter. Mezclarlos es solo ofuscación visual: en tiempo de compilación todos se reducen al mismo valor numérico, por lo que automatizar el parseo (en vez de hacerlo a mano) evita errores y es mucho más rápido.

### Referencias