#### Descripción
The SOC team discovered a suspiciously large log file after a recent breach. When they opened it, they found an enormous block of encoded text instead of typical logs. Could there be something hidden within? Your mission is to inspect the resulting file and reveal the real purpose of it. The team is relying on your skills to uncover any concealed information within this unusual log. Download the encoded data here: [Logs Data](https://challenge-files.cylabacademy.net/library/e6fc51b98dd61381c5cd54dc836c8344fb475f17728f2095969e3a0f401ea195/logs.txt). Be prepared—the file is large, and examining it thoroughly is crucial .

Hint: Use `base64` to decode the data and generate the image file.

### Solución
1. Descargar el archivo logs.txt
2. La pista menciona algo sobre usar base64 para decodificar los datos y generar una imagen por ello usaremos:
	```
	base64 -d logs.txt > decode.png
	```
3. Ahora al abrir la imagen vamos a ver unos números, yo le pase la imagen a gemini para que me diera esos numeros en texto y ya solo aplique el comando:
```
~/cylab/sp_forensic 
❯ echo "61636164656D797B666F72656E736963735F616E616C797369735F69735F616D617A696E675F32303433646264317D" | xxd -r -p
academy{forensics_analysis_is_amazing_2043dbd1}
```

**Flag**: academy{forensics_analysis_is_amazing_2043dbd1}
### Notas Adicionales

### Referencias