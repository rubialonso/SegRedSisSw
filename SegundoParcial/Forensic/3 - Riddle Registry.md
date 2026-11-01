### Descripción
Hi, intrepid investigator! 📄🔍 You've stumbled upon a peculiar PDF filled with what seems like nothing more than garbled nonsense. But beware! Not everything is as it appears. Amidst the chaos lies a hidden treasure—an elusive flag waiting to be uncovered. Find the PDF file here [Hidden Confidential Document](https://challenge-files.cylabacademy.net/library/cd10271d1755c79f00fce1beff6a218832ac3678783ccfce59c111813fcb7276/confidential.pdf) and uncover the flag within the metadata.

Hints:
- Don't be fooled by the visible text; it’s just a decoy!
- Look beyond the surface for hidden clues
### Solución
1. Descargar el archivo con wget
2. Examinar el archivo con exiftool:
```
~/cylab/sp_forensic 
❯ exiftool confidential.pdf
ExifTool Version Number         : 13.25
File Name                       : confidential.pdf
Directory                       : .
File Size                       : 183 kB
File Modification Date/Time     : 2026:09:23 00:28:16-06:00
File Access Date/Time           : 2026:10:31 16:53:18-06:00
File Inode Change Date/Time     : 2026:10:31 16:53:09-06:00
File Permissions                : -rw-rw-r--
File Type                       : PDF
File Type Extension             : pdf
MIME Type                       : application/pdf
PDF Version                     : 1.7
Linearized                      : No
Page Count                      : 1
Producer                        : PyPDF2
Author                          : YWNhZGVteXtwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV80NzcwZDRlY30=
```

3. Como vemos, en el autor se muestra un texto en base64, asi que lo desciframos con el comando:
```
~/cylab/sp_forensic 
➜ echo "YWNhZGVteXtwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV80NzcwZDRlY30=" | base64 -d
academy{puzzl3d_m3tadata_f0und!_4770d4ec}
```

**Flag**: academy{puzzl3d_m3tadata_f0und!_4770d4ec}
### Notas Adicionales

### Referencias