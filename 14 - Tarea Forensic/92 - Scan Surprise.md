### Descripción

I've gotten bored of handing out flags as text. Wouldn't it be cool if they were an image instead? [challenge.zip](https://challenge-files.cylabacademy.net/library/e48eb57d2e3cbfa7fc0b3f0023b5de68ffbea6ed090caca4ceeaf403fdc00f9b/challenge.zip)

### Solución

1. Descargar y descomprimir `challenge.zip`:

```bash
   unzip challenge.zip
   # home/ctf-player/drop-in/flag.png  (99x99, 1-bit colormap)
```

2. La imagen de 99x99 en blanco y negro tiene toda la pinta de un código QR.
3. Se decodifica con OpenCV (escalando antes la imagen para facilitar la detección):

```python
   import cv2
   img = cv2.imread('flag.png')
   img_big = cv2.resize(img, (img.shape[1]*8, img.shape[0]*8), interpolation=cv2.INTER_NEAREST)
   detector = cv2.QRCodeDetector()
   data, bbox, _ = detector.detectAndDecode(img_big)
   print(data)
```

4. El QR contiene la flag directamente en texto plano.

**Flag:** `academy{p33k_@_b00_a2658a69}`

### Notas Adicionales

No fue necesario lanzar la instancia remota (shell) del reto; la flag ya estaba codificada en el QR de los archivos descargables.

### Referencias