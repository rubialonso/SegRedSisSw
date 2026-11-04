### Descripción
What can you do with this file? I forgot the key to my safe but this [file](https://challenge-files.cylabacademy.net/library/ab11765bacdcb205c97aa89731aa7bdfd295ee56ec3201559f977e30565188bf/SafeOpener.class) is supposed to help me with retrieving the lost key. Can you help me unlock my safe?

Hint: Download and try to decompile the file
### Solución
1. Descargar el archivo con wget
2. Ejecutar el comando:
```
strings -n 10 SafeOpener.class | grep aca
,academy{SAf3_0p3n3rr_y0u_solv3d_it_63446779}	
```

**Flag**: academy{SAf3_0p3n3rr_y0u_solv3d_it_63446779}
### Notas Adicionales

### Referencias