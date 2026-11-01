### Descripción
Attackers have hidden information in a very large mass of data in the past, maybe they are still doing it. Download the data [here](https://challenge-files.cylabacademy.net/library/1e5b915df467718ade9bc65b9de2094f73159c40c620fbea7bfec17f657252b3/anthem.flag.txt).

Hint: Download the file and search for the flag based on the known prefix.
### Solución
1. Descargar el archivo con wget:
```
wget https://challenge-files.cylabacademy.net/library/1e5b915df467718ade9bc65b9de2094f73159c40c620fbea7bfec17f657252b3/anthem.flag.txt
```
2. Hacer un cat junto con grep para encontrar la flag:
```
~/cylab/sp_forensic 
➜ cat anthem.flag.txt | grep aca
      we think that the men of academy{gr3p_15_@w3s0m3_33595e98}
```

**Flag**: academy{gr3p_15_@w3s0m3_33595e98}
### Notas Adicionales

### Referencias