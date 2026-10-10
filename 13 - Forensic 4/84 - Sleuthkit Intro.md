### Descripción
Download the disk image and use `mmls` on it to find the size of the Linux partition. Connect to the remote checker service to check your answer and get the flag.

Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.
### Solución

```
~/cylab/sleuthintro 
➜ wget https://challenge-files.cylabacademy.net/library/d8718cbbc14dcd9f9aad532a51d7a01b00e1715ca3b1d654dfef687d0b15cbf5/disk.img.gz
--2026-10-07 11:08:47--  https://challenge-files.cylabacademy.net/library/d8718cbbc14dcd9f9aad532a51d7a01b00e1715ca3b1d654dfef687d0b15cbf5/disk.img.gz
Resolviendo challenge-files.cylabacademy.net (challenge-files.cylabacademy.net)... 18.238.132.115, 18.238.132.26, 18.238.132.88, ...
Conectando con challenge-files.cylabacademy.net (challenge-files.cylabacademy.net)[18.238.132.115]:443... conectado.
Petición HTTP enviada, esperando respuesta... 200 OK
Longitud: 29714372 (28M) [application/octet-stream]
Grabando a: «disk.img.gz»

disk.img.gz               100%[=====================================>]  28.34M   255KB/s    en 20m 55s 

2026-10-07 11:29:49 (23.1 KB/s) - «disk.img.gz» guardado [29714372/29714372]


~/cylab/sleuthintro took 21m1s 
➜ zgrip disk.img.gz
bash: zgrip: orden no encontrada

~/cylab/sleuthintro 
❯ ls -lah
total 29M
drwxrwxr-x 1 rubi rubi  22 oct  7 11:08 .
drwxrwxr-x 1 rubi rubi 15K oct  7 11:08 ..
-rw-rw-r-- 1 rubi rubi 29M sep 22 20:52 disk.img.gz

~/cylab/sleuthintro 
➜ gzip disk.img.gz
gzip: disk.img.gz already has .gz suffix -- unchanged

~/cylab/sleuthintro 
➜ ls
disk.img.gz

~/cylab/sleuthintro 
➜ gzip -d disk.img.gz

~/cylab/sleuthintro 
➜ ls
disk.img

~/cylab/sleuthintro 
➜ mmls disk.img
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000204799   0000202752   Linux (0x83)

~/cylab/sleuthintro 
➜ nc chatelaine.cylabacademy.net 35783
What is the size of the Linux partition in the given disk image?
Length in sectors: 202752
202752
Great work!
academy{mm15_f7w!}
```

**Flag**: academy{mm15_f7w!}
### Notas Adicionales

### Referencias