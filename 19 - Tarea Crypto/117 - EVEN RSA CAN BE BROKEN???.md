### Descripción
This service provides you an encrypted flag. Can you decrypt it with just N & e?
Hints:
- How much do we trust randomness?
- Notice anything interesting about N?
-  Try comparing N across multiple requests
### Solución
1. Descargar el archivo con wget
2. Hacer la conexión con el nc que nos dan de la instancia: nc chatelaine.cylabacademy.net 35408
3. Ahora en un archivo de python le pasamos el siguiente codigo cambiando los datos que nos dan en la conexión. **OJO:** hay que tener un entorno virtual creado e instalar *pip install pycryptodome* :
```
from Crypto.Util.number import long_to_bytes  
  
N = <given_even_N>  #aquii reemplazamos
e = 65537  
  
q = N // 2  
phi_N = q - 1  
d = pow(e, -1, phi_N)  
  
c = <given_ciphertext>  #aqui también
m = pow(c, d, N)  
flag = long_to_bytes(m)  
print(flag)	
```
4. Ejecutar el programa para que nos de la flag:
```
~/cylab via 🐍 v3.13.5 (venv) took 9s 
➜ python script_rsa.py
b'academy{tw0_1$_pr!m3cfb893a9}'
```
**Flag**: academy{tw0_1$_pr!m3cfb893a9}
### Notas Adicionales

### Referencias