### Descripción

A digital ghost has breached my defenses, and my sensitive data has been stolen! Your mission is to uncover how this phantom intruder infiltrated my system and retrieve the hidden flag. To solve this challenge, you'll need to analyze the provided PCAP file and track down the attack method. The attacker has cleverly concealed his moves in well timely manner. [myNetworkTraffic.pcap](https://challenge-files.cylabacademy.net/library/fb6cbf6a3b21ee30ba1d3211a2d6d4fa46e492a19fd414c294943edc8b8ac101/myNetworkTraffic.pcap)

### Solución

1. Descargar el `.pcap`. Son solo 22 paquetes IP "en crudo" (sin Ethernet), TCP del host `10.200.0.2` al `192.168.1.2` por el puerto 80.
2. Se parsea el pcap manualmente con Python (cabecera global de 24 bytes + cabecera de paquete de 16 bytes: `ts_sec, ts_usec, incl_len, orig_len`), y de cada paquete se extrae el payload TCP (después de la cabecera IP y TCP):

```python
   import struct, base64
   data = open('myNetworkTraffic.pcap','rb').read()
   offset = 24
   pkts = []
   while offset < len(data):
       ts_sec, ts_usec, incl_len, orig_len = struct.unpack('<IIII', data[offset:offset+16])
       offset += 16
       pkts.append((ts_usec, data[offset:offset+incl_len]))
       offset += incl_len
```

3. Cada payload es una cadena con pinta de Base64, pero la mayoría decodifican a bytes basura (ruido de relleno agregado por el atacante para despistar). Solo algunos decodifican a texto ASCII imprimible limpio.
4. La pista "concealed his moves in **well timely manner**" apunta a que el **orden real del mensaje está dado por el timestamp** (`ts_usec`) de cada paquete, no por el orden en que aparecen en el archivo. Se ordenan los paquetes por `ts_usec` y se filtran solo los que decodifican a texto imprimible:

```python
   pkts.sort(key=lambda x: x[0])
   full = ''
   for ts_usec, p in pkts:
       ihl = (p[0] & 0x0F) * 4
       tcp_hdr_len = (p[ihl+12] >> 4) * 4
       payload = p[ihl+tcp_hdr_len:]
       dec = base64.b64decode(payload)
       if all(32 <= b < 127 for b in dec):
           full += dec.decode()
   print(full)
```

5. Concatenando los fragmentos válidos en orden de timestamp se arma la flag completa.

**Flag:** `academy{1t_w4snt_th4t_34sy_tbh_4r_298cb9ba}`

### Notas Adicionales

El reto mezcla dos técnicas: (1) exfiltración de datos vía Base64 dentro de payloads TCP, y (2) paquetes señuelo (que decodifican a bytes no imprimibles) para que no sea tan directo filtrar "lo bueno" solo por el patrón Base64. La clave fue reordenar por timestamp y quedarse únicamente con los fragmentos que decodifican a texto ASCII imprimible.

### Referencias