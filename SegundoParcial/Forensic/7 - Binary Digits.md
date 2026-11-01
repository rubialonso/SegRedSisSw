### Descripción
This file doesn't look like much... just a bunch of 1s and 0s. But maybe it's not just random noise. Can you recover anything meaningful from this? Download the file [here](https://challenge-files.cylabacademy.net/library/4f119c7324ffc27875b984a1d0db0591c4214fa81bd566946f1d08ed29f35135/digits.bin).
### Solución
1. Descargar el archivo con wget
2. Ahora usamos el comando:
```
~/cylab/sp_forensic 
➜ python3 -c "s=open('digits.bin').read().strip(); open('decoded.jpg','wb').write(bytes(int(s[i:i+8],2) for i in range(0,len(s),8)))"
```
3. Y abrimos el archivo con este comando y en la imagen saldrá la flag:
```
~/cylab/sp_forensic 
➜ xdg-open decoded.jpg
```

**Flag**: academy{h1dd3n_1n_th3_b1n4ry_75fdfb71}
### Notas Adicionales

### Referencias