### Descripción
We found this packet capture. Recover the flag that was pilfered from the network.

### Solución
Primero hay que descargar el archivo:

```
~/cylab via 🐍 v3.13.5 (mivenv) 
➜ wget <URL-del-archivo>/shark-on-wire-2-capture.pcap

```

Luego abrimos la captura en Wireshark y filtramos el tráfico UDP con el filtro `udp`. Hay mucho tráfico de ruido, pero un flujo destaca: el de `10.0.0.66` hacia `10.0.0.1`, cuyo puerto origen cambia en cada paquete. Los demás hosts mandan paquetes con puertos fijos (por ejemplo 5000), que son señuelos.

Cada puerto origen de ese flujo, menos 5000, es el código ASCII de un carácter:

```
5097 - 5000 = 97  -> 'a'
5099 - 5000 = 99  -> 'c'
5097 - 5000 = 97  -> 'a'
...
```

Para sacarlo con Wireshark, usa el filtro `ip.src == 10.0.0.66 && ip.dst == 10.0.0.1 && udp`, anota los puertos origen en orden, réstales 5000 y conviértelos a ASCII. Si prefieres un script, este es un parser mínimo en Python que no necesita librerías externas:

```python
import struct

d = open('shark-on-wire-2-capture.pcap', 'rb').read()
i, flag = 24, ''
while i + 16 <= len(d):
    cl = struct.unpack('<I', d[i+8:i+12])[0]
    p = d[i+16:i+16+cl]; i += 16 + cl
    ip = p[14:]
    if len(ip) < 28 or ip[0] >> 4 != 4 or ip[9] != 17:
        continue
    src, dst = ip[12:16], ip[16:20]
    if src == bytes([10,0,0,66]) and dst == bytes([10,0,0,1]):
        sport = struct.unpack('>H', ip[20:22])[0]
        c = sport - 5000
        if 32 <= c < 127:
            flag += chr(c)
print(flag)
```

Flag: academy{p1LLf3r3d_data_v1a_st3g0}

### Notas Adicionales
- Es un caso de esteganografía de red: el mensaje no va en el contenido de los paquetes, sino en un campo de cabecera (el puerto origen UDP).
- El primer paquete del flujo da un carácter no imprimible, que se descarta.
- Otros hosts (`10.0.0.75`, `10.0.0.2`, etc.) envían tráfico parecido, pero solo dan letras repetidas o basura. Son señuelos.
- Si el resultado no sale, comprueba que filtras por host origen y destino, y que mantienes el orden de los paquetes.

### Referencias
- Wireshark, filtros de visualización: https://wiki.wireshark.org/DisplayFilters
- Tabla ASCII: https://www.asciitable.com/