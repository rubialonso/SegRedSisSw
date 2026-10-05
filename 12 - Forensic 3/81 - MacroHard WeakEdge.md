### Descripción

### Solución
1. Descargamos el archivo con wget 
```
~/cylab/macrohard 
➜ wget https://challenge-files.cylabacademy.net/library/ef35dfe613527d28fe872d94179b53bc1a0497ddecf57e51d160c910be3a8e8a/Forensics_is_fun.pptm
```

2. Analizamos el archivo con binwalk, veremos que hay mas archivos empaquetados, al final aparece uno llamado hidden:
```
~/cylab/macrohard 
➜ binwalk Forensics_is_fun.pptm 
	.
	.
	.
  inflating: ppt/tableStyles.xml     
  inflating: docProps/core.xml       
  inflating: docProps/app.xml        
  inflating: ppt/slideMasters/hidden  
```

3. Le hacemos un cat, salen caracteres separados por espacios, le quitamos los espacios.
   Como sale en base 64 lo desciframos para que aparezca nuestra bandera:
```
~/cylab/macrohard 
➜ cat ppt/slideMasters/hidden
Z m x h Z z o g Y W N h Z G V t e X t E M W R f d V 9 r b j B 3 X 3 B w d H N f c l 9 6 M X A 1 f Q
~/cylab/macrohard 
➜ cat ppt/slideMasters/hidden | tr -d ' '
ZmxhZzogYWNhZGVteXtEMWRfdV9rbjB3X3BwdHNfcl96MXA1fQ
~/cylab/macrohard 

//Este comando es el bueno:
➜ cat ppt/slideMasters/hidden | tr -d ' ' | base64 -d
flag: academy{D1d_u_kn0w_ppts_r_z1p5}
```
**Flag**: academy{D1d_u_kn0w_ppts_r_z1p5}
### Notas Adicionales

### Referencias