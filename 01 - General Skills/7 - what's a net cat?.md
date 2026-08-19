### Descripción
Using netcat (nc) is going to be pretty important. Can you connect to fickle-tempest.picoctf.net at port 49384 to get the flag?

pista >   nc tutorial
### Solución
Ir a la terminal y ejecutar:
```
nc -z -v fickle-tempest.picoctf.net 49384

>>> DNS fwd/rev mismatch: fickle-tempest.picoctf.net != ec2-3-137-126-208.us-east-2.compute.amazonaws.com
fickle-tempest.picoctf.net [3.137.126.208] 49384 (?) open

nc -v 3.137.126.208 49384
>>>ec2-3-137-126-208.us-east-2.compute.amazonaws.com [3.137.126.208] 49384 (?) open
You're on your way to becoming the net cat master
picoCTF{nEtCat_Mast3ry_5c7cC1a9}

```

**Flag**: 
### Notas Adicionales
* nc - es una herramienta de red que permite conectarse a un servidor en un puerto especifico

### Referencias