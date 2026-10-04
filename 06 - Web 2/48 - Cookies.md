### Descripción
Who doesn't love cookies? Try to figure out the best one.
### Solución
Buscamos entre todas las cookies "pico" y busca entre todas las cookies: 
```
~ via 🐍 v3.13.5 took 38s 
➜ for i in {4..20}; do curl -s http://wily-courier.picoctf.net:58673/check -H "Cookie: name=$i" | grep "pico"; done
            <p style="text-align:center; font-size:30px;"><b>Flag</b>: <code>picoCTF{3v3ry1_l0v3s_c00k135_a4dadb49}
```

**Flag**: picoCTF{3v3ry1_l0v3s_c00k135_a4dadb49}
### Notas Adicionales

### Referencias