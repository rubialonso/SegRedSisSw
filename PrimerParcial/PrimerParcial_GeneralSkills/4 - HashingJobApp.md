### Descripción
If you want to hash with the best, beat this test! `nc xebec.cylabacademy.net 22624`

Hints
1. You can use a commandline tool or web app to hash text
2. Press Ctrl and c on your keyboard to close your connection and return to the command prompt.
### Solución
1 . Crear un archivo con nano y meter el siguiente script de pyhton, reemplazando el servidor y el puerto que esta activo en la instancia:
```
~/cylab via 🐍 v3.13.5 took 39s 
➜ cat solve.py
import socket
import hashlib
import re

# Reemplaza el host y el puerto con los de tu instancia
host = 'xebec.cylabacademy.net'
port = 46703 

def solve():
    # Conectamos al servidor usando sockets puros
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.connect((host, port))
    
    # Bucle para resolver los 3 desafíos
    for i in range(3):
        buffer = ""
        # Leer datos hasta que el servidor pida la respuesta
        while "Answer:" not in buffer:
            chunk = s.recv(1024).decode('utf-8')
            if not chunk: break
            buffer += chunk
            
        # Buscar el texto que está entre comillas simples
        match = re.search(r"quotes:\s*'([^']+)'", buffer)
        if match:
            texto = match.group(1)
            print(f"[*] Texto recibido: {texto}")
            
            # Calcular el hash MD5
            hash_md5 = hashlib.md5(texto.encode()).hexdigest()
            print(f"[*] Enviando Hash: {hash_md5}")
            
            # Enviar el hash seguido de un salto de línea
            s.sendall((hash_md5 + "\n").encode())
            
    # Leer e imprimir la bandera final
    print("\n[+] Bandera obtenida:")
    respuesta_final = s.recv(4096).decode('utf-8')
    print(respuesta_final)
    
    s.close()

if __name__ == '__main__':
    solve()
```

2. Ejecutamos el archivo de python:
```
~/cylab via 🐍 v3.13.5 took 41s 
➜ python3 solve.py 
[*] Texto recibido: Japan
[*] Enviando Hash: 53a577bb3bc587b0c28ab808390f1c9b
[*] Texto recibido: a treehouse
[*] Enviando Hash: 98b0ee4dfd8e04322c60bd32481b512e
[*] Texto recibido: Clint Eastwood
[*] Enviando Hash: b84954cb41831fa842dd69f6e1836b6e

[+] Bandera obtenida:
b84954cb41831fa842dd69f6e1836b6e
Correct.
academy{4ppl1c4710n_r3c31v3d_467e06bf}
```

**Flag**: academy{4ppl1c4710n_r3c31v3d_467e06bf}
### Notas Adicionales

### Referencias