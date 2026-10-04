### Descripción
This website can be rendered only by picobrowser, go and catch the flag!
### Solución

```
~ via 🐍 v3.13.5 
❯ curl -s http://fickle-tempest.picoctf.net:52581/flag -H "User-Agent: picobrowser" | grep pico
         <!-- <strong>Title</strong> --> picobrowser!
            <p style="text-align:center; font-size:30px;"><b>Flag</b>: <code>picoCTF{p1c0_s3cr3t_ag3nt_fba5c48f}</code></p>
```
**Flag**: picoCTF{p1c0_s3cr3t_ag3nt_fba5c48f}
### Notas Adicionales

### Referencias