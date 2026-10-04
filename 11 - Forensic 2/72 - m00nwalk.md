### Descripción
Decode this [message](https://challenge-files.cylabacademy.net/library/d825fde6581b1311eafdd403da1cc96f1f98fe3fe84cd71d850310ebb3908088/message.wav) from the moon.
Hints:
- How did pictures from the moon landing get sent back to Earth?
- What is the CMU mascot?, that might help select a RX option
### Solución
```
  GNU nano 8.4                                                  decode.py                                                              
for line in range(256):
    line_start = int(start_sample + line * line_samples)
    if line_start + int(line_samples) >= len(freqs):
        break

    red_start = line_start + int((9.0 + 1.5) * 48)
    green_start = line_start + int((9.0 + 1.5 + 138.24 + 1.5) * 48)
    blue_start = line_start + int((9.0 + 1.5 + 138.24 + 1.5 + 138.24 + 1.5) * 48)

    for px in range(320):
        r_idx = red_start + int(px * px_samples)
        g_idx = green_start + int(px * px_samples)
        b_idx = blue_start + int(px * px_samples)

        if b_idx < len(freqs):
            img[line, px, 0] = freq_to_byte(freqs[r_idx])
            img[line, px, 1] = freq_to_byte(freqs[g_idx])
            img[line, px, 2] = freq_to_byte(freqs[b_idx])

# 5. Guardar la imagen resultante (rotada 180° para que quede derecha)
pil_img = Image.fromarray(img)
final_img = pil_img.rotate(180)
final_img.save("result.png")
print("¡Imagen guardada exitosamente como result.png!")
```

```
~/cylab via 🐍 v3.13.5 (mivenv) 
➜ nano decode.py

~/cylab via 🐍 v3.13.5 (mivenv) took 7s 
➜ python decode.py
Traceback (most recent call last):
  File "/home/rubi/cylab/decode.py", line 3, in <module>
    from scipy.io import wavfile
ModuleNotFoundError: No module named 'scipy'

~/cylab via 🐍 v3.13.5 (mivenv) 
❯ nano decode.py

~/cylab via 🐍 v3.13.5 (mivenv) took 19s 
➜ pip install scipy numpy

~/cylab via 🐍 v3.13.5 (mivenv) took 12s 
➜ python decode.py
¡Imagen guardada exitosamente como result.png!

~/cylab via 🐍 v3.13.5 (mivenv) took 4s 
➜ open result.png
```
Se resolvio por un script de python, se coupa una libreria llamada scipy si no esta se instala y se vuelve a ejecutar el codigo y nos da el archivo convertido a imagen, ya solo la abrimos y escribimos la flag.

**Flag**: picoCTF{beep_boop_im_in_space}
### Notas Adicionales

### Referencias