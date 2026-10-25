### Descripción

Morse code is well known. Can you decrypt this? Wrap your answer with `academy{}`, put underscores in place of pauses, and use all uppercase.

Archivo adjunto: `morse_chal.wav` (audio mono, 16-bit, 44100 Hz, ~29 segundos).

### Solución

1. Se analiza el archivo de audio con Python/NumPy, extrayendo la envolvente de amplitud (valor absoluto de las muestras suavizado con una ventana de 10 ms) para detectar los tramos de sonido ("encendido") y silencio ("apagado"):

```python
import wave, numpy as np
w = wave.open('morse_chal.wav', 'rb')
fr = w.getframerate()
samples = np.frombuffer(w.readframes(w.getnframes()), dtype=np.int16).astype(np.float64)
env = np.convolve(np.abs(samples), np.ones(int(fr*0.01))/int(fr*0.01), mode='same')
on = env > env.max()*0.25
```

2. Se agrupan los tramos consecutivos de "encendido/apagado" en duraciones, y se observa que:
    - Tramos "encendido" cortos (~0.1 s) = punto (`.`)
    - Tramos "encendido" largos (~0.3 s) = raya (`-`)
    - Silencios cortos (~0.1 s) = separación interna de un mismo símbolo (no se añade separador)
    - Silencios medios (~0.4 s) = separación entre letras (espacio simple)
    - Silencios largos (~0.8 s) = separación entre palabras (espacio doble)
3. Se reconstruye la cadena Morse y se decodifica con la tabla estándar Morse → texto:

```
.-- .... ....- --...   .... ....- --... ....   ----. ----- -..   .-- ..--- ----- ..- ----. .... --...
```

```
WH47   H47H   90D   W20U9H7
```

4. Interpretando los dígitos como "leetspeak" (4→A, 7→T, 9→G, 0→O, 2→R) el mensaje se lee como **"WHAT HATH GOD WROUGHT"**, la célebre primera frase transmitida en código Morse por Samuel Morse en 1844.
5. Siguiendo las instrucciones del reto (mayúsculas, guiones bajos en lugar de las pausas entre palabras, envuelto en `academy{}`):

Flag: `academy{WH47_H47H_90D_W20U9H7}`

### Notas Adicionales

No fue necesario decodificar manualmente el Morse símbolo por símbolo: automatizar la detección de energía de la señal de audio (envolvente + umbral) permitió extraer con precisión los tiempos de punto/raya/espacio y aplicar directamente la tabla Morse.

### Referencias

- [Morse code - Wikipedia](https://en.wikipedia.org/wiki/Morse_code)
- [What hath God wrought - Wikipedia](https://en.wikipedia.org/wiki/What_hath_God_wrought)