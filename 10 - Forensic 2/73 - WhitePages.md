### Descripción
I stopped using YellowPages and moved onto WhitePages... but [the page they gave me](https://challenge-files.cylabacademy.net/library/164023ae7e53a7b325e50a82f7cd942427fd0f38084d555c162501500fc475c3/whitepages.txt) is all blank!
Hint: There is data encoded somewhere... there might be an online decoder.
### Solución
Se paso este codigo a un archivo de python usando nano, ya solo se ejecuto y nos dio la bandera.
```
# Cargar el contenido del archivo en formato UTF-8
with open('whitepages.txt', 'r', encoding='utf-8') as f:
    data = f.read()

# Convertir los espacios invisibles en bits:
# EM Space (U+2003) -> 0
# Espacio común (U+0020) -> 1
binary_str = data.replace('\u2003', '0').replace(' ', '1')

# Convertir cada grupo de 8 bits a su carácter ASCII
decoded_bytes = bytearray()
for i in range(0, len(binary_str), 8):
    byte = binary_str[i:i+8]
    decoded_bytes.append(int(byte, 2))

# Mostrar el texto revelado
print(decoded_bytes.decode('utf-8'))
```

Esta fue la salida:
```
SEE PUBLIC RECORDS & BACKGROUND REPORT
5000 Forbes Ave, Pittsburgh, PA 15213
academy{not_all_spaces_are_created_equal_d4c2f3dcae81af992c8e86ddecdf2dd5}
```
**Flag**: academy{not_all_spaces_are_created_equal_d4c2f3dcae81af992c8e86ddecdf2dd5}
### Notas Adicionales

### Referencias