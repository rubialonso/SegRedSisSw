### Descripción
This file contains more than it seems. Get the flag from [garden.jpg](https://challenge-files.cylabacademy.net/library/29dc79fc1e76c1c4f57311a5649e686a42aee58e6b401e81acd7daef441459c1/garden.jpg).
What is a hex editor?
### Solución
Descargar la imagen con wget
```
~/cylab 
➜ wget https://challenge-files.cylabacademy.net/library/29dc79fc1e76c1c4f57311a5649e686a42aee58e6b401e81acd7daef441459c1/garden.jpg

```

Si le hacemos cat al archivo salen muchos caracteres, entonces vamos a pedir en cadena el archivo:
```
~/cylab 
➜ strings garden.jpg | grep academy
Here is a flag: academy{more_than_m33ts_the_3y3ee53c6bc}
```

### Solución 2
usar el comando xxd garden.jpg

**Flag**: academy{more_than_m33ts_the_3y3ee53c6bc}

### Notas Adicionales

### Referencias