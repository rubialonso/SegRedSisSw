**Descripción:**
Help us test the form by submiting the username as `test` and password as `test!` The website running [here](http://chatelaine.cylabacademy.net:36291/).
**Solución 1:**
fui al sitio e ingrese de la siguiente manera:
![[Pasted image 20261003205405.png]]

luego con el inspeccionar mas y volviendo al link anterior hasta la base, veo lo siguiente


![[Pasted image 20261003214046.png]]

bF90aGVfd2F5X2E1Yjg0YzY2fQ==

![[Pasted image 20261003214223.png]]

YWNhZGVteXtwcm94aWVzX2Fs
pude darme cuenta que son las 2 partes de un String en base64, uniendolas en cyberchef
obtengo la bandera
![[Pasted image 20261003214335.png]]
academy{proxies_all_the_way_a5b84c66}
**Solución 2:**

**Referencias:**  
https://www.youtube.com/watch?v=3prQFqQ-h94

**Notas:**
- el navegador puede bloquear las redirecciones  y son importantes pues ahí están partes de la bandera , por eso hay que cambiar la configuración de permisos del navegador o usar otro