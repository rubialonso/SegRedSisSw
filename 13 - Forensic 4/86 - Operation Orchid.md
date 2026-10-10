### Descripción
Download this disk image and find the flag.

Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.
### Solución
1. Descargamos el archivo y luego se descomprime, todo se realizo en la carpeta de tmp:
```
/tmp/operationorchid 
➜ wget https://challenge-files.cylabacademy.net/library/c43b9c25ad2c97fb0c7c393a7b5f95065b79c0faf5848e1eeb6a453ec3e78f7d/disk.flag.img.gz

/tmp/operationorchid took 18s 
➜ gzip -d disk.flag.img.gz 	
```

2. Eejcutamos los siguientes comandos:
```
/tmp/operationorchid took 3s 
➜ mmls disk.flag.img 
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000206847   0000204800   Linux (0x83)
003:  000:001   0000206848   0000411647   0000204800   Linux Swap / Solaris x86 (0x82)
004:  000:002   0000411648   0000819199   0000407552   Linux (0x83)

/tmp/operationorchid 
➜ fls -o 411648 -r disk.flag.img | grep -i "flag"
+ r/r * 1876(realloc):	flag.txt
+ r/r 1782:	flag.txt.enc

/tmp/operationorchid 
➜ icat -o 411648 disk.flag.img 1782
Salted__�v �S>�!�jfo(�s:�Kr�ـd�I/Uq�+����fȤ7� ���؎$�'%

/tmp/operationorchid 
➜ fls -o 411648 -r disk.flag.img | grep -i "history"
+ r/r 1875:	.ash_history

/tmp/operationorchid 
➜ icat -o 411648 disk.flag.img 1875
touch flag.txt
nano flag.txt 
apk get nano
apk --help
apk add nano
nano flag.txt 
openssl
openssl aes256 -salt -in flag.txt -out flag.txt.enc -k unbreakablepassword1234567
shred -u flag.txt
ls -al
halt

/tmp/operationorchid 
❯ openssl aes-256-cbc -d salt -in flag.txt.enc -out flag.txt -k unbreakablepassword1234567
aes-256-cbc: Extra option: "salt"
aes-256-cbc: Use -help for summary.

/tmp/operationorchid 
❯ cat flag.txt
academy{h4un71ng_p457_0cf3a06d}

```


**Flag**: academy{h4un71ng_p457_0cf3a06d}
### Notas Adicionales

### Referencias