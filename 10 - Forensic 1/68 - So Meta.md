### Descripción
Find the flag in this [picture](https://challenge-files.cylabacademy.net/library/7ed1ce00a2228a823941d5586923914d39f3085ee0a9a432555322b8dfa9f92e/pico_img.png)
Hints
* What does meta mean in the context of files?
- Ever heard of metadata?
### Solución
Usamos el comando exiftool, en el apartado de artist encontraremos la flag
```
~/cylab 
➜ exiftool pico_img.png
```
**Flag**: academy{s0_m3ta_b52e28f5}
### Notas Adicionales

### Referencias