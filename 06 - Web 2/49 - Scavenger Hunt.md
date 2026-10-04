### Descripción
There is some interesting information hidden around this site. Can you find it?
### Solución
Primero buscar en el html la primer parte:
<!-- Here's the first part of the flag: picoCTF{t -->

Luego en el CSS:
/* CSS makes the page look nice, and yes, it also has part of the flag. Here's part 2: h4ts_4_l0 */

En el js nos da la pista: /* How can I keep Google from indexing my website? */

Entrar a robots.txt:
User-agent: *
Disallow: /index.html
Part 3: t_0f_pl4c
 I think this is an apache server... can you Access the next flag?

Entrar a .htaccess
Part 4: 3s_2_lO0k
I love making websites on my Mac, I can Store a lot of information there.

Por ultimo entrar a .DS_Store:
Congrats! You've completed the scavenger hunt! Part 5: _9588550}

**Flag**: picoCTF{th4ts_4_l0t_0f_pl4c3s_2_lO0k_9588550}
### Notas Adicionales

### Referencias