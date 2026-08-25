### Descripción
Can you make sense of this file?

Pista: Multiple decoding is always good.
### Solución
```
~ 
➜ wget https://artifacts.picoctf.net/c/473/enc_flag
--2026-08-24 19:24:10--  https://artifacts.picoctf.net/c/473/enc_flag
Resolviendo artifacts.picoctf.net (artifacts.picoctf.net)... 2600:9000:249b:a200:e:c945:f180:93a1, 2600:9000:249b:f800:e:c945:f180:93a1, 2600:9000:249b:8c00:e:c945:f180:93a1, ...
Conectando con artifacts.picoctf.net (artifacts.picoctf.net)[2600:9000:249b:a200:e:c945:f180:93a1]:443... conectado.
Petición HTTP enviada, esperando respuesta... 200 OK
Longitud: 349 [application/octet-stream]
Grabando a: «enc_flag»

enc_flag                          100%[===========================================================>]     349  --.-KB/s    en 0s      

2026-08-24 19:24:11 (10.5 MB/s) - «enc_flag» guardado [349/349]


~ 
➜ cat enc_flag
VmpGU1EyRXlUWGxTYmxKVVYwZFNWbGxyV21GV1JteDBUbFpPYWxKdFVsaFpWVlUxWVZaS1ZWWnVh
RmRXZWtab1dWWmtSMk5yTlZWWApiVVpUVm10d1VWZFdVa2RpYlZaWFZtNVdVZ3BpU0VKeldWUkNk
MlZXVlhoWGJYQk9VbFJXU0ZkcVRuTldaM0JZVWpGS2VWWkdaSGRXCk1sWnpWV3hhVm1KRk5XOVVW
VkpEVGxaYVdFMVhSbHBWV0VKVVZGWm9RMlZzV2tWUmJFNVNDbUpXV25wWmExSmhWMGRHZEdWRlZs
aGkKYlRrelZERldUMkpzUWxWTlJYTkxDZz09Cg==
```


Repetir el proceso con el resultado:

```
V1RCa2MyRnRTWGRVYkZaVFltNVNjRmRXYUU5aVJUVnhWVzFhYVdGck5UWmFSVkpQWVRGbmVWVnVR
bHBsYTBweVUxWmpNRTVHWjNsVgpXR1JyVFdwV2VsUlZVbE5oTURCNVZXMWFZUXBTTVhCelZEQlNR
bVZzYkRaWGFteEVXbm93T1VOblBUMEsK
```


```
WTBkc2FtSXdUbFZTYm5ScFdWaE9iRTVxVW1aaWFrNTZaRVJPYTFneVVuQlpla0pyU1ZjME5GZ3lV
WGRrTWpWelRVUlNhMDB5VW1aYQpSMXBzVDBSQmVsbDZXamxEWnowOUNnPT0K
```


```
Y0dsamIwTlVSbnRpWVhObE5qUmZiak56ZEROa1gyUnBZekJrSVc0NFgyUXdkMjVzTURSa00yUmZa
R1psT0RBell6WjlDZz09Cg==
```

```
cGljb0NURntiYXNlNjRfbjNzdDNkX2RpYzBkIW44X2Qwd25sMDRkM2RfZGZlODAzYzZ9Cg=
```

```
picoCTF{base64_n3st3d_dic0d!n8_d0wnl04d3d_dfe803c6}
```

**Flag**: picoCTF{base64_n3st3d_dic0d!n8_d0wnl04d3d_dfe803c6}
### Notas Adicionales

### Referencias
https://gchq.github.io/CyberChef/