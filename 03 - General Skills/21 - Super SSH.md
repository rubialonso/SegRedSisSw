### Descripción
  Using a Secure Shell (SSH) is going to be pretty important.

Can you `ssh` as `ctf-player` to `titan.picoctf.net` at port `60882` to get the flag?

You'll also need the password `6dd28e9b`. If asked, accept the fingerprint with `yes`.

If your device doesn't have a shell, you can use: [](https://webshell.picoctf.org/)[https://webshell.picoctf.org](https://webshell.picoctf.org/)

If you're not sure what a shell is, check out our Primer: [](https://primer.picoctf.com/#_the_shell)[https://primer.picoctf.com/#_the_shell](https://primer.picoctf.com/#_the_shell)

Hints
 - https://linux.die.net/man/1/ssh
-  You can try logging in 'as' someone with `<user>`@titan.picoctf.net
-  How could you specify the port?
* Remember, passwords are hidden when typed into the shell
### Solución
```
~ 
➜ ssh ctf-player@titan.picoctf.net -p 60882

The authenticity of host '[titan.picoctf.net]:60882 ([3.139.174.234]:60882)' can't be established.
ED25519 key fingerprint is: SHA256:4S9EbTSSRZm32I+cdM5TyzthpQryv5kudRP9PIKT7XQ
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[titan.picoctf.net]:60882' (ED25519) to the list of known hosts.
** WARNING: connection is not using a post-quantum key exchange algorithm.
** This session may be vulnerable to "store now, decrypt later" attacks.
** The server may need to be upgraded. See https://openssh.com/pq.html
ctf-player@titan.picoctf.net's password: 
Welcome ctf-player, here's your flag: picoCTF{s3cur3_c0nn3ct10n_5d09a462}
Connection to titan.picoctf.net closed.
```

**Flag**: picoCTF{s3cur3_c0nn3ct10n_5d09a462}
### Notas Adicionales

### Referencias