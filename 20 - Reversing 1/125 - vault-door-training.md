### Descripción

Your mission is to enter Dr. Evil's laboratory and retrieve the blueprints for his Doomsday Project. The laboratory is protected by a series of locked vault doors. Each door is controlled by a computer and requires a password to open. Unfortunately, our undercover agents have not been able to obtain the secret passwords for the vault doors, but one of our junior agents obtained the source code for each vault's computer! You will need to read the source code for each level to figure out what the password is for that vault door. As a warmup, we have created a replica vault in our training facility.

The source code for the training vault is here: [VaultDoorTraining.java](https://challenge-files.cylabacademy.net/library/83cea9a75c072b1b2dff071720061929c5a4e9817a86613e1c51ebc0540cbc73/VaultDoorTraining.java)

### Solución

1. El archivo `.java` se descarga como adjunto (no se puede ver directamente en el navegador), así que se usa la terminal web integrada de la plataforma (botón "Terminal" del workspace) para descargarlo y leerlo:

```
~ $ curl -sS -o VaultDoorTraining.java "https://challenge-files.cylabacademy.net/library/83cea9a75c072b1b2dff071720061929c5a4e9817a86613e1c51ebc0540cbc73/VaultDoorTraining.java" && cat VaultDoorTraining.java
```

2. El código fuente muestra que el programa:
    - Pide al usuario una contraseña con el formato `academy{...}`.
    - Extrae el contenido entre las llaves con `userInput.substring("academy{".length(), userInput.length()-1)`.
    - Llama a `checkPassword(input)`, que simplemente compara el valor ingresado contra una cadena fija con `password.equals(...)`:

```java
public boolean checkPassword(String password) {
    return password.equals("w4rm1ng_Up_w1tH_jAv4_4cfa5369b93");
}
```

3. La contraseña está escrita en texto plano directamente en el código fuente (el propio comentario del archivo bromea sobre lo insegura que es esta práctica: "Is it safe to put the password in the source code?"). Basta con leerla y envolverla en el formato `academy{...}` pedido por el programa.

Flag: `academy{w4rm1ng_Up_w1tH_jAv4_4cfa5369b93}`

### Notas Adicionales

Este reto es un ejemplo clásico de por qué nunca se deben hardcodear contraseñas o secretos directamente en el código fuente: cualquiera con acceso al código (o al binario compilado, vía decompilación) puede leer la contraseña sin necesidad de romper ningún algoritmo criptográfico.

### Referencias