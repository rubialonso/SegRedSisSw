### Descripción
  
Sometimes you need to handle process data outside of a file. Can you find a way to keep the output from this program and search for the flag?

Connect to fickle-tempest.picoctf.net 61191
### Solución
```
➜ nc fickle-tempest.picoctf.net 61191 > flag

➜ cat flag | grep pico
picoCTF{digital_plumb3r_A01Bc3eC}
```

**Flag**: picoCTF{digital_plumb3r_A01Bc3eC}
### Notas Adicionales
 * > se utiliza para redirigir la salida de cualquier comando a un archivo de texto
 * | la barra vertical o pipe redirige la salida de un comando a otro comando

### Referencias