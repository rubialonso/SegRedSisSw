### Descripción

There's something in the [building](https://challenge-files.cylabacademy.net/library/5235bfccd8f3cc2d059ee828f774846542f28f7ec66cb4f0c6ceb536c38026d4/buildings.png). Can you retrieve the flag?

Hints
- There is data encoded somewhere... there might be an online decoder.
### Solución
Primero descargamos la imagen con wget
```

```
Buscamos el online decoder, entramos a https://stylesuxx.github.io/steganography/


**Flag**: academy{h1d1ng_1n_th3_b1t5}

### Solución 2
```
~ 
❯ sudo apt install ruby

~ took 49s 
➜ sudo gem install zsteg

~ took 12s 
➜ zsteg -a buildings.png | grep academy
b1,rgb,lsb,xy       .. text: "academy{h1d1ng_1n_th3_b1t5}"
```
### Notas Adicionales

### Referencias
https://stylesuxx.github.io/steganography/